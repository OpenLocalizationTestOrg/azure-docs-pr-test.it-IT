---
title: aaaHow tooUse Twilio per vocali e SMS (linguaggio) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Gli esempi di codice sono scritti in Java.
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
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="70f66-104">Come tooUse Twilio per funzionalità voce ed SMS in Java</span><span class="sxs-lookup"><span data-stu-id="70f66-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="70f66-105">Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="70f66-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="70f66-106">scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message).</span><span class="sxs-lookup"><span data-stu-id="70f66-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="70f66-107">Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.</span><span class="sxs-lookup"><span data-stu-id="70f66-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="70f66-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="70f66-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="70f66-109">Twilio è un'API web-servizio di telefonia che consente di utilizzare i linguaggi web esistenti e vocale toobuild competenze e le applicazioni di SMS.</span><span class="sxs-lookup"><span data-stu-id="70f66-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="70f66-110">Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70f66-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="70f66-111">**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="70f66-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="70f66-112">**SMS Twilio** consente toomake le applicazioni e la ricezione di messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="70f66-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="70f66-113">**Twilio Client** consente alle applicazioni comunicazioni vocali tooenable tramite connessioni Internet esistenti, incluse le connessioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="70f66-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="70f66-114"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="70f66-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="70f66-115">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="70f66-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="70f66-116">Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="70f66-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="70f66-117">toosign per questa offerta o ottenere ulteriori informazioni, visitare [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="70f66-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="70f66-118"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="70f66-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="70f66-119">API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="70f66-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="70f66-120">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="70f66-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="70f66-121">Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="70f66-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="70f66-122"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="70f66-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="70f66-123">Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="70f66-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="70f66-124">Hello seguito è riportato un elenco dei verbi di Twilio.</span><span class="sxs-lookup"><span data-stu-id="70f66-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="70f66-125">**&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="70f66-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="70f66-126">**&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.</span><span class="sxs-lookup"><span data-stu-id="70f66-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="70f66-127">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="70f66-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="70f66-128">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="70f66-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="70f66-129">**&lt;Coda&gt;**: aggiungere hello tooa coda dei chiamanti.</span><span class="sxs-lookup"><span data-stu-id="70f66-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="70f66-130">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="70f66-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="70f66-131">**&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="70f66-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="70f66-132">**&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="70f66-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="70f66-133">**&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si.</span><span class="sxs-lookup"><span data-stu-id="70f66-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="70f66-134">**&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="70f66-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="70f66-135">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="70f66-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="70f66-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="70f66-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="70f66-137">TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.</span><span class="sxs-lookup"><span data-stu-id="70f66-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="70f66-138">Ad esempio, hello seguente TwiML conversione testo hello **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="70f66-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="70f66-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="70f66-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="70f66-140">Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="70f66-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="70f66-141">A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="70f66-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="70f66-142">È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.</span><span class="sxs-lookup"><span data-stu-id="70f66-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="70f66-143">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="70f66-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="70f66-144">Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="70f66-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="70f66-145"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="70f66-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="70f66-146">Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="70f66-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="70f66-147">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="70f66-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="70f66-148">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="70f66-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="70f66-149">Entrambi saranno necessari toomake Twilio API chiamate.</span><span class="sxs-lookup"><span data-stu-id="70f66-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="70f66-150">non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="70f66-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="70f66-151">L'ID account e l'autenticazione token possono essere visualizzati in hello [Twilio Console][twilio_console]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="70f66-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="70f66-152"><a id="create_app"></a>Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="70f66-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="70f66-153">Ottenere hello JAR Twilio e aggiungerlo tooyour percorso e l'assembly di distribuzione WAR di compilazione Java.</span><span class="sxs-lookup"><span data-stu-id="70f66-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="70f66-154">In [https://github.com/twilio/twilio-java][twilio_java], è possibile scaricare origini GitHub hello e creare la propria JAR o scaricare un file JAR preesistente (con o senza dipendenze).</span><span class="sxs-lookup"><span data-stu-id="70f66-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="70f66-155">Verificare che il pacchetto JDK **cacerts** keystore contiene un certificato di autorità di certificazione sicura Equifax hello con 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numero di serie hello è 35:DE:F4:CF e hello SHA1 impronta digitale è D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="70f66-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="70f66-156">Questo è certificato di autorità di certificazione certificato hello per hello [https://api.twilio.com] [ twilio_api_service] servizio, che viene chiamato quando si utilizza Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="70f66-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="70f66-157">Per informazioni su come assicurare il JDK **cacerts** keystore contiene hello corretta autorità di certificazione, vedere [aggiunta di un archivio certificati Autorità di certificazione di Java di toohello certificato][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="70f66-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="70f66-158">Istruzioni dettagliate per l'utilizzo della libreria client di hello Twilio per Java sono disponibili in [come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="70f66-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="70f66-159"><a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="70f66-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="70f66-160">All'interno del codice, è possibile aggiungere **importare** istruzioni nella parte superiore di hello dei file di origine per hello Twilio pacchetti o le classi si desidera toouse nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70f66-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="70f66-161">Per i file di origine Java:</span><span class="sxs-lookup"><span data-stu-id="70f66-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="70f66-162">Per i file di origine JSP (Java Server Page):</span><span class="sxs-lookup"><span data-stu-id="70f66-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="70f66-163">A seconda di quale Twilio pacchetti o le classi si desideri toouse, il **importare** istruzioni potrebbero essere diverse.</span><span class="sxs-lookup"><span data-stu-id="70f66-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="70f66-164"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="70f66-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="70f66-165">Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **chiamare** classe.</span><span class="sxs-lookup"><span data-stu-id="70f66-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="70f66-166">Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="70f66-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="70f66-167">Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.</span><span class="sxs-lookup"><span data-stu-id="70f66-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="70f66-168">Per ulteriori informazioni sui parametri hello passato toohello **Call.creator** metodo, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="70f66-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="70f66-169">Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta.</span><span class="sxs-lookup"><span data-stu-id="70f66-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="70f66-170">È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte in un'applicazione Java in Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="70f66-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="70f66-171"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="70f66-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="70f66-172">Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello **messaggio** classe.</span><span class="sxs-lookup"><span data-stu-id="70f66-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="70f66-173">Hello **da** numero, **4155992671**, viene fornito da Twilio per versione di valutazione account toosend messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="70f66-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="70f66-174">Hello **a** numero deve essere verificato per il codice di hello Twilio account toorunning precedente.</span><span class="sxs-lookup"><span data-stu-id="70f66-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="70f66-175">Per ulteriori informazioni sui parametri hello passato toohello **Message.creator** metodo, vedere [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="70f66-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="70f66-176"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="70f66-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="70f66-177">Quando l'applicazione avvia toohello una chiamata API di Twilio, ad esempio tramite hello **CallCreator.create** , Twilio verrà inviato l'URL tooa richiesta tooreturn prevista una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="70f66-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="70f66-178">esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="70f66-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="70f66-179">(Mentre TwiML deve essere utilizzato dai servizi Web, è possibile visualizzare hello TwiML nel browser.</span><span class="sxs-lookup"><span data-stu-id="70f66-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="70f66-180">Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota  **&lt;risposta&gt;**  elemento; ad esempio, fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee un  **&lt;risposta&gt;**  elemento che contiene un  **&lt;pronuncia &gt;**  elemento.)</span><span class="sxs-lookup"><span data-stu-id="70f66-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="70f66-181">Anziché basarsi sul URL fornito Twilio hello, è possibile creare un URL sito che restituisce le risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="70f66-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="70f66-182">È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte HTTP. In questo argomento si presuppone che si sarà hosting hello URL in una pagina JSP.</span><span class="sxs-lookup"><span data-stu-id="70f66-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="70f66-183">Hello seguente JSP pagina risultati in una risposta TwiML indicante **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="70f66-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="70f66-184">chiamata di hello.</span><span class="sxs-lookup"><span data-stu-id="70f66-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="70f66-185">Hello seguente JSP pagina risultati in una risposta TwiML che indica un testo, che indica le informazioni sulla versione dell'API di Twilio hello e nome del ruolo Azure hello ha diverse pause.</span><span class="sxs-lookup"><span data-stu-id="70f66-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="70f66-186">Hello **ApiVersion** parametro è disponibile nelle richieste di Twilio vocale (non richieste SMS).</span><span class="sxs-lookup"><span data-stu-id="70f66-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="70f66-187">parametri di richiesta disponibili hello toosee vocale Twilio e richieste SMS, vedere <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="70f66-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="70f66-188">Hello **RoleName** variabile di ambiente è disponibile come parte di una distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="70f66-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="70f66-189">(Se si desidera che le variabili di ambiente personalizzato tooadd pertanto potrebbe essere prelevati dal **System.getenv**, vedere la sezione di variabili di ambiente hello al [varie impostazioni di configurazione di ruolo] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="70f66-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="70f66-190">Dopo aver creato la pagina JSP imposta tooprovide TwiML risposte, usare hello URL della pagina JSP hello come hello URL passato hello **Call.creator** metodo.</span><span class="sxs-lookup"><span data-stu-id="70f66-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="70f66-191">Ad esempio, se si dispone di un'applicazione Web denominata tooan MyTwiML distribuiti servizio ospitato di Azure e hello pagina JSP hello è denominato mytwiml.jsp, hello URL può essere passato troppo**Call.creator** come illustrato nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="70f66-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="70f66-192">È un'altra opzione per la risposta con TwiML tramite hello **VoiceResponse** (classe), disponibile in hello **com.twilio.twiml** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="70f66-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="70f66-193">Per ulteriori informazioni sull'utilizzo di Twilio in Azure con Java, vedere [come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="70f66-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="70f66-194"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="70f66-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="70f66-195">Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="70f66-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="70f66-196">Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="70f66-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="70f66-197"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70f66-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="70f66-198">Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:</span><span class="sxs-lookup"><span data-stu-id="70f66-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="70f66-199">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="70f66-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="70f66-200">[Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)</span><span class="sxs-lookup"><span data-stu-id="70f66-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="70f66-201">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="70f66-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="70f66-202">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="70f66-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="70f66-203">[Comunicare tooTwilio supporto][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="70f66-203">[Talk tooTwilio Support][twilio_support]</span></span>

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
