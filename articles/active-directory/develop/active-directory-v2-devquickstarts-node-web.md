---
title: Accesso all'app Web Node.js con Azure Active Directory 2.0 | Microsoft Docs
description: Informazioni su come creare un'app Web Node.js che consente agli utenti di accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="a8459-103">Aggiungere l'accesso a un'app Web Node.js</span><span class="sxs-lookup"><span data-stu-id="a8459-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="a8459-104">Non tutti gli scenari e le funzionalità di Azure Active Directory usano l'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="a8459-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="a8459-105">Per determinare se è necessario usare l'endpoint v2.0 o l'endpoint v1.0, leggere le informazioni sulle [limitazioni della versione 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a8459-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="a8459-106">In questa esercitazione si userà Passport per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8459-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="a8459-107">In un'app Web, consentire l'accesso dell'utente con Azure Active Directory (Azure AD) e l'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="a8459-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="a8459-108">Visualizzare informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-108">Display information about the user.</span></span>
* <span data-ttu-id="a8459-109">Disconnettere l'utente dall'app.</span><span class="sxs-lookup"><span data-stu-id="a8459-109">Sign the user out of the app.</span></span>

<span data-ttu-id="a8459-110">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="a8459-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="a8459-111">Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="a8459-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="a8459-112">In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="a8459-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="a8459-113">È stata sviluppata una strategia per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8459-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="a8459-114">Questo articolo illustra come installare il modulo e quindi aggiungere il plug-in `passport-azure-ad` di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8459-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="a8459-115">Scaricare</span><span class="sxs-lookup"><span data-stu-id="a8459-115">Download</span></span>
<span data-ttu-id="a8459-116">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="a8459-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="a8459-117">Per seguire l'esercitazione, è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="a8459-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="a8459-118">Al termine dell'esercitazione, è anche possibile ottenere l'applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="a8459-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="a8459-119">1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="a8459-119">1: Register an app</span></span>
<span data-ttu-id="a8459-120">Per registrare un'app creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a8459-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="a8459-121">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="a8459-121">Make sure you:</span></span>

* <span data-ttu-id="a8459-122">Copiare l'**ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="a8459-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="a8459-123">È necessario per eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a8459-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="a8459-124">Aggiungere la piattaforma **Web** per l'app.</span><span class="sxs-lookup"><span data-stu-id="a8459-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="a8459-125">Copiare l' **URI di reindirizzamento** dal portale.</span><span class="sxs-lookup"><span data-stu-id="a8459-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="a8459-126">È necessario usare il valore URI predefinito `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="a8459-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="a8459-127">2: Aggiungere prerequisiti alla directory</span><span class="sxs-lookup"><span data-stu-id="a8459-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="a8459-128">Al prompt dei comandi passare alla cartella radice, se necessario.</span><span class="sxs-lookup"><span data-stu-id="a8459-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="a8459-129">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8459-129">Run the following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="a8459-130">Nella struttura di avvio rapido si usa anche `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="a8459-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="a8459-131">In questo modo, vengono installate le librerie usate da `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a8459-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="a8459-132">3: Configurare l'app per l'uso della strategia passport-node-js</span><span class="sxs-lookup"><span data-stu-id="a8459-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="a8459-133">Configurare il middleware Express per l'uso del protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a8459-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a8459-134">Passport verrà usato, tra le altre cose, per inviare richieste di accesso e disconnessione, gestire la sessione utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="a8459-135">Nella radice del progetto aprire il file Config.js.</span><span class="sxs-lookup"><span data-stu-id="a8459-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="a8459-136">Nella sezione `exports.creds` immettere i valori di configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a8459-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="a8459-137">`clientID`: l'**ID applicazione** assegnato all'app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8459-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="a8459-138">`returnURL`: l'**URI di reindirizzamento** immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="a8459-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="a8459-139">`clientSecret`: il segreto generato nel portale.</span><span class="sxs-lookup"><span data-stu-id="a8459-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="a8459-140">Nella radice del progetto aprire il file App.js.</span><span class="sxs-lookup"><span data-stu-id="a8459-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="a8459-141">Per richiamare la strategia OIDCStrategy, fornita con `passport-azure-ad`, aggiungere la chiamata seguente:</span><span class="sxs-lookup"><span data-stu-id="a8459-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="a8459-142">Per gestire le richieste di accesso usare la strategia a cui si è appena fatto riferimento:</span><span class="sxs-lookup"><span data-stu-id="a8459-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

<span data-ttu-id="a8459-143">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via).</span><span class="sxs-lookup"><span data-stu-id="a8459-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="a8459-144">Tutti i writer di strategie rispettano questo modello.</span><span class="sxs-lookup"><span data-stu-id="a8459-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="a8459-145">Passare alla strategia un elemento `function()` che usa un token e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="a8459-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="a8459-146">La strategia viene restituita dopo l'esecuzione di tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="a8459-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="a8459-147">Archiviare l'utente e mettere da parte il token per non doverlo richiedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a8459-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a8459-148">Il codice precedente accetta qualsiasi utente che può eseguire l'autenticazione al server.</span><span class="sxs-lookup"><span data-stu-id="a8459-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="a8459-149">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="a8459-149">This is known as auto-registration.</span></span> <span data-ttu-id="a8459-150">Nei server di produzione è preferibile non consentire l'accesso a chiunque senza prima prevedere un processo di registrazione a scelta.</span><span class="sxs-lookup"><span data-stu-id="a8459-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="a8459-151">Questo è il criterio solitamente adottato per le app consumer.</span><span class="sxs-lookup"><span data-stu-id="a8459-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="a8459-152">L'app potrebbe consentire di eseguire la registrazione con Facebook, ma poi richiede di inserire informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a8459-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="a8459-153">Se per questa esercitazione non è stato usato un programma della riga di comando, è possibile estrarre il messaggio di posta elettronica dall'oggetto token restituito.</span><span class="sxs-lookup"><span data-stu-id="a8459-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="a8459-154">Quindi, è possibile chiedere all'utente di inserire informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a8459-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="a8459-155">Trattandosi di un server di test, è possibile aggiungere l'utente direttamente al database in-memory.</span><span class="sxs-lookup"><span data-stu-id="a8459-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="a8459-156">Aggiungere i metodi che consentono di tenere traccia degli utenti che hanno eseguito l'accesso, come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="a8459-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="a8459-157">Questa operazione include la serializzazione e deserializzazione delle informazioni dell'utente:</span><span class="sxs-lookup"><span data-stu-id="a8459-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  <span data-ttu-id="a8459-158">Aggiungere il codice che carica il motore di Express.</span><span class="sxs-lookup"><span data-stu-id="a8459-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="a8459-159">Verranno usati i modelli /views e /routes predefiniti forniti da Express:</span><span class="sxs-lookup"><span data-stu-id="a8459-159">You use the default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="a8459-160">Aggiungere le route POST che trasferiscono le richieste di accesso effettive al motore `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="a8459-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="a8459-161">4: Usare Passport per inviare le richieste di accesso e disconnessione ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8459-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="a8459-162">L'app è configurata ora per comunicare con l'endpoint 2.0 mediante il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a8459-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a8459-163">La strategia `passport-azure-ad` gestisce tutti i dettagli relativi alla creazione dei messaggi di autenticazione, alla convalida dei token da Azure AD e alla gestione della sessione utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="a8459-164">A questo punto, è sufficiente offrire agli utenti un modo per accedere e disconnettersi e per raccogliere informazioni aggiuntive sull'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="a8459-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="a8459-165">Aggiungere al file App.js i metodi **default**, **login**, **account** e **logout**:</span><span class="sxs-lookup"><span data-stu-id="a8459-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="a8459-166">Di seguito sono riportati i dettagli:</span><span class="sxs-lookup"><span data-stu-id="a8459-166">Here are the details:</span></span>
    
    * <span data-ttu-id="a8459-167">La route `/` reindirizza alla vista index.ejs e</span><span class="sxs-lookup"><span data-stu-id="a8459-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="a8459-168">passa l'utente nella richiesta (se esistente).</span><span class="sxs-lookup"><span data-stu-id="a8459-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="a8459-169">La route `/account` prima *verifica che l'utente sia autenticato* (questo passaggio viene implementato nel codice seguente)</span><span class="sxs-lookup"><span data-stu-id="a8459-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="a8459-170">e quindi passa l'utente nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="a8459-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="a8459-171">In questo modo è possibile ottenere altre informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="a8459-172">La route `/login` chiama l'autenticatore `azuread-openidconnect` da `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="a8459-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="a8459-173">Se l'operazione ha esito negativo, reindirizza di nuovo l'utente a `/login`.</span><span class="sxs-lookup"><span data-stu-id="a8459-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="a8459-174">La route `/logout` chiama la vista logout.ejs (e route).</span><span class="sxs-lookup"><span data-stu-id="a8459-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="a8459-175">I cookie vengono cancellati e quindi l'utente torna a index.ejs.</span><span class="sxs-lookup"><span data-stu-id="a8459-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="a8459-176">Aggiungere il metodo **EnsureAuthenticated** usato in precedenza in `/account`:</span><span class="sxs-lookup"><span data-stu-id="a8459-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="a8459-177">In App.js creare il server:</span><span class="sxs-lookup"><span data-stu-id="a8459-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="a8459-178">5: Creare le viste e le route in Express per visualizzare l'utente nel sito Web</span><span class="sxs-lookup"><span data-stu-id="a8459-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="a8459-179">Aggiungere le route e le viste che mostrano informazioni all'utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="a8459-180">Le route e le viste gestiscono anche le route `/logout` e `/login` precedentemente create.</span><span class="sxs-lookup"><span data-stu-id="a8459-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="a8459-181">Nella directory radice creare la route `/routes/index.js`.</span><span class="sxs-lookup"><span data-stu-id="a8459-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="a8459-182">Nella directory radice creare la route `/routes/user.js`.</span><span class="sxs-lookup"><span data-stu-id="a8459-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="a8459-183">`/routes/index.js` e `/routes/user.js` sono semplici route che passeranno la richiesta alle viste, incluso l'utente se presente.</span><span class="sxs-lookup"><span data-stu-id="a8459-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="a8459-184">Nella directory radice creare la vista `/views/index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="a8459-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="a8459-185">Questa pagina chiama i metodi **login** e **logout**.</span><span class="sxs-lookup"><span data-stu-id="a8459-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="a8459-186">È possibile anche usare la vista `/views/index.ejs` per acquisire informazioni sull'account.</span><span class="sxs-lookup"><span data-stu-id="a8459-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="a8459-187">È possibile usare l'espressione `if (!user)` condizionale quando l'utente viene passato nella richiesta,</span><span class="sxs-lookup"><span data-stu-id="a8459-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="a8459-188">a prova che l'utente ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a8459-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="a8459-189">Nella directory radice creare la vista `/views/account.ejs`.</span><span class="sxs-lookup"><span data-stu-id="a8459-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="a8459-190">La vista `/views/account.ejs` consente di visualizzare informazioni aggiuntive che `passport-azuread` inserisce nella richiesta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a8459-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="a8459-191">Aggiungere un layout.</span><span class="sxs-lookup"><span data-stu-id="a8459-191">Add a layout.</span></span> <span data-ttu-id="a8459-192">Nella directory radice creare la vista `/views/layout.ejs`.</span><span class="sxs-lookup"><span data-stu-id="a8459-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="a8459-193">Per compilare ed eseguire l'app, eseguire `node app.js`</span><span class="sxs-lookup"><span data-stu-id="a8459-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="a8459-194">e quindi passare a `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="a8459-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="a8459-195">Accedere con un account Microsoft personale o con un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a8459-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="a8459-196">Osservare come l'identità dell'utente sia riflessa nell'elenco /account.</span><span class="sxs-lookup"><span data-stu-id="a8459-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="a8459-197">Si dispone ora di un'app Web protetta tramite protocolli standard del settore.</span><span class="sxs-lookup"><span data-stu-id="a8459-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="a8459-198">È possibile autenticare gli utenti nell'app usando i relativi account personali e aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a8459-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8459-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8459-199">Next steps</span></span>
<span data-ttu-id="a8459-200">Come riferimento viene fornito l'esempio completato, senza i valori di configurazione, [come file zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a8459-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="a8459-201">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="a8459-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="a8459-202">È possibile ora passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="a8459-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="a8459-203">È consigliabile provare:</span><span class="sxs-lookup"><span data-stu-id="a8459-203">You might want to try:</span></span>

[<span data-ttu-id="a8459-204">Proteggere un'API Web Node.js usando l'endpoint 2.0</span><span class="sxs-lookup"><span data-stu-id="a8459-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="a8459-205">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="a8459-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="a8459-206">Guida per sviluppatori Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="a8459-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a8459-207">StackOverflow: tag "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="a8459-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a8459-208">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="a8459-208">Get security updates for our products</span></span>
<span data-ttu-id="a8459-209">È consigliabile eseguire l'iscrizione per ricevere una notifica quando si verificano problemi di protezione.</span><span class="sxs-lookup"><span data-stu-id="a8459-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="a8459-210">Nella pagina [Notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) effettuare la sottoscrizione agli advisory sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a8459-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

