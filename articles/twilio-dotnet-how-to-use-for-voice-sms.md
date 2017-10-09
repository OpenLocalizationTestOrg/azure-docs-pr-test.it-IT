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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Come toouse Twilio per funzionalità voce ed SMS da Azure
Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure. scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message). Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.

## <a id="WhatIs"></a>Informazioni su Twilio
Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica. Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello. Le applicazioni sono toobuild semplice e scalabile. Offre flessibilità, grazie a un modello di prezzi con pagamento in base al consumo, e l'affidabilità del cloud.

**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche. **SMS Twilio** consente toosend le applicazioni e la ricezione di messaggi SMS. **Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.

## <a id="Pricing"></a>Prezzi e offerte speciali di Twilio
I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio. Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica). Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina all'indirizzo [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio è un servizio con pagamento in base al consumo. Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento. Per altre informazioni, vedere la pagina relativa ai [prezzi di Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Concetti
API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni. Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).

Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbi Twilio
Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.

Hello seguito è riportato un elenco dei verbi di Twilio.  Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.
* **&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.
* **&lt;Hangup&gt;**: termina una chiamata.
* **&lt;Play&gt;**: riproduce un file audio.
* **&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.
* **&lt;Record&gt;**: registra una voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.
* **&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.
* **&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si
* **&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.
* **&lt;Sms&gt;**: invia un SMS.

### <a id="TwiML"></a>TwiML
TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.

Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello. A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni. È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.

Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml]. Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creare un account Twilio
Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio]. È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.

Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione. Entrambi saranno necessari toomake Twilio API chiamate. non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione. L'ID account e l'autenticazione token possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.

## <a id="create_app"></a>Creare un'applicazione Azure
Un'applicazione Azure che ospita un'applicazione compatibile con Twilio non è diversa da qualsiasi altra applicazione Azure. Aggiungi libreria .NET di Twilio hello e configurare le librerie .NET di Twilio di hello ruolo toouse hello.
Per informazioni sulla creazione di un progetto Azure iniziale, vedere [Creazione di un progetto Azure con Visual Studio][vs_project].

## <a id="configure_app"></a>Configurare le librerie di Twilio toouse dell'applicazione
Twilio fornisce un set di librerie di supporto .NET che eseguono il wrapping di vari aspetti di Twilio tooprovide modi molto semplice toointeract con hello API REST di Twilio e dei Twilio Client toogenerate TwiML risposte.

Twilio offre cinque librerie per sviluppatori .NET:
Libreria|Descrizione
---|---
Twilio.API|Hello libreria principale di Twilio che esegue il wrapping di API REST di Twilio hello in una libreria .NET descrittiva. Questa libreria è disponibile per .NET, Silverlight e Windows Phone 7.
Twilio.TwiML|Fornisce un codice di TwiML toogenerate modo descrittivo .NET.
Twilio.MVC|Per gli sviluppatori che usano ASP.NET MVC, questa libreria include un controller TwilioController, una classe ActionResult TwiML e un attributo di convalida della richiesta.
Twilio.WebMatrix|Per gli sviluppatori che utilizzano lo strumento di sviluppo WebMatrix gratuito di Microsoft, questa libreria contiene gli helper della sintassi Razor per varie azioni Twilio.
Twilio.Client.Capability|Contiene generatore token hello di funzionalità per l'utilizzo con hello Twilio Client JavaScript SDK.

Si noti che tutte le librerie richiedono .NET 3.5, Silverlight 4 o Windows Phone 7 o versioni successive.

esempi di Hello forniti in questa Guida utilizzano libreria Twilio.API hello.

possono essere librerie Hello [installato utilizzando l'estensione Gestione pacchetti NuGet di hello](http://www.twilio.com/docs/csharp/install) disponibile per Visual Studio 2010 up too2015.  Hello codice sorgente è ospitato in [GitHub][twilio_github_repo], che include una pagina Wiki che contiene la documentazione completa per l'utilizzo di librerie hello.

Per impostazione predefinita, con Microsoft Visual Studio 2010 viene installata la versione 1.2 di NuGet. Installazione di librerie di Twilio hello richiede la versione 1.6 di NuGet. Per informazioni sull'installazione o l'aggiornamento di NuGet, vedere [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall hello più recente di NuGet, è necessario innanzitutto disinstallare hello versione caricata utilizzando hello Gestione estensioni di Visual Studio. toodo in tal caso, è necessario eseguire Visual Studio come amministratore. In caso contrario, il pulsante di disinstallazione hello è disabilitato.
>
>

### <a id="use_nuget"></a>tooadd hello Twilio librerie tooyour progetto di Visual Studio:
1. Aprire la soluzione in Visual Studio.
2. Fare clic con il pulsante destro del mouse su **Riferimenti**.
3. Scegliere **Gestisci pacchetti NuGet...**
4. Fare clic su **Online**.
5. Nella casella di ricerca hello online, digitare *twilio*.
6. Fare clic su **installare** pacchetto Twilio hello.

## <a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita
Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **CallResource** classe. Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML). Sostituire i valori per hello **a** e **da** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per l'account di Twilio prima di eseguire codice hello.

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

Per ulteriori informazioni sui parametri hello passato toohello **CallResource.Create** metodo, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta. È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per altre informazioni, vedere [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses) (Procedura: Fornire risposte TwiML dal proprio sito Web).

## <a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS
Hello schermata riportata di seguito viene illustrato come un messaggio SMS utilizzando toosend hello **MessageResource** classe. Hello **da** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS. Hello **a** numero deve essere verificato per l'account di Twilio prima di eseguire codice hello.

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

## <a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web
Quando l'applicazione avvia toohello una chiamata API di Twilio, ad esempio, tramite hello **CallResource.Create** metodo - Twilio invia l'URL tooan richiesta tooreturn prevista una risposta TwiML. esempio Hello in [procedura: effettuare una chiamata in uscita](#howto_make_call) utilizza hello URL fornito Twilio [http://twimlets.com/message] [ twimlet_message_url] risposta hello tooreturn.

> [!NOTE]
> Mentre TwiML deve essere utilizzato dai servizi web, è possibile visualizzare hello TwiML nel browser. Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota &lt;risposta&gt; elemento; ad esempio, fare clic su [http://twimlets.com/message ? Messaggio % 5B0 %5D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee un &lt;risposta&gt; elemento che contiene un &lt;pronuncia&gt; elemento.
>
>

Anziché basarsi sul URL fornito Twilio hello, è possibile creare un URL sito che restituisce le risposte HTTP. È possibile creare il sito hello in qualsiasi linguaggio che restituisce le risposte HTTP. Si presuppone che si sarà hosting hello URL da un gestore generico di ASP.NET.

Hello seguente gestore ASP.NET presenta una risposta TwiML che afferma **Hello World** chiamata hello.

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
    
Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML. libreria Twilio.TwiML Hello contiene le classi che generano TwiML automaticamente. Hello esempio riportato di seguito genera risposta equivalente hello, come illustrato in precedenza, ma utilizza hello **VoiceResponse** classe.

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

Per ulteriori informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Dopo aver impostato le risposte di TwiML tooprovide un modo, è possibile passare tale toohello URL **CallResource.Create** metodo. Ad esempio, se si dispone di un'applicazione web denominata tooan MyTwiML distribuiti servizio cloud di Azure e il nome di hello del gestore di ASP.NET è mytwiml.ashx, hello URL può essere passato troppo**CallResource.Create** come illustrato nel seguente codice hello esempio:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Per ulteriori informazioni sull'utilizzo di Twilio in Azure con ASP.NET, vedere [come toomake un telefono chiamata tramite Twilio in un ruolo web in Azure][howto_phonecall_dotnet].

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
