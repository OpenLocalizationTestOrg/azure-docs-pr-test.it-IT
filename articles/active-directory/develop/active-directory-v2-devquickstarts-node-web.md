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
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Aggiungere app web di accesso tooa Node.js

> [!NOTE]
> Non tutti gli scenari di Azure Active Directory e le funzionalità di lavoro con endpoint v 2.0 hello. toodetermine se è necessario utilizzare hello v 2.0 endpoint o hello v 1.0, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 

In questa esercitazione, si usa hello toodo Passport seguenti attività:

* In un'app web, l'accesso utente hello con Azure Active Directory (Azure AD) e hello v 2.0 endpoint.
* Visualizzare le informazioni sull'utente hello.
* Sign hello utente all'esterno dell'app hello.

**Passport** è il middleware di autenticazione per Node.js. Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify. In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni. È stata sviluppata una strategia per Azure AD. In questo articolo è illustrato come tooinstall hello modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.

## <a name="download"></a>Scaricare
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). esercitazione di hello toofollow, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) o scheletro hello clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

È anche possibile ottenere un'applicazione hello completata alla fine di hello di questa esercitazione.

## <a name="1-register-an-app"></a>1: Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire [questi passaggi dettagliati](active-directory-v2-app-registration.md) tooregister un'app. Assicurarsi di:

* Hello copia **Id applicazione** assegnato tooyour app. È necessario per eseguire questa esercitazione.
* Aggiungere hello **Web** piattaforma per l'app.
* Hello copia **URI di reindirizzamento** dal portale hello. È necessario utilizzare hello URI valore predefinito `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: aggiungere directory tooyour dei prerequisiti
Al prompt dei comandi, modificare le directory toogo tooyour nella cartella radice fare se non si è già presente. Eseguire hello seguenti comandi:

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

Inoltre, utilizziamo `passport-azure-ad` scheletro hello di avvio rapido di hello:

* `npm install passport-azure-ad`

Ciò consente di installare le librerie di hello che `passport-azure-ad` utilizza.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: impostare la strategia di passport-nodo-js hello toouse app
Impostare il middleware toouse hello protocollo di autenticazione OpenID Connect di hello Express. Utilizzare le richieste di accesso e disconnessione tooissue Passport, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.

1.  Nella radice del progetto hello hello aprire file Config.js hello. In hello `exports.creds` sezione, immettere i valori di configurazione dell'applicazione.
  
  * `clientID`: hello **Id applicazione** che viene assegnato tooyour app nel portale di Azure hello.
  * `returnURL`: hello **URI di reindirizzamento** immesso nel portale di hello.
  * `clientSecret`: il segreto hello generato nel portale di hello.

2.  Nella radice del progetto hello hello aprire file App.js hello. tooinvoke hello OIDCStrategy stratey, che viene fornito con `passport-azure-ad`, aggiungere hello in seguito a chiamata:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle le richieste di accesso, utilizzare la strategia di hello solo a cui fa riferimento:

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

Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via). Tutti i writer strategia rispettare toohello modello. Passare la strategia di hello un `function()` che utilizza un token e `done` come parametri. strategia di Hello viene restituito dopo esegue automaticamente tutte le relative operazioni. Archivio utente hello e token hello stash pertanto non è necessario tooask per tale nuovamente.

  > [!IMPORTANT]
  > Hello precedente il codice in tutti gli utenti possono eseguire l'autenticazione server tooyour. Questa operazione è nota come registrazione automatica. In un server di produzione, è preferibile toolet chiunque senza prima li passare attraverso un processo di registrazione desiderato. Si tratta in genere di modello di hello visualizzato nell'App consumer. app Hello potrebbero consentire di tooregister con Facebook, ma viene chiesto di tooenter ulteriori informazioni. Se non è stato utilizzato un programma della riga di comando per questa esercitazione, è stato possibile estrarre posta elettronica hello dall'oggetto hello token restituito. Quindi, è possibile chiedere informazioni aggiuntive di hello utente tooenter. Poiché si tratta di un server di prova, aggiungere l'utente hello toohello direttamente i database di in memoria.
  > 
  > 

4.  Aggiungere metodi hello utilizzare traccia tookeep di utenti che hanno eseguito l'accesso, come richiesto da Passport. Ciò include la serializzazione e deserializzazione delle informazioni dell'utente hello:

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

5.  Aggiungere codice hello che carica il motore di Express hello. Utilizzare /views predefinito hello e modello /routes che esprimono offre:

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

6.  Aggiungere hello POST instrada tale consegnare hello le richieste di accesso effettiva toohello `passport-azure-ad` motore:

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: usare Passport tooissue accesso e disconnessione richiede tooAzure AD
L'app è ora impostato toocommunicate con endpoint v 2.0 hello con protocollo di autenticazione OpenID Connect hello. Hello `passport-azure-ad` strategia si occupa di tutti i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione sessione utente hello. Tutto ciò che resta toodo è toogive agli utenti un modo toosign in e accedere out e toogather ulteriori informazioni sull'utente hello che ha effettuato l'accesso.

1.  Aggiungere hello **predefinito**, **accesso**, **account**, e **logout** file App.js tooyour di metodi:

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

  Di seguito sono riportati i dettagli di hello:
    
    * Hello `/` route reindirizza toohello index.ejs visualizzazione. Passa utente hello nella richiesta di hello (se presente).
    * Hello `/account` distribuito prima *assicura che sono autenticati* (è implementare che nel seguente codice hello). Viene quindi passato utente hello nella richiesta di hello. Si tratta pertanto è possibile ottenere ulteriori informazioni sull'utente hello.
    * Hello `/login` il routing delle chiamate del `azuread-openidconnect` autenticatore da `passport-azuread`. Se che non hanno esito positivo, viene reindirizzato nuovamente utente hello troppo`/login`.
    * Hello `/logout` route chiama logout.ejs visualizzazione hello (e route). Ciò consente di cancellare i cookie e quindi restituisce hello tooindex.ejs indietro utente.

2.  Aggiungere hello **EnsureAuthenticated** metodo utilizzato in precedenza nella `/account`:

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

3.  In App.js, creare server hello:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: creare visualizzazioni hello e route in Express mostrare l'utente nel sito Web di hello
Aggiungere le route hello e visualizzazioni che mostrano informazioni toohello utente. viste e le route Hello anche gestiscono hello `/logout` e `/login` route creata.

1. Nella directory radice di hello, creare hello `/routes/index.js` route.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  Nella directory radice di hello, creare hello `/routes/user.js` route.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`e `/routes/user.js` le route semplice che passano hello richiesta tooyour visualizzazioni, ad esempio utente hello, se presente.

3.  Nella directory radice di hello, creare hello `/views/index.ejs` visualizzazione. Questa pagina chiama i metodi **login** e **logout**. Utilizzare inoltre hello `/views/index.ejs` consente di visualizzare informazioni sull'account toocapture. È possibile utilizzare hello condizionale `if (!user)` come utente hello passati tramite richiesta hello. a prova che l'utente ha eseguito l'accesso.

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

4.  Nella directory radice di hello, creare hello `/views/account.ejs` visualizzazione. Hello `/views/account.ejs` visualizzazione consente di informazioni aggiuntive tooview che `passport-azuread` inserisce nella richiesta utente hello.

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

5.  Aggiungere un layout. Nella directory radice di hello, creare hello `/views/layout.ejs` visualizzazione.

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

6.  toobuild ed eseguire l'app, eseguire `node app.js`. Quindi, passare troppo`http://localhost:3000`.

7.  Accedere con un account Microsoft personale o con un account aziendale o dell'istituto di istruzione. Si noti che l'identità dell'utente hello viene riflessa nell'elenco /account hello. 

Si dispone ora di un'app Web protetta tramite protocolli standard del settore. È possibile autenticare gli utenti nell'app usando i relativi account personali e aziendali o dell'istituto di istruzione.

## <a name="next-steps"></a>Passaggi successivi
Per riferimento, l'esempio hello completata (senza i valori di configurazione) viene fornito come [un file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). È anche possibile clonarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Successivamente, è possibile passare argomenti avanzati toomore. È possibile tootry:

[Proteggere un'API web di Node.js tramite hello v 2.0 endpoint](active-directory-v2-devquickstarts-node-api.md)

Altre risorse:

* [Guida per sviluppatori Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "azure-active-directory"](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Che incoraggia la collaborazione toosign backup toobe notificate quando si verificano eventi di sicurezza. In hello [notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) pagina, la sottoscrizione di avvisi advisory tooSecurity.

