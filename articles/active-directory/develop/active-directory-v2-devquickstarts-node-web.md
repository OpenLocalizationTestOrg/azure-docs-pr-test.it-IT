---
title: versione 2.0 di Active Directory aaaAzure sign-in app web Node. js | Documenti Microsoft
description: Informazioni su come toobuild un Node.js web app che un utente accede usando un account Microsoft personale e un account aziendale o dell'istituto di istruzione.
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
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="946a8-103">Aggiungere app web di accesso tooa Node.js</span><span class="sxs-lookup"><span data-stu-id="946a8-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="946a8-104">Non tutti gli scenari di Azure Active Directory e le funzionalità di lavoro con endpoint v 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="946a8-105">toodetermine se è necessario utilizzare hello v 2.0 endpoint o hello v 1.0, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="946a8-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="946a8-106">In questa esercitazione, si usa hello toodo Passport seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="946a8-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="946a8-107">In un'app web, l'accesso utente hello con Azure Active Directory (Azure AD) e hello v 2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="946a8-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="946a8-108">Visualizzare le informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-108">Display information about hello user.</span></span>
* <span data-ttu-id="946a8-109">Sign hello utente all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="946a8-110">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="946a8-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="946a8-111">Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="946a8-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="946a8-112">In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="946a8-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="946a8-113">È stata sviluppata una strategia per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="946a8-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="946a8-114">In questo articolo è illustrato come tooinstall hello modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="946a8-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="946a8-115">Scaricare</span><span class="sxs-lookup"><span data-stu-id="946a8-115">Download</span></span>
<span data-ttu-id="946a8-116">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="946a8-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="946a8-117">esercitazione di hello toofollow, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="946a8-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="946a8-118">È anche possibile ottenere un'applicazione hello completata alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="946a8-119">1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="946a8-119">1: Register an app</span></span>
<span data-ttu-id="946a8-120">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire [questi passaggi dettagliati](active-directory-v2-app-registration.md) tooregister un'app.</span><span class="sxs-lookup"><span data-stu-id="946a8-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="946a8-121">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="946a8-121">Make sure you:</span></span>

* <span data-ttu-id="946a8-122">Hello copia **Id applicazione** assegnato tooyour app.</span><span class="sxs-lookup"><span data-stu-id="946a8-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="946a8-123">È necessario per eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="946a8-124">Aggiungere hello **Web** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="946a8-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="946a8-125">Hello copia **URI di reindirizzamento** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="946a8-126">È necessario utilizzare hello URI valore predefinito `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="946a8-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="946a8-127">2: aggiungere directory tooyour dei prerequisiti</span><span class="sxs-lookup"><span data-stu-id="946a8-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="946a8-128">Al prompt dei comandi, modificare le directory toogo tooyour nella cartella radice fare se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="946a8-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="946a8-129">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="946a8-129">Run hello following commands:</span></span>

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

<span data-ttu-id="946a8-130">Inoltre, utilizziamo `passport-azure-ad` scheletro hello di avvio rapido di hello:</span><span class="sxs-lookup"><span data-stu-id="946a8-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="946a8-131">Ciò consente di installare le librerie di hello che `passport-azure-ad` utilizza.</span><span class="sxs-lookup"><span data-stu-id="946a8-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="946a8-132">3: impostare la strategia di passport-nodo-js hello toouse app</span><span class="sxs-lookup"><span data-stu-id="946a8-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="946a8-133">Impostare il middleware toouse hello protocollo di autenticazione OpenID Connect di hello Express.</span><span class="sxs-lookup"><span data-stu-id="946a8-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="946a8-134">Utilizzare le richieste di accesso e disconnessione tooissue Passport, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="946a8-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="946a8-135">Nella radice del progetto hello hello aprire file Config.js hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="946a8-136">In hello `exports.creds` sezione, immettere i valori di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="946a8-137">`clientID`: hello **Id applicazione** che viene assegnato tooyour app nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="946a8-138">`returnURL`: hello **URI di reindirizzamento** immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="946a8-139">`clientSecret`: il segreto hello generato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="946a8-140">Nella radice del progetto hello hello aprire file App.js hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="946a8-141">tooinvoke hello OIDCStrategy stratey, che viene fornito con `passport-azure-ad`, aggiungere hello in seguito a chiamata:</span><span class="sxs-lookup"><span data-stu-id="946a8-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="946a8-142">toohandle le richieste di accesso, utilizzare la strategia di hello solo a cui fa riferimento:</span><span class="sxs-lookup"><span data-stu-id="946a8-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
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

<span data-ttu-id="946a8-143">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via).</span><span class="sxs-lookup"><span data-stu-id="946a8-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="946a8-144">Tutti i writer strategia rispettare toohello modello.</span><span class="sxs-lookup"><span data-stu-id="946a8-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="946a8-145">Passare la strategia di hello un `function()` che utilizza un token e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="946a8-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="946a8-146">strategia di Hello viene restituito dopo esegue automaticamente tutte le relative operazioni.</span><span class="sxs-lookup"><span data-stu-id="946a8-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="946a8-147">Archivio utente hello e token hello stash pertanto non è necessario tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="946a8-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="946a8-148">Hello precedente il codice in tutti gli utenti possono eseguire l'autenticazione server tooyour.</span><span class="sxs-lookup"><span data-stu-id="946a8-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="946a8-149">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="946a8-149">This is known as auto-registration.</span></span> <span data-ttu-id="946a8-150">In un server di produzione, è preferibile toolet chiunque senza prima li passare attraverso un processo di registrazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="946a8-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="946a8-151">Si tratta in genere di modello di hello visualizzato nell'App consumer.</span><span class="sxs-lookup"><span data-stu-id="946a8-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="946a8-152">app Hello potrebbero consentire di tooregister con Facebook, ma viene chiesto di tooenter ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="946a8-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="946a8-153">Se non è stato utilizzato un programma della riga di comando per questa esercitazione, è stato possibile estrarre posta elettronica hello dall'oggetto hello token restituito.</span><span class="sxs-lookup"><span data-stu-id="946a8-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="946a8-154">Quindi, è possibile chiedere informazioni aggiuntive di hello utente tooenter.</span><span class="sxs-lookup"><span data-stu-id="946a8-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="946a8-155">Poiché si tratta di un server di prova, aggiungere l'utente hello toohello direttamente i database di in memoria.</span><span class="sxs-lookup"><span data-stu-id="946a8-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="946a8-156">Aggiungere metodi hello utilizzare traccia tookeep di utenti che hanno eseguito l'accesso, come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="946a8-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="946a8-157">Ciò include la serializzazione e deserializzazione delle informazioni dell'utente hello:</span><span class="sxs-lookup"><span data-stu-id="946a8-157">This includes serializing and deserializing hello user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  <span data-ttu-id="946a8-158">Aggiungere codice hello che carica il motore di Express hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="946a8-159">Utilizzare /views predefinito hello e modello /routes che esprimono offre:</span><span class="sxs-lookup"><span data-stu-id="946a8-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="946a8-160">Aggiungere hello POST instrada tale consegnare hello le richieste di accesso effettiva toohello `passport-azure-ad` motore:</span><span class="sxs-lookup"><span data-stu-id="946a8-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="946a8-161">4: usare Passport tooissue accesso e disconnessione richiede tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="946a8-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="946a8-162">L'app è ora impostato toocommunicate con endpoint v 2.0 hello con protocollo di autenticazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="946a8-163">Hello `passport-azure-ad` strategia si occupa di tutti i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione sessione utente hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="946a8-164">Tutto ciò che resta toodo è toogive agli utenti un modo toosign in e accedere out e toogather ulteriori informazioni sull'utente hello che ha effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="946a8-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="946a8-165">Aggiungere hello **predefinito**, **accesso**, **account**, e **logout** file App.js tooyour di metodi:</span><span class="sxs-lookup"><span data-stu-id="946a8-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="946a8-166">Di seguito sono riportati i dettagli di hello:</span><span class="sxs-lookup"><span data-stu-id="946a8-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="946a8-167">Hello `/` route reindirizza toohello index.ejs visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="946a8-168">Passa utente hello nella richiesta di hello (se presente).</span><span class="sxs-lookup"><span data-stu-id="946a8-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="946a8-169">Hello `/account` distribuito prima *assicura che sono autenticati* (è implementare che nel seguente codice hello).</span><span class="sxs-lookup"><span data-stu-id="946a8-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="946a8-170">Viene quindi passato utente hello nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="946a8-171">Si tratta pertanto è possibile ottenere ulteriori informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="946a8-172">Hello `/login` il routing delle chiamate del `azuread-openidconnect` autenticatore da `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="946a8-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="946a8-173">Se che non hanno esito positivo, viene reindirizzato nuovamente utente hello troppo`/login`.</span><span class="sxs-lookup"><span data-stu-id="946a8-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="946a8-174">Hello `/logout` route chiama logout.ejs visualizzazione hello (e route).</span><span class="sxs-lookup"><span data-stu-id="946a8-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="946a8-175">Ciò consente di cancellare i cookie e quindi restituisce hello tooindex.ejs indietro utente.</span><span class="sxs-lookup"><span data-stu-id="946a8-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="946a8-176">Aggiungere hello **EnsureAuthenticated** metodo utilizzato in precedenza nella `/account`:</span><span class="sxs-lookup"><span data-stu-id="946a8-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="946a8-177">In App.js, creare server hello:</span><span class="sxs-lookup"><span data-stu-id="946a8-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="946a8-178">5: creare visualizzazioni hello e route in Express mostrare l'utente nel sito Web di hello</span><span class="sxs-lookup"><span data-stu-id="946a8-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="946a8-179">Aggiungere le route hello e visualizzazioni che mostrano informazioni toohello utente.</span><span class="sxs-lookup"><span data-stu-id="946a8-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="946a8-180">viste e le route Hello anche gestiscono hello `/logout` e `/login` route creata.</span><span class="sxs-lookup"><span data-stu-id="946a8-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="946a8-181">Nella directory radice di hello, creare hello `/routes/index.js` route.</span><span class="sxs-lookup"><span data-stu-id="946a8-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="946a8-182">Nella directory radice di hello, creare hello `/routes/user.js` route.</span><span class="sxs-lookup"><span data-stu-id="946a8-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="946a8-183">`/routes/index.js`e `/routes/user.js` le route semplice che passano hello richiesta tooyour visualizzazioni, ad esempio utente hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="946a8-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="946a8-184">Nella directory radice di hello, creare hello `/views/index.ejs` visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="946a8-185">Questa pagina chiama i metodi **login** e **logout**.</span><span class="sxs-lookup"><span data-stu-id="946a8-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="946a8-186">Utilizzare inoltre hello `/views/index.ejs` consente di visualizzare informazioni sull'account toocapture.</span><span class="sxs-lookup"><span data-stu-id="946a8-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="946a8-187">È possibile utilizzare hello condizionale `if (!user)` come utente hello passati tramite richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="946a8-188">a prova che l'utente ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="946a8-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="946a8-189">Nella directory radice di hello, creare hello `/views/account.ejs` visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="946a8-190">Hello `/views/account.ejs` visualizzazione consente di informazioni aggiuntive tooview che `passport-azuread` inserisce nella richiesta utente hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="946a8-191">Aggiungere un layout.</span><span class="sxs-lookup"><span data-stu-id="946a8-191">Add a layout.</span></span> <span data-ttu-id="946a8-192">Nella directory radice di hello, creare hello `/views/layout.ejs` visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="946a8-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="946a8-193">toobuild ed eseguire l'app, eseguire `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="946a8-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="946a8-194">Quindi, passare troppo`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="946a8-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="946a8-195">Accedere con un account Microsoft personale o con un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="946a8-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="946a8-196">Si noti che l'identità dell'utente hello viene riflessa nell'elenco /account hello.</span><span class="sxs-lookup"><span data-stu-id="946a8-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="946a8-197">Si dispone ora di un'app Web protetta tramite protocolli standard del settore.</span><span class="sxs-lookup"><span data-stu-id="946a8-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="946a8-198">È possibile autenticare gli utenti nell'app usando i relativi account personali e aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="946a8-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="946a8-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="946a8-199">Next steps</span></span>
<span data-ttu-id="946a8-200">Per riferimento, l'esempio hello completata (senza i valori di configurazione) viene fornito come [un file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="946a8-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="946a8-201">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="946a8-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="946a8-202">Successivamente, è possibile passare argomenti avanzati toomore.</span><span class="sxs-lookup"><span data-stu-id="946a8-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="946a8-203">È possibile tootry:</span><span class="sxs-lookup"><span data-stu-id="946a8-203">You might want tootry:</span></span>

[<span data-ttu-id="946a8-204">Proteggere un'API web di Node.js tramite hello v 2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="946a8-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="946a8-205">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="946a8-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="946a8-206">Guida per sviluppatori Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="946a8-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="946a8-207">StackOverflow: tag "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="946a8-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="946a8-208">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="946a8-208">Get security updates for our products</span></span>
<span data-ttu-id="946a8-209">Che incoraggia la collaborazione toosign backup toobe notificate quando si verificano eventi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="946a8-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="946a8-210">In hello [notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) pagina, la sottoscrizione di avvisi advisory tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="946a8-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

