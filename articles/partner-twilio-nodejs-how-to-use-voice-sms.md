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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="ef330-104">Uso di Twilio per le funzionalità voce, VoIP e SMS in Azure</span><span class="sxs-lookup"><span data-stu-id="ef330-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="ef330-105">Questa guida illustra come App toobuild che comunicano con Twilio e node.js in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef330-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="ef330-106">Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="ef330-106">What is Twilio?</span></span>
<span data-ttu-id="ef330-107">Twilio è una piattaforma di API che consente agli sviluppatori toomake facilmente e ricezione chiamate telefoniche, inviare e ricevere messaggi di testo e incorporare chiamate VoIP nelle applicazioni per dispositivi mobili basati su browser e native.</span><span class="sxs-lookup"><span data-stu-id="ef330-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="ef330-108">Prima di entrare nel dettaglio, verrà illustrato brevemente il funzionamento della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="ef330-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="ef330-109">Ricevere chiamate e SMS</span><span class="sxs-lookup"><span data-stu-id="ef330-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="ef330-110">Twilio consente agli sviluppatori troppo[acquistare i numeri di telefono programmabile] [ purchase_phone] che può essere utilizzato tooboth di inviare e ricevere le chiamate e messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="ef330-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="ef330-111">Quando un numero di Twilio riceve una chiamata in ingresso o testo, Twilio invierà all'applicazione web un HTTP POST o GET, in cui viene richiesto per istruzioni su come toohandle hello chiamata o testo.</span><span class="sxs-lookup"><span data-stu-id="ef330-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="ef330-112">Il server risponderà richiesta HTTP del tooTwilio con [TwiML][twiml], una semplice serie di tag XML che contengono istruzioni su come toohandle una telefonata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="ef330-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="ef330-113">Più avanti verranno illustrati esempi del linguaggio TwiML.</span><span class="sxs-lookup"><span data-stu-id="ef330-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="ef330-114">Effettuare chiamate e inviare SMS</span><span class="sxs-lookup"><span data-stu-id="ef330-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="ef330-115">Apportando toohello le richieste HTTP Twilio API del servizio web, gli sviluppatori possono inviare messaggi di testo o avviare le chiamate in uscita.</span><span class="sxs-lookup"><span data-stu-id="ef330-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="ef330-116">Per le chiamate in uscita, sviluppatore hello deve inoltre specificare un URL che restituisce le istruzioni TwiML per come toohandle hello in uscita chiama quando è connesso.</span><span class="sxs-lookup"><span data-stu-id="ef330-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="ef330-117">Incorporare funzionalità VoIP nel codice dell'interfaccia utente (JavaScript, iOS o Android)</span><span class="sxs-lookup"><span data-stu-id="ef330-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="ef330-118">Twilio offre un SDK lato client che consente di trasformare qualsiasi Web browser desktop, app per iOS o app per Android in un telefono VoIP.</span><span class="sxs-lookup"><span data-stu-id="ef330-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="ef330-119">In questo articolo esamineremo come toouse VoIP chiamata nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="ef330-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="ef330-120">In aggiunta toohello *Twilio JavaScript SDK* in esecuzione nel browser hello, un'applicazione sul lato server (l'applicazione di Node. js) deve essere utilizzato tooissue toohello un "token funzionalità" client JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ef330-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="ef330-121">È possibile leggere altre informazioni sull'utilizzo VoIP con node.js [sul blog di sviluppo Twilio hello][voipnode].</span><span class="sxs-lookup"><span data-stu-id="ef330-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="ef330-122">Iscriversi a Twilio (sconto Microsoft)</span><span class="sxs-lookup"><span data-stu-id="ef330-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="ef330-123">Prima di usare i servizi Twilio, è necessario [iscriversi per creare un account][signup].</span><span class="sxs-lookup"><span data-stu-id="ef330-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="ef330-124">I clienti di Microsoft Azure ricevono uno sconto speciale - [essere toosign verificare qui][signup]!</span><span class="sxs-lookup"><span data-stu-id="ef330-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="ef330-125">Creare e distribuire un sito Web Node.js in Azure</span><span class="sxs-lookup"><span data-stu-id="ef330-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="ef330-126">Successivamente, sarà necessario toocreate un sito Web node.js in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef330-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="ef330-127">[documentazione ufficiale di Hello per eseguire questa operazione è disponibile in][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="ef330-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="ef330-128">A un livello elevato, è necessario effettuare i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="ef330-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="ef330-129">Creazione di un account Azure, se non già disponibile</span><span class="sxs-lookup"><span data-stu-id="ef330-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="ef330-130">Utilizzo di hello Azure admin console toocreate un nuovo sito Web</span><span class="sxs-lookup"><span data-stu-id="ef330-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="ef330-131">Aggiunta del supporto per il controllo del codice sorgente (si presuppone che sia stato usato git)</span><span class="sxs-lookup"><span data-stu-id="ef330-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="ef330-132">Creazione di un file `server.js` con una semplice applicazione Web Node.js</span><span class="sxs-lookup"><span data-stu-id="ef330-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="ef330-133">Distribuzione tooAzure questa semplice applicazione</span><span class="sxs-lookup"><span data-stu-id="ef330-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="ef330-134">Configurare hello modulo Twilio</span><span class="sxs-lookup"><span data-stu-id="ef330-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="ef330-135">Successivamente, verrà avviato toowrite utilizzato da un'applicazione node.js semplice che consente di hello Twilio API.</span><span class="sxs-lookup"><span data-stu-id="ef330-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="ef330-136">Prima di procedere, dobbiamo tooconfigure i nostri le credenziali dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="ef330-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="ef330-137">Configurare le credenziali Twilio in variabili di ambiente di sistema</span><span class="sxs-lookup"><span data-stu-id="ef330-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="ef330-138">Nelle richieste di ordine toomake autenticato sul back-end di hello Twilio, è necessario il SID dell'account e un token di autenticazione, la funzione hello username e password per l'account di Twilio.</span><span class="sxs-lookup"><span data-stu-id="ef330-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="ef330-139">Questi valori da usare con il modulo nodo hello in Azure tooconfigure modo più sicuro Hello è tramite variabili di ambiente di sistema, che è possibile impostare direttamente nella console di amministrazione di Azure di hello.</span><span class="sxs-lookup"><span data-stu-id="ef330-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="ef330-140">Selezionare il sito Web node.js e fare clic sul collegamento "Configura" hello.</span><span class="sxs-lookup"><span data-stu-id="ef330-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="ef330-141">Scorrendo verso il basso verrà visualizzata un'area in cui è possibile impostare le proprietà di configurazione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ef330-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="ef330-142">Immettere le credenziali dell'account Twilio ([trovato per la Console di Twilio][twilio_console]) come illustrato - rendere tooname che li `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`, rispettivamente:</span><span class="sxs-lookup"><span data-stu-id="ef330-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Console di amministrazione di Azure][azure-admin-console]

<span data-ttu-id="ef330-144">Dopo aver configurato queste variabili, riavviare l'applicazione hello console Azure.</span><span class="sxs-lookup"><span data-stu-id="ef330-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="ef330-145">Dichiarazione di modulo di Twilio hello in package. JSON</span><span class="sxs-lookup"><span data-stu-id="ef330-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="ef330-146">È quindi necessario toocreate toomanage un package. JSON le dipendenze del modulo il nodo tramite [npm].</span><span class="sxs-lookup"><span data-stu-id="ef330-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="ef330-147">Hello stesso livello come hello `server.js` file creato nella hello *Azure/node.js* esercitazione, creare un file denominato `package.json`.</span><span class="sxs-lookup"><span data-stu-id="ef330-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="ef330-148">All'interno del file, inserire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ef330-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="ef330-149">Modulo di twilio hello viene dichiarata come una dipendenza, nonché hello diffusi [Express framework web] [ express] e motore del modello di hello EJS.</span><span class="sxs-lookup"><span data-stu-id="ef330-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="ef330-150">A questo punto, è possibile iniziare a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="ef330-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="ef330-151">Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="ef330-151">Make an Outbound Call</span></span>
<span data-ttu-id="ef330-152">Creare un form semplice in cui verrà inserito un numero di chiamate tooa che scelti.</span><span class="sxs-lookup"><span data-stu-id="ef330-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="ef330-153">Aprire la console di `server.js`, quindi immettere hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="ef330-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="ef330-154">Si noti in cui è visualizzato "CHANGE_ME" - inseriti nome hello del sito Web di azure:</span><span class="sxs-lookup"><span data-stu-id="ef330-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

<span data-ttu-id="ef330-155">Successivamente, creare una directory denominata `views` : in questa directory, creare un file denominato `index.ejs` con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="ef330-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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

<span data-ttu-id="ef330-156">A questo punto, distribuire tooAzure il sito Web e aprire la home page.</span><span class="sxs-lookup"><span data-stu-id="ef330-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="ef330-157">Si deve essere in grado di tooenter il numero di telefono nel campo di testo hello e ricevere una chiamata dal numero di Twilio!</span><span class="sxs-lookup"><span data-stu-id="ef330-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="ef330-158">Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="ef330-158">Send an SMS Message</span></span>
<span data-ttu-id="ef330-159">A questo punto, verrà configurata un'interfaccia utente e il modulo Gestione logica toosend un messaggio di testo.</span><span class="sxs-lookup"><span data-stu-id="ef330-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="ef330-160">Aprire la console di `server.js`e aggiungere hello seguente codice dopo l'ultima chiamata hello troppo`app.post`:</span><span class="sxs-lookup"><span data-stu-id="ef330-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

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

<span data-ttu-id="ef330-161">In `views/index.ejs`, aggiungere un altro modulo in un primo toosubmit hello un numero e un messaggio di testo:</span><span class="sxs-lookup"><span data-stu-id="ef330-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="ef330-162">Distribuire nuovamente l'applicazione tooAzure e dovrebbe essere in grado di toosubmit che costituiscono e inviare un messaggio di testo di se stessi (o uno dei tuoi amici più vicini)!</span><span class="sxs-lookup"><span data-stu-id="ef330-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="ef330-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef330-163">Next Steps</span></span>
<span data-ttu-id="ef330-164">Si sono appena appreso hello utilizzo base node.js e Twilio toobuild app di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="ef330-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="ef330-165">Ma in questi esempi scratch poco area hello di ciò che è possibile con Twilio e node.js.</span><span class="sxs-lookup"><span data-stu-id="ef330-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="ef330-166">Per ulteriori informazioni sull'utilizzo di Twilio con node.js, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="ef330-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="ef330-167">[Documentazione ufficiale del modulo][docs]</span><span class="sxs-lookup"><span data-stu-id="ef330-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="ef330-168">[Tutorial on VoIP with node.js applications][voipnode] (Esercitazione sull'uso di VoIP con le applicazioni node.js)</span><span class="sxs-lookup"><span data-stu-id="ef330-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="ef330-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr] (Votr: un'applicazione di voto via SMS in tempo reale con node.js e CouchDB (tre parti))</span><span class="sxs-lookup"><span data-stu-id="ef330-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="ef330-170">[Programmazione di coppia nel browser hello con node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="ef330-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="ef330-171">A questo punto, non resta che sperimentare tutte le possibilità offerte dall'uso di Node.js e Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef330-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

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
