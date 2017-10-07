---
title: aaaGetting avviata con Accedi AD Azure e la disconnessione con Node.js | Documenti Microsoft
description: Informazioni su come toobuild un MVC Express Node.js web app che si integra con Azure AD per l'accesso.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Accesso e disconnessione all'app Web di Node. js con Azure AD
Passport viene usato per:

* Sign hello utente in app toohello con Azure Active Directory (Azure AD).
* Visualizzare le informazioni sull'utente hello.
* Sign hello utente all'esterno dell'app hello.

Passport è il middleware di autenticazione per Node.js. Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o restify applicazione web. Una gamma completa di strategie supporta l'autenticazione mediante nome utente e password, Facebook, Twitter e altro ancora. È stata sviluppata una strategia per Microsoft Azure Active Directory. È installare il modulo e quindi aggiungere hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo, hello take alla procedura seguente:

1. Registrare un'app.
2. Impostare il hello toouse app `passport-azure-ad` strategia.
3. Usare Passport tooissue Accedi e richieste di disconnessione tooAzure Active Directory.
4. Stampare i dati relativi a utente hello.

codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow lungo, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o scheletro hello clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

un'applicazione Hello completato viene fornita alla fine hello anche in questa esercitazione.

## <a name="step-1-register-an-app"></a>Passaggio 1: Registrare un'app
1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel menu di hello nella parte superiore di hello di hello pagina, selezionare l'account. In hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.

3. Selezionare **più servizi** in hello menu hello lasciato lato dello schermo hello e quindi selezionare **Azure Active Directory**.

4. Selezionare **Registrazioni per l'app**, quindi scegliere **Aggiungi**.

5. Seguire hello richieste toocreate un **applicazione Web** e/o **WebAPI**.
  * Hello **nome** di hello applicazione descrive toousers l'applicazione.

  * Hello **Sign-On URL** hello URL di base dell'app.  Hello valore predefinito del scheletro è ' http://localhost:3000/Authentication/openid/restituito '.

6. Dopo la registrazione, Azure AD assegna all'app un ID applicazione univoco. È necessario questo valore nella seguente hello sezioni, quindi copiarlo dalla pagina dell'applicazione hello.
7. Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App. Hello **URI ID App** è un identificatore univoco per l'applicazione. convenzione di Hello è formato hello toouse `https://<tenant-domain>/<app-name>`, ad esempio: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Passaggio 2: Aggiungere directory tooyour prerequisiti
1. Dalla riga di comando hello, Modifica cartella radice di directory tooyour se non si è già presente, e quindi esecuzione hello seguenti comandi:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Inoltre, è necessario `passport-azure-ad`:
    * `npm install passport-azure-ad`

Ciò consente di installare le librerie di hello che `passport-azure-ad` dipende.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Passaggio 3: Impostare la strategia di passport-nodo-js hello toouse app
In questo caso, è stato possibile configurare Express toouse hello OpenID Connect il protocollo di autenticazione.  Passport è toodo utilizzato diversi elementi, incluse le richieste di accesso e disconnessione problema, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello.

1. toobegin, aprire hello `config.js` file alla radice hello hello progetto e quindi immettere i valori di configurazione dell'applicazione in hello `exports.creds` sezione.

  * Hello `clientID` è hello **Id applicazione** che viene assegnato tooyour app nel portale di registrazione hello.

  * Hello `returnURL` è hello **Uri di reindirizzamento** immesso nel portale di hello.

  * Hello `clientSecret` segreto hello generato nel portale di hello.

2. Aprire quindi hello `app.js` file nella directory radice del progetto hello hello. Aggiungere quindi hello seguente chiamata tooinvoke hello `OIDCStrategy` strategia che prevede `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Successivamente, utilizzare la strategia di hello è solo a cui fa riferimento toohandle nostri richieste di accesso.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
        // asynchronous verification, for effect...
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
Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via) seguite dagli scrittori della strategia. Esaminando la strategia di hello, vedrai che vengono passati una funzione che ha un token e un fatto come parametri hello. strategia di Hello proviene toous nuovamente dopo che esegue il proprio lavoro. Quindi è importante utente hello toostore e token hello stash è necessario tooask per tale nuovamente.

> [!IMPORTANT]
il codice precedente di Hello in tutti gli utenti che si verificano tooauthenticate tooour server. Questa operazione è nota come registrazione automatica. È consigliabile non consentire tutti gli utenti ad autenticare il server di produzione tooa senza prima li registrate tramite un processo che si decide in. Si tratta in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere tooprovide ulteriori informazioni. Se questo non sono stati di un'applicazione di esempio, è possibile estrarre indirizzo di posta elettronica dell'utente hello dall'oggetto token hello è restituito e quindi richiesto hello utente toofill informazioni aggiuntive. Poiché si tratta di un server di prova, aggiungerli database in memoria toohello.


4. Successivamente, aggiungere metodi hello che consentano di risalire tootrack hello utenti connessi come richiesto da Passport. Questi metodi includono la serializzazione e deserializzazione hello le informazioni utente.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Successivamente, aggiungere il motore Express hello di hello code tooload. Qui utilizziamo /views predefinito hello e modello /routes che esprimono offre.

    ```JavaScript

        // configure Express (section 2)

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

6. Infine, aggiungere hello instrada tale consegnare hello le richieste di accesso effettiva toohello `passport-azure-ad` motore:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Passaggio 4: Usare Passport tooissue Accedi e richieste di disconnessione tooAzure AD
L'app è configurato correttamente toocommunicate con endpoint hello tramite protocollo di autenticazione OpenID Connect hello.  `passport-azure-ad`ha preso in considerazione tutti i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione delle sessioni utente. Che rimane garantisce agli utenti un modo toosign in sia di disconnessione e raccolto le informazioni aggiuntive sugli utenti connessi di hello.

1. In primo luogo, aggiungere predefinito hello, accesso, account e metodi disconnessione tooour `app.js` file:

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Esaminare nel dettaglio questi aspetti:

  * Hello `/`route reindirizza toohello index.ejs vista, passando utente hello richiesta hello (se presente).
  * Hello `/account` distribuito prima *assicura ci stiamo autenticate* (è implementare che nell'esempio seguente hello), e quindi passa hello utente nella richiesta di hello in modo che è possibile ottenere ulteriori informazioni sull'utente hello.
  * Hello `/login` route chiama l'autenticatore azuread openidconnect da `passport-azuread`. Se che non hanno esito positivo, viene reindirizzato hello indietro troppo/account di accesso utente.
  * Hello `/logout` route chiama semplicemente hello logout.ejs e route, che cancella cookie e quindi restituisce hello tooindex.ejs indietro utente.

3. Per l'ultima parte di hello del `app.js`, aggiungere hello **EnsureAuthenticated** metodo utilizzato in `/account`, come illustrato in precedenza.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Infine, creare server hello in `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Passaggio 5: toodisplay l'utente nel sito Web di hello, creare visualizzazioni hello e route in Express
Ora il file `app.js` è completo. È semplicemente necessario route hello tooadd e visualizzazioni che mostrano informazioni hello è ottenere toohello utente, nonché gestire hello `/logout` e `/login` route creata.

1. Creare hello `/routes/index.js` route nella directory radice hello.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Creare hello `/routes/user.js` route nella directory radice hello.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Questi passano hello richiesta tooour visualizzazioni, ad esempio utente hello se presente.

3. Creare hello `/views/index.ejs` visualizzazione nella directory radice hello. Si tratta di una pagina semplice che chiama i metodi di accesso e disconnessione e consente di ottenere informazioni sull'account toograb. Si noti che è possibile utilizzare hello condizionale `if (!user)` come utente hello passati tramite richiesta hello evidenza abbiamo un utente connesso.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Creare hello `/views/account.ejs` visualizzazione nella directory radice hello in modo che è possibile visualizzare informazioni aggiuntive che `passport-azuread` è inserito nella richiesta utente hello.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Ora viene aggiunto un layout per modificare l'aspetto. Creare hello ' / directory radice di visualizzazione degli views/layout.ejs in hello.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Passaggi successivi
Per finire, compilare ed eseguire l'app. Eseguire `node app.js`, quindi andare troppo`http://localhost:3000`.

Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione e notare come identità dell'utente hello si riflette nell'elenco /account hello. È ora disponibile un'app Web protetta con protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). In alternativa, è possibile eseguire la clonazione da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Ora è possibile passare ad argomenti più avanzati. È possibile tootry:

[Proteggere un'API Web con Azure AD](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
