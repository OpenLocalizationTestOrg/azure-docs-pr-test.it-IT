---
title: "Come usare Twilio per le funzionalità voce e SMS (Java) | Microsoft Docs"
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Gli esempi di codice sono scritti in Java.
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="76bf7-104">Come usare Twilio per le funzionalità voce ed SMS in Java</span><span class="sxs-lookup"><span data-stu-id="76bf7-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="76bf7-105">In questa guida viene illustrato come eseguire attività di programmazione comuni con il servizio API Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="76bf7-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="76bf7-106">Gli scenari presentati includono la composizione di una chiamata telefonica e l'invio di un messaggio SMS (Short Message Service).</span><span class="sxs-lookup"><span data-stu-id="76bf7-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="76bf7-107">Per altre informazioni su Twilio e sull'utilizzo delle funzionalità voce ed SMS nelle applicazioni, vedere la sezione [Passaggi successivi](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="76bf7-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="76bf7-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="76bf7-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="76bf7-109">Twilio è un'API per servizi Web di telefonia che consente di usare le competenze e i linguaggi Web esistenti per sviluppare applicazioni SMS e vocali.</span><span class="sxs-lookup"><span data-stu-id="76bf7-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="76bf7-110">Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76bf7-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="76bf7-111">**Twilio Voice** consente alle applicazioni di effettuare e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="76bf7-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="76bf7-112">**Twilio SMS** consente alle applicazioni di inviare e ricevere SMS.</span><span class="sxs-lookup"><span data-stu-id="76bf7-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="76bf7-113">**Twilio Client** consente alle applicazioni di abilitare le comunicazioni vocali utilizzando le connessioni Internet esistenti, comprese le connessioni mobili.</span><span class="sxs-lookup"><span data-stu-id="76bf7-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="76bf7-114"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="76bf7-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="76bf7-115">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="76bf7-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="76bf7-116">Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="76bf7-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="76bf7-117">Per avvalersi dell'offerta o per altre informazioni, visitare il sito Web all'indirizzo [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="76bf7-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="76bf7-118"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="76bf7-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="76bf7-119">L'API Twilio è un'API RESTful che fornisce funzionalità voce ed SMS per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="76bf7-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="76bf7-120">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="76bf7-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="76bf7-121">I concetti principali dell'API Twilio sono costituiti dai verbi Twilio e dal linguaggio di markup Twilio (Twilio Markup Language, TwiML).</span><span class="sxs-lookup"><span data-stu-id="76bf7-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="76bf7-122"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="76bf7-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="76bf7-123">Nell'API vengono usati i verbi di Twilio: il verbo **&lt;Say&gt;**, ad esempio, indica a Twilio di recapitare un messaggio acustico in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="76bf7-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="76bf7-124">Di seguito è riportato un elenco dei verbi Twilio.</span><span class="sxs-lookup"><span data-stu-id="76bf7-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="76bf7-125">**&lt;Dial&gt;**: connette il chiamante a un altro telefono.</span><span class="sxs-lookup"><span data-stu-id="76bf7-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="76bf7-126">**&lt;Gather&gt;**: raccoglie i numeri digitati sulla tastiera del telefono.</span><span class="sxs-lookup"><span data-stu-id="76bf7-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="76bf7-127">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="76bf7-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="76bf7-128">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="76bf7-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="76bf7-129">**&lt;Queue&gt;**: aggiunge l'elemento a una coda di chiamanti.</span><span class="sxs-lookup"><span data-stu-id="76bf7-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="76bf7-130">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="76bf7-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="76bf7-131">**&lt;Record&gt;**: registra la voce del chiamante e restituisce l'URL del file contenente la registrazione.</span><span class="sxs-lookup"><span data-stu-id="76bf7-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="76bf7-132">**&lt;Redirect&gt;**: trasferisce il controllo di una chiamata o di un SMS al codice TwiML presso un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="76bf7-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="76bf7-133">**&lt;Reject&gt;**: rifiuta una chiamata in arrivo al numero Twilio senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="76bf7-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="76bf7-134">**&lt;Say&gt;**: effettua la sintesi vocale del testo durante una chiamata.</span><span class="sxs-lookup"><span data-stu-id="76bf7-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="76bf7-135">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="76bf7-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="76bf7-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="76bf7-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="76bf7-137">TwiML è un set di istruzioni basate su XML e sui verbi Twilio che indicano a Twilio come elaborare una chiamata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="76bf7-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="76bf7-138">Ad esempio, il codice TwiML seguente effettua la sintesi vocale del testo **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="76bf7-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="76bf7-139">sintesi vocale.</span><span class="sxs-lookup"><span data-stu-id="76bf7-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="76bf7-140">Quando l'applicazione chiama l'API Twilio, uno dei parametri dell'API è l'URL che restituisce la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="76bf7-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="76bf7-141">Ai fini dello sviluppo, è possibile utilizzare gli URL offerti da Twilio per fornire le risposte TwiML utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="76bf7-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="76bf7-142">È inoltre possibile ospitare gli URL per produrre le risposte TwiML oppure utilizzare l'oggetto **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="76bf7-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="76bf7-143">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="76bf7-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="76bf7-144">Per altre informazioni sull'API Twilio, vedere [Twilio API][twilio_api] (API Twilio).</span><span class="sxs-lookup"><span data-stu-id="76bf7-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="76bf7-145"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="76bf7-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="76bf7-146">Se si desidera creare un account Twilio, iscriversi nella pagina [Try Twilio][try_twilio] (Provare Twilio).</span><span class="sxs-lookup"><span data-stu-id="76bf7-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="76bf7-147">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="76bf7-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="76bf7-148">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="76bf7-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="76bf7-149">Entrambe queste informazioni sono necessarie per effettuare chiamate all'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="76bf7-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="76bf7-150">Per prevenire accessi autorizzati all'account, conservare il token di autenticazione in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="76bf7-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="76bf7-151">L'ID account e il token di autorizzazione sono visualizzabili nella [console di Twilio][twilio_console], rispettivamente nei campi **ACCOUNT SID** (SID ACCOUNT) e **AUTH TOKEN** (TOKEN AUTORIZZAZIONE).</span><span class="sxs-lookup"><span data-stu-id="76bf7-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="76bf7-152"><a id="create_app"></a>Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="76bf7-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="76bf7-153">Ottenere il file JAR di Twilio e aggiungerlo al percorso di compilazione Java e all'assembly di distribuzione del file WAR.</span><span class="sxs-lookup"><span data-stu-id="76bf7-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="76bf7-154">Dall'indirizzo [https://github.com/twilio/twilio-java][twilio_java] è possibile scaricare i file di origine disponibili in GitHub e creare un file JAR personalizzato o scaricarne uno precompilato, con o senza dipendenze.</span><span class="sxs-lookup"><span data-stu-id="76bf7-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="76bf7-155">Verificare che l'archivio chiavi **cacerts** del JDK contenga il certificato Equifax Secure Certificate Authority con ID digitale MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (il numero di serie è 35:DE:F4:CF e l'ID digitale SHA1 è D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="76bf7-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="76bf7-156">Si tratta del certificato dell'Autorità di certificazione (CA) per il servizio [https://api.twilio.com][twilio_api_service], che viene chiamato quando si usano le API Twilio.</span><span class="sxs-lookup"><span data-stu-id="76bf7-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="76bf7-157">Per informazioni su come verificare che l'archivio chiavi **cacerts** del JDK contenga il certificato CA corretto, vedere [Aggiunta di un certificato all'archivio certificati CA Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="76bf7-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="76bf7-158">Per istruzioni dettagliate sull'uso della libreria client Twilio per Java, vedere [Come effettuare una chiamata tramite Twilio in un'applicazione Java in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="76bf7-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="76bf7-159"><a id="configure_app"></a>Configurare l'applicazione per l'uso delle librerie Twilio</span><span class="sxs-lookup"><span data-stu-id="76bf7-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="76bf7-160">All'interno del codice è possibile aggiungere istruzioni **import** nella parte superiore dei file di origine per i pacchetti o le classi Twilio da utilizzare nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="76bf7-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="76bf7-161">Per i file di origine Java:</span><span class="sxs-lookup"><span data-stu-id="76bf7-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="76bf7-162">Per i file di origine JSP (Java Server Page):</span><span class="sxs-lookup"><span data-stu-id="76bf7-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="76bf7-163">Le istruzioni **import** possono variare in base ai pacchetti o alle classi Twilio che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="76bf7-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="76bf7-164"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="76bf7-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="76bf7-165">Di seguito è illustrato come effettuare una chiamata in uscita usando la classe **Call**.</span><span class="sxs-lookup"><span data-stu-id="76bf7-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="76bf7-166">Questo codice utilizza inoltre un sito fornito da Twilio per restituire la risposta TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="76bf7-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="76bf7-167">Sostituire i valori di **from_number** e **to_number** relativi ai numeri di telefono e, prima di eseguire il codice, verificare il numero di telefono specificato in **from_number** per l'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="76bf7-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="76bf7-168">Per altre informazioni sui parametri passati al metodo **Call.creator**, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="76bf7-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="76bf7-169">Come indicato in precedenza, questo codice utilizza un sito fornito da Twilio per restituire la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="76bf7-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="76bf7-170">Per fornire la risposta TwiML è inoltre possibile usare il proprio sito. Per altre informazioni, vedere [Procedura per fornire risposte TwiML in un'applicazione Java in Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="76bf7-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="76bf7-171"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="76bf7-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="76bf7-172">La schermata seguente mostra come inviare un messaggio SMS usando la classe **Message**.</span><span class="sxs-lookup"><span data-stu-id="76bf7-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="76bf7-173">Il numero riportato in **from_number**, **4155992671**, è fornito da Twilio per l'invio di messaggi SMS con gli account di valutazione.</span><span class="sxs-lookup"><span data-stu-id="76bf7-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="76bf7-174">Il numero riportato in **to_number** deve essere verificato per l'account Twilio prima dell'esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="76bf7-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="76bf7-175">Per altre informazioni sui parametri passati al metodo **Message.creator**, vedere [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="76bf7-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="76bf7-176"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="76bf7-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="76bf7-177">Quando l'applicazione avvia una chiamata all'API Twilio, ad esempio tramite il metodo **CallCreator.create**, Twilio invia la richiesta a un URL che deve restituire una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="76bf7-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="76bf7-178">Nell'esempio precedente viene usato l'URL fornito da Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="76bf7-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="76bf7-179">Poiché TwiML è progettato per essere usato da servizi Web, è possibile visualizzare il codice TwiML nel browser.</span><span class="sxs-lookup"><span data-stu-id="76bf7-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="76bf7-180">Ad esempio, fare clic su [http://twimlets.com/message][twimlet_message_url] per visualizzare un elemento **&lt;Response&gt;** vuoto oppure fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] per visualizzare un elemento **&lt;Response&gt;** contenente un elemento **&lt;Say&gt;**.</span><span class="sxs-lookup"><span data-stu-id="76bf7-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="76bf7-181">Anziché utilizzare l'URL fornito da Twilio, è possibile creare un sito Web personalizzato che restituisce risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="76bf7-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="76bf7-182">È possibile creare il sito in qualsiasi linguaggio che restituisca risposte XML. In questo argomento si presuppone che l'URL sarà ospitato in una pagina JSP.</span><span class="sxs-lookup"><span data-stu-id="76bf7-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="76bf7-183">La pagina JSP seguente genera una risposta TwiML **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="76bf7-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="76bf7-184">nella chiamata.</span><span class="sxs-lookup"><span data-stu-id="76bf7-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="76bf7-185">La pagina JSP seguente crea una risposta TwiML che pronuncia del testo, contiene diverse pause e pronuncia informazioni sulla versione dell'API Twilio e sul nome del ruolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="76bf7-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="76bf7-186">Il parametro **ApiVersion** è disponibile nelle richieste vocali Twilio, non nelle richieste SMS.</span><span class="sxs-lookup"><span data-stu-id="76bf7-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="76bf7-187">Per visualizzare i parametri di richiesta disponibili per le richieste vocali e SMS di Twilio, vedere rispettivamente <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request>.</span><span class="sxs-lookup"><span data-stu-id="76bf7-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="76bf7-188">La variabile di ambiente **RoleName** è disponibile come parte di una distribuzione Azure.</span><span class="sxs-lookup"><span data-stu-id="76bf7-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="76bf7-189">Se si vuole aggiungere variabili di ambiente personalizzate in modo che possano essere recuperate da **System.getenv**, vedere la sezione relativa alle variabili di ambiente in [Impostazioni varie di configurazione dei ruoli][misc_role_config_settings].</span><span class="sxs-lookup"><span data-stu-id="76bf7-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="76bf7-190">Dopo aver configurato la pagina JSP in modo che vengano fornite risposte TwiML, usare l'URL della pagina JSP come URL passato nel metodo **Call.creator**.</span><span class="sxs-lookup"><span data-stu-id="76bf7-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="76bf7-191">Se, ad esempio, si dispone di un'applicazione Web denominata MyTwiML distribuita in un servizio ospitato in Azure e il nome della pagina JSP è mytwiml.jsp, è possibile passare l'URL a **Call.creator** come illustrato nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="76bf7-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="76bf7-192">Un'altra possibilità per rispondere con TwiML consiste nell'usare la classe **VoiceResponse**, disponibile nel pacchetto **com.twilio.twiml**.</span><span class="sxs-lookup"><span data-stu-id="76bf7-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="76bf7-193">Per altre informazioni sull'uso di Twilio in Azure con Java, vedere [Come effettuare una chiamata tramite Twilio in un'applicazione Java in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="76bf7-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="76bf7-194"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="76bf7-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="76bf7-195">Oltre agli esempi illustrati in questa pagina, Twilio offre API basate su Web che è possibile utilizzare per sfruttare altre funzionalità di Twilio dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="76bf7-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="76bf7-196">Per informazioni dettagliate, vedere la [documentazione sull'API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="76bf7-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="76bf7-197"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76bf7-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="76bf7-198">Dopo aver appreso le nozioni di base sul servizio Twilio, utilizzare i collegamenti seguenti per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="76bf7-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="76bf7-199">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="76bf7-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="76bf7-200">[Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)</span><span class="sxs-lookup"><span data-stu-id="76bf7-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="76bf7-201">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="76bf7-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="76bf7-202">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="76bf7-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="76bf7-203">[Talk to Twilio Support][twilio_support] (Contattare il supporto di Twilio)</span><span class="sxs-lookup"><span data-stu-id="76bf7-203">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
