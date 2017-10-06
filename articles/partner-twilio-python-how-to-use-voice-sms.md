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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Come tooUse Twilio per funzionalità voce ed SMS in Python
Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure. scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message). Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.

## <a id="WhatIs"></a>Informazioni su Twilio
Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica. Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello. Le applicazioni sono toobuild semplice e scalabile. Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.

**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.
**SMS Twilio** consente toosend l'applicazione e ricevere messaggi di testo.
**Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.

## <a id="Pricing"></a>Prezzi e offerte speciali di Twilio
I clienti di Azure ricevono un'[offerta speciale][special_offer]: $ 10 di credito Twilio quando si esegue l'aggiornamento dell'account Twilio. Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica). Riscattare il [credito Twilio][special_offer] e iniziare a usare il servizio.

Twilio è un servizio con pagamento in base al consumo. Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento. Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).

## <a id="Concepts"></a>Concetti
API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni. Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).

Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbi Twilio
Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.

Hello seguito è riportato un elenco dei verbi di Twilio. Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio][twiml].

* **&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.
* **&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.
* **&lt;Hangup&gt;**: termina una chiamata.
* **&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.
* **&lt;Play&gt;**: riproduce un file audio.
* **&lt;Coda&gt;**: aggiungere hello tooa coda dei chiamanti.
* **&lt;Record&gt;**: registra vocale hello del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.
* **&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.
* **&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si.
* **&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.
* **&lt;Sms&gt;**: invia un SMS.

### <a id="TwiML"></a>TwiML
TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.

Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello. A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni. È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse `TwiMLResponse` oggetto.

Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml]. Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creare un account Twilio
Quando si è pronti tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio]. È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.

Quando si effettua l'iscrizione a un account Twilio, si riceveranno il SID account e un token di autenticazione. Entrambi saranno necessari toomake Twilio API chiamate. non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione. Il SID dell'account e un token di autenticazione sono visibili in hello [Twilio Console][twilio_console]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.

## <a id="create_app"></a>Creare un'applicazione Python
Un'applicazione Python che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione Python che utilizza il servizio di Twilio hello. Mentre i servizi di Twilio basato su REST possono essere chiamati da Python in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria Twilio per Python da GitHub][twilio_python]. Per ulteriori informazioni sull'utilizzo della libreria di hello Twilio per Python, vedere [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Innanzitutto, [configurazione una nuova macchina virtuale Linux di Azure] [azure_vm_setup] tooact come host per la nuova applicazione web di Python. Una volta hello macchina virtuale è in esecuzione, sarà necessario tooexpose dell'applicazione su una porta pubblica come descritto di seguito.

### <a name="add-an-incoming-rule"></a>Aggiungere una regola in ingresso
  1. Passare toohello [Network Security Group] [azure_nsg] pagina.
  2. Selezionare hello Network Security Group corrispondente con la macchina virtuale.
  3. Aggiungere una **Regola in uscita** per la **porta 80**. Impossibile verificare tooallow in ingresso da qualsiasi indirizzo.

### <a name="set-hello-dns-name-label"></a>Impostare l'etichetta del nome DNS hello
  1. Passare toohello [hello indirizzi IP pubblici] [azure_ips] pagina.
  2. Selezionare hello IP pubblico che correspends con la macchina virtuale.
  3. Set hello **etichetta del nome DNS** in hello **configurazione** sezione. Nel caso di hello di questo esempio avrà un aspetto simile al seguente *l'etichetta di dominio*. centralus.cloudapp.azure.com

Quando si è in grado di tooconnect tramite SSH toohello macchina virtuale è possibile installare hello Framework Web di propria scelta (hello due più noti in fase di Python [pallone](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com)). È possibile installare una di esse semplicemente eseguendo hello `pip install` comando.

Tenere presente che è stato configurato il traffico tooallow hello macchine virtuali solo sulla porta 80. Verificare pertanto che tooconfigure hello applicazione toouse questa porta.

## <a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione
È possibile configurare la libreria di Twilio applicazione hello toouse per Python in due modi:

* Installare libreria Twilio hello per Python come pacchetto Pip. Può essere installato con hello seguenti comandi:
   
        $ pip install twilio

    -OPPURE-

* Scaricare una libreria di Twilio hello per Python da GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e installarlo simile al seguente:

        $ python setup.py install

Dopo aver installato libreria Twilio hello per Python, è quindi possibile `import` in file Python:

        import twilio

Per altre informazioni, vedere [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita
Hello seguente viene illustrato come chiamare toomake in uscita. Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML). Sostituire i valori per hello **from_number** e **to_number** i numeri di telefono e assicurarsi di aver verificato hello **from_number** numero di telefono per l'account di Twilio prima di eseguire il codice hello.

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

Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta. È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte da un sito Web di](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS
Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello `TwilioRestClient` classe. Hello **from_number** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS. Hello **to_number** numero deve essere verificato per l'account di Twilio prima di eseguire codice hello.

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

## <a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web
Quando l'applicazione avvia toohello una chiamata API di Twilio, Twilio invierà l'URL tooa richiesta è previsto tooreturn una risposta TwiML. esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url]. Poiché TwiML è stato progettato per essere usato da Twilio, è possibile visualizzarlo nel browser. Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota `<Response>` elemento; ad esempio, fare clic su [http://twimlets.com/message? Messaggio % 5B0 %5D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` elemento che contiene un `<Say>` elemento.)

Anziché basarsi sul URL fornito Twilio hello, è possibile creare un sito che restituisce le risposte HTTP. È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte XML. In questo argomento si presuppone che si userà hello toocreate Python TwiML.

Hello negli esempi seguenti genera una risposta TwiML che afferma **Hello World** chiamata hello.

Con Flask:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Con Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML. libreria di Twilio Hello per Python contiene classi che generano TwiML automaticamente. Hello esempio riportato di seguito genera risposta equivalente hello, come illustrato in precedenza, ma utilizza hello `twiml` modulo nella libreria di Twilio hello per Python:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference].

Dopo aver creato l'applicazione Python imposta risposte TwiML tooprovide, utilizzare l'URL di hello di un'applicazione hello come hello URL passato hello `client.calls.create` metodo. Ad esempio, se si dispone di un'applicazione Web denominata **MyTwiML** tooan distribuito Azure servizio ospitato, è possibile usare il relativo url come webhook, come illustrato nell'esempio seguente hello:

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

## <a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi
Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api].

## <a id="NextSteps"></a>Passaggi successivi
Ora che si è appreso nozioni di base di hello di hello servizio Twilio, seguire questi toolearn collegamenti più:

* [Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)
* [Twilio HowTo Guides and Example Code][twilio_howtos] (Procedure e codice di esempio su Twilio)
* [Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)
* [Twilio on GitHub][twilio_on_github] (Twilio su GitHub)
* [Comunicare tooTwilio supporto][twilio_support]

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
