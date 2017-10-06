---
title: aaaAdd Accedi tooa Node.js dell'app web Azure B2C | Documenti Microsoft
description: Come toobuild un'app web Node. js che accede agli utenti tramite un tenant B2C.
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure Active Directory B2C: Aggiungere app web di accesso tooa Node.js

**Passport** è il middleware di autenticazione per Node.js. Passport, estremamente flessibile e modulare, può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify. Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora.

È stata sviluppata una strategia per Azure Active Directory (Azure AD). Verranno installate in questo modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.

toodo, è necessario:

1. Registrare un'applicazione usando Azure AD.
2. Impostare il hello toouse app `passport-azure-ad` plug-in.
3. Usare Passport tooissue Accedi e richieste di disconnessione tooAzure Active Directory.
4. Stampare i dati utente.

Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow lungo, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). È anche possibile clonare scheletro hello:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

un'applicazione Hello completato viene fornita alla fine di hello di questa esercitazione.

## <a name="get-an-azure-ad-b2c-directory"></a>Ottenere una directory di Azure AD B2C

Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.  Una directory è un contenitore per utenti, app, gruppi e così via. Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.

## <a name="create-an-application"></a>Creare un'applicazione

Successivamente, è necessario toocreate un'app nel servizio directory B2C. Vengono riportate informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app. Entrambi hello app client e l'API web sarà rappresentato da un singolo **ID applicazione**, poiché comprendono una sola app logica. toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md). Assicurarsi di:

- Includere un **app web**/**web API** in un'applicazione hello.
- Immettere `http://localhost:3000/auth/openid/return` come **URL di risposta**. È l'URL predefinito hello per questo esempio di codice.
- Creare un **segreto applicazione** per l'applicazione e prenderne nota. Sarà necessario più avanti. Si noti che questo valore deve toobe [XML sottoposto a escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) prima di utilizzarlo.
- Hello copia **ID applicazione** ovvero tooyour assegnato app. Sarà necessario più avanti.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri

In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questa app contiene tre esperienze di identità: iscrizione, accesso e accesso con Facebook. È necessario toocreate questo criterio di ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Durante la creazione dei tre criteri assicurarsi di:

- Scegliere hello **nome visualizzato** e altri attributi per l'abbonamento nel criterio di iscrizione.
- Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio. È consentito scegliere anche altre attestazioni.
- Hello copia **nome** dei criteri dopo averlo creato. Devono contenere il prefisso hello `b2c_1_`.  I nomi dei criteri saranno necessari in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo aver creato i tre criteri, si è pronti toobuild l'app.

Si noti che questo articolo non viene illustrata la modalità criteri hello toouse appena creato. toolearn sul funzionamento dei criteri in Azure Active Directory B2C, iniziare con hello [.NET web app esercitazione introduttiva](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Aggiunta di prerequisiti tooyour directory

Dalla riga di comando hello, Modifica cartella radice tooyour di directory, se non si è già presente. Eseguire hello seguenti comandi:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Inoltre, abbiamo utilizzato `passport-azure-ad` per l'anteprima scheletro hello di hello Guida introduttiva.

- `npm install passport-azure-ad`

Verranno installate le librerie di hello che `passport-azure-ad` dipende.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Impostare il hello toouse app strategia Passport Node.js
Configurare hello toouse di hello Express middleware OpenID Connect di protocollo di autenticazione. Passport verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire le sessioni utente e ottenere informazioni sugli utenti, tra le altre azioni.

Aprire hello `config.js` file nella directory radice del progetto hello hello e immettere i valori di configurazione dell'applicazione hello `exports.creds` sezione.
- `clientID`: hello **ID applicazione** assegnato tooyour app nel portale di registrazione hello.
- `returnURL`: hello **URI di reindirizzamento** immesso nel portale di hello.
- `tenantName`: nome del tenant hello dell'app, ad esempio, **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Aprire hello `app.js` file nella directory radice del progetto hello hello. Aggiungere hello seguente chiamata tooinvoke hello `OIDCStrategy` strategia che prevede `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Utilizzare la strategia di hello è stato fatto riferimento solo le richieste di accesso toohandle.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
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
Passport usa un modello simile per tutte le strategie (inclusi Twitter e Facebook). Tutti i writer strategia rispettare toothis modello. Quando si esamina la strategia di hello, è possibile vedere che si passa un `function()` che dispone di un token e un `done` come parametri hello. strategia di Hello torna tooyou dopo che ha eseguito tutte le operazioni. Archivio utente hello e accantonare token hello in modo che non sia necessario tooask per tale nuovamente.

> [!IMPORTANT]
Hello precedente il codice in tutti gli utenti che esegue l'autenticazione server hello. Questa operazione è la registrazione automatica. Quando si utilizzano server di produzione, non si desidera toolet gli utenti a meno che non che sono state registrate tramite un processo di registrazione che è stato impostato. Questo modello è frequente nelle app consumer Che consentono di tooregister con Facebook, ma quindi vengono chiesto toofill informazioni aggiuntive. Se l'applicazione non è un esempio, è stato possibile estrarre un indirizzo di posta elettronica da oggetto hello token restituito e quindi chiedere hello utente toofill informazioni aggiuntive. Poiché si tratta di un server di prova, è sufficiente aggiungere i database in memoria toohello di utenti.

Aggiungere metodi hello che consentono di tenere traccia di tookeep di utenti che hanno effettuato l'accesso, come richiesto da Passport. Questa operazione include la serializzazione e la deserializzazione delle informazioni dell'utente:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Aggiungere il motore Express hello di hello code tooload. Nella seguente hello, è possibile visualizzare l'utilizzo predefinito di hello `/views` e `/routes` modello che fornisce Express.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Aggiungere hello `POST` route consegnare hello toohello le richieste di accesso effettiva `passport-azure-ad` motore:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Usare Passport tooissue Accedi e richieste di disconnessione tooAzure AD

L'app è configurato correttamente toocommunicate con endpoint v 2.0 hello tramite protocollo di autenticazione OpenID Connect hello. `passport-azure-ad`ha preso in considerazione dei dettagli di hello relativi alla creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione della sessione utente. Che rimane è toogive agli utenti un modo toosign in e accedere out e toogather ulteriori informazioni sugli utenti che hanno effettuato l'accesso.

Aggiungere innanzitutto predefinito hello, accesso, account e metodi disconnessione tooyour `app.js` file:

```JavaScript

//Routes (Section 4)

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

tooreview questi metodi in modo dettagliato:
- Hello `/` route reindirizza toohello `index.ejs` vista passando utente hello nella richiesta di hello (se presente).
- Hello `/account` route verifica innanzitutto che sono autenticati (hello implementazione di questa situazione sotto). Passa quindi utente hello nella richiesta di hello in modo che sia possibile ottenere ulteriori informazioni sull'utente hello.
- Hello `/login` route chiamate hello `azuread-openidconnect` autenticatore da `passport-azure-ad`. Se non viene completato, route hello utente viene reindirizzato hello nuovamente troppo`/login`.
- `/logout` chiama semplicemente `logout.ejs` e la rispettiva route. Ciò consente di cancellare i cookie e quindi restituisce hello utente nuovamente troppo`index.ejs`.


Per l'ultima parte di hello del `app.js`, aggiungere hello `EnsureAuthenticated` metodo utilizzato in hello `/account` route.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Infine, creare server hello in `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Creare visualizzazioni hello e instrada in Express toocall i criteri

`app.js` è stato completato. È sufficiente route hello tooadd e visualizzazioni che consentono di criteri di accesso ed effettuare l'iscrizione hello toocall. Questi anche gestire hello `/logout` e `/login` route creata.

Creare hello `/routes/index.js` route nella directory radice hello.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Creare hello `/routes/user.js` route nella directory radice hello.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Queste route semplice passano dalle visualizzazioni tooyour richieste. Includono utente hello, se presente.

Creare hello `/views/index.ejs` visualizzazione nella directory radice hello. Si tratta di una semplice pagina che chiama i criteri per l'accesso e la disconnessione. È possibile inoltre utilizzare è toograb informazioni dell'account. Si noti che è possibile utilizzare hello condizionale `if (!user)` come utente hello viene passata nella richiesta hello tooprovide evidenza utente hello è connesso.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Creare hello `/views/account.ejs` visualizzazione nella directory radice hello in modo che è possibile visualizzare informazioni aggiuntive che `passport-azure-ad` inserito nella richiesta utente hello.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Ora è possibile compilare ed eseguire l'app.

Eseguire `node app.js` e passare troppo`http://localhost:3000`


Iscriversi o accedere nell'app toohello tramite e-mail o Facebook. Disconnettersi e accedere nuovamente come un utente diverso.

##<a name="next-steps"></a>Passaggi successivi

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). È anche possibile clonarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

È possibile procedere con toomore argomenti avanzati. È possibile provare a:

[Proteggere un'API web utilizzando il modello di hello B2C in Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
