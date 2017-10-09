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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Come tooUse Twilio per funzionalità voce ed SMS in Java
Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure. scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message). Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.

## <a id="WhatIs"></a>Informazioni su Twilio
Twilio è un'API web-servizio di telefonia che consente di utilizzare i linguaggi web esistenti e vocale toobuild competenze e le applicazioni di SMS. Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.

**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche. **SMS Twilio** consente toomake le applicazioni e la ricezione di messaggi SMS. **Twilio Client** consente alle applicazioni comunicazioni vocali tooenable tramite connessioni Internet esistenti, incluse le connessioni per dispositivi mobili.

## <a id="Pricing"></a>Prezzi e offerte speciali di Twilio
Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio). Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata. toosign per questa offerta o ottenere ulteriori informazioni, visitare [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Concetti
API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni. Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).

Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbi Twilio
Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.

Hello seguito è riportato un elenco dei verbi di Twilio.

* **&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.
* **&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.
* **&lt;Hangup&gt;**: termina una chiamata.
* **&lt;Play&gt;**: riproduce un file audio.
* **&lt;Coda&gt;**: aggiungere hello tooa coda dei chiamanti.
* **&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.
* **&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.
* **&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.
* **&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si.
* **&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.
* **&lt;Sms&gt;**: invia un SMS.

### <a id="TwiML"></a>TwiML
TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.

Ad esempio, hello seguente TwiML conversione testo hello **Hello World!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello. A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni. È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.

Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml]. Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creare un account Twilio
Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio]. È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.

Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione. Entrambi saranno necessari toomake Twilio API chiamate. non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione. L'ID account e l'autenticazione token possono essere visualizzati in hello [Twilio Console][twilio_console]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.

## <a id="create_app"></a>Creare un'applicazione Java
1. Ottenere hello JAR Twilio e aggiungerlo tooyour percorso e l'assembly di distribuzione WAR di compilazione Java. In [https://github.com/twilio/twilio-java][twilio_java], è possibile scaricare origini GitHub hello e creare la propria JAR o scaricare un file JAR preesistente (con o senza dipendenze).
2. Verificare che il pacchetto JDK **cacerts** keystore contiene un certificato di autorità di certificazione sicura Equifax hello con 67:CB:9 impronta digitale MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numero di serie hello è 35:DE:F4:CF e hello SHA1 impronta digitale è D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Questo è certificato di autorità di certificazione certificato hello per hello [https://api.twilio.com] [ twilio_api_service] servizio, che viene chiamato quando si utilizza Twilio APIs. Per informazioni su come assicurare il JDK **cacerts** keystore contiene hello corretta autorità di certificazione, vedere [aggiunta di un archivio certificati Autorità di certificazione di Java di toohello certificato][add_ca_cert].

Istruzioni dettagliate per l'utilizzo della libreria client di hello Twilio per Java sono disponibili in [come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure][howto_phonecall_java].

## <a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione
All'interno del codice, è possibile aggiungere **importare** istruzioni nella parte superiore di hello dei file di origine per hello Twilio pacchetti o le classi si desidera toouse nell'applicazione.

Per i file di origine Java:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Per i file di origine JSP (Java Server Page):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
A seconda di quale Twilio pacchetti o le classi si desideri toouse, il **importare** istruzioni potrebbero essere diverse.

## <a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita
Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **chiamare** classe. Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML). Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.

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

Per ulteriori informazioni sui parametri hello passato toohello **Call.creator** metodo, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta. È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte in un'applicazione Java in Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS
Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello **messaggio** classe. Hello **da** numero, **4155992671**, viene fornito da Twilio per versione di valutazione account toosend messaggi SMS. Hello **a** numero deve essere verificato per il codice di hello Twilio account toorunning precedente.

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

Per ulteriori informazioni sui parametri hello passato toohello **Message.creator** metodo, vedere [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web
Quando l'applicazione avvia toohello una chiamata API di Twilio, ad esempio tramite hello **CallCreator.create** , Twilio verrà inviato l'URL tooa richiesta tooreturn prevista una risposta TwiML. esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url]. (Mentre TwiML deve essere utilizzato dai servizi Web, è possibile visualizzare hello TwiML nel browser. Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota  **&lt;risposta&gt;**  elemento; ad esempio, fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee un  **&lt;risposta&gt;**  elemento che contiene un  **&lt;pronuncia &gt;**  elemento.)

Anziché basarsi sul URL fornito Twilio hello, è possibile creare un URL sito che restituisce le risposte HTTP. È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte HTTP. In questo argomento si presuppone che si sarà hosting hello URL in una pagina JSP.

Hello seguente JSP pagina risultati in una risposta TwiML indicante **Hello World!** chiamata di hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

Hello seguente JSP pagina risultati in una risposta TwiML che indica un testo, che indica le informazioni sulla versione dell'API di Twilio hello e nome del ruolo Azure hello ha diverse pause.

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

Hello **ApiVersion** parametro è disponibile nelle richieste di Twilio vocale (non richieste SMS). parametri di richiesta disponibili hello toosee vocale Twilio e richieste SMS, vedere <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, rispettivamente. Hello **RoleName** variabile di ambiente è disponibile come parte di una distribuzione di Azure. (Se si desidera che le variabili di ambiente personalizzato tooadd pertanto potrebbe essere prelevati dal **System.getenv**, vedere la sezione di variabili di ambiente hello al [varie impostazioni di configurazione di ruolo] [misc_role_config_settings].)

Dopo aver creato la pagina JSP imposta tooprovide TwiML risposte, usare hello URL della pagina JSP hello come hello URL passato hello **Call.creator** metodo. Ad esempio, se si dispone di un'applicazione Web denominata tooan MyTwiML distribuiti servizio ospitato di Azure e hello pagina JSP hello è denominato mytwiml.jsp, hello URL può essere passato troppo**Call.creator** come illustrato nell'esempio hello:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

È un'altra opzione per la risposta con TwiML tramite hello **VoiceResponse** (classe), disponibile in hello **com.twilio.twiml** pacchetto.

Per ulteriori informazioni sull'utilizzo di Twilio in Azure con Java, vedere [come tooMake un Twilio tramite chiamata telefonica in un'applicazione Java in Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi
Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:

* [Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)
* [Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)
* [Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)
* [Twilio on GitHub][twilio_on_github] (Twilio su GitHub)
* [Comunicare tooTwilio supporto][twilio_support]

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
