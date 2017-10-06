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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Come tooUse Twilio per funzionalità voce ed SMS in Ruby
Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure. scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message). Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.

## <a id="WhatIs"></a>Informazioni su Twilio
Twilio è un'API web-servizio di telefonia che consente di utilizzare i linguaggi web esistenti e vocale toobuild competenze e le applicazioni di SMS. Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.

**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche. **SMS Twilio** consente toomake le applicazioni e la ricezione di messaggi SMS. **Twilio Client** consente alle applicazioni comunicazioni vocali tooenable tramite connessioni Internet esistenti, incluse le connessioni per dispositivi mobili.

## <a id="Pricing"></a>Prezzi e offerte speciali di Twilio
Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio). Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata. toosign per questa offerta o ottenere ulteriori informazioni, visitare [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Concetti
API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni. Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).

### <a id="TwiML"></a>TwiML
TwiML è un set di istruzioni basato su XML che informano Twilio come tooprocess una telefonata o SMS.

Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Tutti i documenti TwiML dispongono di un elemento radice `<Response>`, Da qui, utilizzare il comportamento di hello toodefine Twilio verbi dell'applicazione.

### <a id="Verbs"></a>Verbi TwiML
I verbi di Twilio sono tag XML in cui indicare Twilio troppo**si**. Ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata. 

Hello seguito è riportato un elenco dei verbi di Twilio.

* **&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.
* **&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.
* **&lt;Hangup&gt;**: termina una chiamata.
* **&lt;Play&gt;**: riproduce un file audio.
* **&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.
* **&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.
* **&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.
* **&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si
* **&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.
* **&lt;Sms&gt;**: invia un SMS.

Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml]. Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creare un account Twilio
Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio]. È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.

Quando si effettua l'iscrizione a Twilio si riceve un numero di telefono gratuito per l'applicazione. Si ricevono inoltre il SID dell'account e un token di autorizzazione. Entrambi saranno necessari toomake Twilio API chiamate. non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione. Il SID dell'account e un token di autorizzazione possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello campi con etichettati **SID di ACCOUNT** e **Authentication TOKEN** , rispettivamente.

### <a id="VerifyPhoneNumbers"></a>Verificare i numeri di telefono
Numero di toohello aggiunta che viene fornita da Twilio, è inoltre possibile verificare i numeri di controllo (ad esempio il telefono cellulare o home numero di telefono) per l'utilizzo nelle applicazioni. 

Per informazioni su come tooverify un numero di telefono, vedere [gestire numeri][verify_phone].

## <a id="create_app"></a>Creare un'applicazione Ruby
Un'applicazione Ruby che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione che utilizza il servizio di Twilio hello Ruby. Mentre Twilio servizi RESTful possono essere chiamati da Ruby in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria helper Twilio per Ruby][twilio_ruby].

Prima di tutto, [configurazione una nuova macchina virtuale Linux di Azure] [ azure_vm_setup] tooact come host per la nuova applicazione web Ruby. Ignorare i passaggi di hello che implicano hello creazione di un'app, guide appena hello di configurazione macchina virtuale. Assicurarsi di creare un endpoint con porta esterna 80 e porta interna 5000.

Negli esempi di hello riportato di seguito, che verrà usato [Sinatra][sinatra], un framework web molto semplice per Ruby. Ma è possibile utilizzare libreria helper di Twilio hello per Ruby con qualsiasi altro framework web, come Ruby on Guide.

Connettersi tramite SSH alla nuova macchina virtuale e creare una directory per la nuova app. All'interno di tale directory, creare un file denominato Gemfile e copia hello seguente codice al suo interno:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Nella riga di comando hello eseguire `bundle install`. Dipendenze di hello precedente verrà installato. Quindi, creare un file denominato `web.rb`. Si tratterà in cui si trova il codice hello per le app web. Incollare hello seguente codice al suo interno:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

A questo punto dovrebbe essere comando hello hello in grado di eseguire `ruby web.rb -p 5000`. Verrà avviato un server Web di dimensioni ridotte sulla porta 5000. Dovrebbe essere in grado di toobrowse toothis app nel browser, visitare l'URL di hello configurazione per la macchina virtuale di Azure. Una volta che è possibile raggiungere l'app web nel browser hello, si è pronti toostart creazione di un'app di Twilio.

## <a id="configure_app"></a>Configurare l'applicazione tooUse Twilio
È possibile configurare la libreria di Twilio web app toouse hello aggiornando il `Gemfile` tooinclude questa riga:

    gem 'twilio-ruby'

Nella riga di comando hello, eseguire `bundle install`. Aprire quindi `web.rb` e tra la riga nella parte superiore di hello:

    require 'twilio-ruby'

Si è ora tutti i set di libreria di supporto toouse hello Twilio per Ruby in app web.

## <a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita
Hello seguente viene illustrato come chiamare toomake in uscita. Concetti principali includono l'utilizzo di libreria di supporto di hello Twilio per Ruby toomake chiamate API REST e TwiML di rendering. Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.

Aggiungere la seguente funzione troppo`web.md`:

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

Se remoto aprire `http://yourdomain.cloudapp.net/make_call` in un browser, che attiverà hello chiamata toohello Twilio API toomake hello telefonata. Hello i primi due parametri in `client.account.calls.create` sono di chiara interpretazione: hello numero hello chiamata `from` ed è chiamata hello numero hello `to`. 

terzo parametro Hello (`url`) è l'URL di hello che Twilio istruzioni tooget su quali toodo le richieste una volta chiamata hello è connesso. In questo caso è senza un URL (`http://yourdomain.cloudapp.net`) che restituisce un documento TwiML semplice e Usa hello `<Say>` toodo verbo alcune sintesi vocale e ad esempio "Hello Monkey" toohello destinatario hello chiamare.

## <a id="howto_recieve_sms"></a>Procedura: Ricevere un messaggio SMS
Nell'esempio precedente hello è stato avviato un **in uscita** telefonata. Questa volta, consente di usare il numero di telefono hello Twilio ha restituito durante l'iscrizione tooprocess un **in ingresso** messaggio SMS.

In primo luogo, accesso tooyour [dashboard Twilio][twilio_account]. Fare clic su "Numeri" nella barra di spostamento superiore di hello e quindi fare clic su hello numero Twilio che sono state fornite. Verranno visualizzati due URL che è possibile configurare, uno per le richieste vocali e uno per le richieste SMS. Si tratta di URL hello effettuate chiamate Twilio ogni volta che una chiamata telefonica o un SMS inviato tooyour numero. Hello URL sono noti anche come "web hook".

Desideriamo tooprocess messaggi in arrivo di SMS, questo punto aggiornare hello URL troppo`http://yourdomain.cloudapp.net/sms_url`. Procedere facendo clic su Salva modifiche nella parte inferiore di hello della pagina hello. Tornare `web.rb` toohandle l'applicazione si programma in questo:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Dopo aver apportato modifiche hello, assicurarsi che toore-inizio l'app web. A questo punto, estrarre il telefono e inviare un numero di Twilio di tooyour SMS. È necessario ottenere immediatamente una risposta SMS che afferma "Hey, grazie per il ping di hello! Twilio and Azure rock!".

## <a id="additional_services"></a>Procedura: Utilizzare servizi Twilio aggiuntivi
Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].

### <a id="NextSteps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:

* [Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)
* [Twilio HowTos and Example Code (Procedure e codice di esempio di Twilio)][twilio_howtos]
* [Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio) 
* [Twilio on GitHub][twilio_on_github] (Twilio su GitHub)
* [Comunicare tooTwilio supporto][twilio_support]

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
