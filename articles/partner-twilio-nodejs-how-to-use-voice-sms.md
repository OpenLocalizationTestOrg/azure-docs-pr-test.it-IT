---
title: aaaUsing Twilio per vocali, VoIP e la messaggistica SMS in Azure
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Gli esempi di codice sono scritti in Node.js.
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Uso di Twilio per le funzionalità voce, VoIP e SMS in Azure
Questa guida illustra come App toobuild che comunicano con Twilio e node.js in Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Informazioni su Twilio
Twilio è una piattaforma di API che consente agli sviluppatori toomake facilmente e ricezione chiamate telefoniche, inviare e ricevere messaggi di testo e incorporare chiamate VoIP nelle applicazioni per dispositivi mobili basati su browser e native. Prima di entrare nel dettaglio, verrà illustrato brevemente il funzionamento della piattaforma.

### <a name="receiving-calls-and-text-messages"></a>Ricevere chiamate e SMS
Twilio consente agli sviluppatori troppo[acquistare i numeri di telefono programmabile] [ purchase_phone] che può essere utilizzato tooboth di inviare e ricevere le chiamate e messaggi di testo. Quando un numero di Twilio riceve una chiamata in ingresso o testo, Twilio invierà all'applicazione web un HTTP POST o GET, in cui viene richiesto per istruzioni su come toohandle hello chiamata o testo. Il server risponderà richiesta HTTP del tooTwilio con [TwiML][twiml], una semplice serie di tag XML che contengono istruzioni su come toohandle una telefonata o un SMS. Più avanti verranno illustrati esempi del linguaggio TwiML.

### <a name="making-calls-and-sending-text-messages"></a>Effettuare chiamate e inviare SMS
Apportando toohello le richieste HTTP Twilio API del servizio web, gli sviluppatori possono inviare messaggi di testo o avviare le chiamate in uscita. Per le chiamate in uscita, sviluppatore hello deve inoltre specificare un URL che restituisce le istruzioni TwiML per come toohandle hello in uscita chiama quando è connesso.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Incorporare funzionalità VoIP nel codice dell'interfaccia utente (JavaScript, iOS o Android)
Twilio offre un SDK lato client che consente di trasformare qualsiasi Web browser desktop, app per iOS o app per Android in un telefono VoIP. In questo articolo esamineremo come toouse VoIP chiamata nel browser hello. In aggiunta toohello *Twilio JavaScript SDK* in esecuzione nel browser hello, un'applicazione sul lato server (l'applicazione di Node. js) deve essere utilizzato tooissue toohello un "token funzionalità" client JavaScript. È possibile leggere altre informazioni sull'utilizzo VoIP con node.js [sul blog di sviluppo Twilio hello][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Iscriversi a Twilio (sconto Microsoft)
Prima di usare i servizi Twilio, è necessario [iscriversi per creare un account][signup]. I clienti di Microsoft Azure ricevono uno sconto speciale - [essere toosign verificare qui][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Creare e distribuire un sito Web Node.js in Azure
Successivamente, sarà necessario toocreate un sito Web node.js in esecuzione in Azure. [documentazione ufficiale di Hello per eseguire questa operazione è disponibile in][azure_new_site]. A un livello elevato, è necessario effettuare i seguenti hello:

* Creazione di un account Azure, se non già disponibile
* Utilizzo di hello Azure admin console toocreate un nuovo sito Web
* Aggiunta del supporto per il controllo del codice sorgente (si presuppone che sia stato usato git)
* Creazione di un file `server.js` con una semplice applicazione Web Node.js
* Distribuzione tooAzure questa semplice applicazione

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Configurare hello modulo Twilio
Successivamente, verrà avviato toowrite utilizzato da un'applicazione node.js semplice che consente di hello Twilio API. Prima di procedere, dobbiamo tooconfigure i nostri le credenziali dell'account Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Configurare le credenziali Twilio in variabili di ambiente di sistema
Nelle richieste di ordine toomake autenticato sul back-end di hello Twilio, è necessario il SID dell'account e un token di autenticazione, la funzione hello username e password per l'account di Twilio. Questi valori da usare con il modulo nodo hello in Azure tooconfigure modo più sicuro Hello è tramite variabili di ambiente di sistema, che è possibile impostare direttamente nella console di amministrazione di Azure di hello.

Selezionare il sito Web node.js e fare clic sul collegamento "Configura" hello.  Scorrendo verso il basso verrà visualizzata un'area in cui è possibile impostare le proprietà di configurazione per l'applicazione.  Immettere le credenziali dell'account Twilio ([trovato per la Console di Twilio][twilio_console]) come illustrato - rendere tooname che li `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`, rispettivamente:

![Console di amministrazione di Azure][azure-admin-console]

Dopo aver configurato queste variabili, riavviare l'applicazione hello console Azure.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Dichiarazione di modulo di Twilio hello in package. JSON
È quindi necessario toocreate toomanage un package. JSON le dipendenze del modulo il nodo tramite [npm]. Hello stesso livello come hello `server.js` file creato nella hello *Azure/node.js* esercitazione, creare un file denominato `package.json`.  All'interno del file, inserire il seguente hello:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

Modulo di twilio hello viene dichiarata come una dipendenza, nonché hello diffusi [Express framework web] [ express] e motore del modello di hello EJS.  A questo punto, è possibile iniziare a scrivere il codice.

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Effettuare una chiamata in uscita
Creare un form semplice in cui verrà inserito un numero di chiamate tooa che scelti. Aprire la console di `server.js`, quindi immettere hello seguente codice. Si noti in cui è visualizzato "CHANGE_ME" - inseriti nome hello del sito Web di azure:

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

Successivamente, creare una directory denominata `views` : in questa directory, creare un file denominato `index.ejs` con hello seguente contenuto:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

A questo punto, distribuire tooAzure il sito Web e aprire la home page. Si deve essere in grado di tooenter il numero di telefono nel campo di testo hello e ricevere una chiamata dal numero di Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Inviare un messaggio SMS
A questo punto, verrà configurata un'interfaccia utente e il modulo Gestione logica toosend un messaggio di testo. Aprire la console di `server.js`e aggiungere hello seguente codice dopo l'ultima chiamata hello troppo`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

In `views/index.ejs`, aggiungere un altro modulo in un primo toosubmit hello un numero e un messaggio di testo:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Distribuire nuovamente l'applicazione tooAzure e dovrebbe essere in grado di toosubmit che costituiscono e inviare un messaggio di testo di se stessi (o uno dei tuoi amici più vicini)!

<a id="nextsteps"/>

## <a name="next-steps"></a>Passaggi successivi
Si sono appena appreso hello utilizzo base node.js e Twilio toobuild app di comunicazione. Ma in questi esempi scratch poco area hello di ciò che è possibile con Twilio e node.js. Per ulteriori informazioni sull'utilizzo di Twilio con node.js, vedere hello seguenti risorse:

* [Documentazione ufficiale del modulo][docs]
* [Tutorial on VoIP with node.js applications][voipnode] (Esercitazione sull'uso di VoIP con le applicazioni node.js)
* [Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr] (Votr: un'applicazione di voto via SMS in tempo reale con node.js e CouchDB (tre parti))
* [Programmazione di coppia nel browser hello con node.js][pair]

A questo punto, non resta che sperimentare tutte le possibilità offerte dall'uso di Node.js e Twilio in Azure.

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
