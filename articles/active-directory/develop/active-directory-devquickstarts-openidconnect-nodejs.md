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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="acdaf-103">Accesso e disconnessione all'app Web di Node. js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdaf-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="acdaf-104">Passport viene usato per:</span><span class="sxs-lookup"><span data-stu-id="acdaf-104">Here we use Passport to:</span></span>

* <span data-ttu-id="acdaf-105">Sign hello utente in app toohello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acdaf-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="acdaf-106">Visualizzare le informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-106">Display information about hello user.</span></span>
* <span data-ttu-id="acdaf-107">Sign hello utente all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="acdaf-108">Passport è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="acdaf-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="acdaf-109">Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o restify applicazione web.</span><span class="sxs-lookup"><span data-stu-id="acdaf-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="acdaf-110">Una gamma completa di strategie supporta l'autenticazione mediante nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="acdaf-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="acdaf-111">È stata sviluppata una strategia per Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="acdaf-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="acdaf-112">È installare il modulo e quindi aggiungere hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="acdaf-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="acdaf-113">toodo, hello take alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="acdaf-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="acdaf-114">Registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="acdaf-114">Register an app.</span></span>
2. <span data-ttu-id="acdaf-115">Impostare il hello toouse app `passport-azure-ad` strategia.</span><span class="sxs-lookup"><span data-stu-id="acdaf-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="acdaf-116">Usare Passport tooissue Accedi e richieste di disconnessione tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="acdaf-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="acdaf-117">Stampare i dati relativi a utente hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-117">Print data about hello user.</span></span>

<span data-ttu-id="acdaf-118">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="acdaf-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="acdaf-119">toofollow lungo, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="acdaf-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="acdaf-120">un'applicazione Hello completato viene fornita alla fine hello anche in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="acdaf-121">Passaggio 1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="acdaf-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="acdaf-122">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="acdaf-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="acdaf-123">Nel menu di hello nella parte superiore di hello di hello pagina, selezionare l'account.</span><span class="sxs-lookup"><span data-stu-id="acdaf-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="acdaf-124">In hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="acdaf-125">Selezionare **più servizi** in hello menu hello lasciato lato dello schermo hello e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acdaf-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="acdaf-126">Selezionare **Registrazioni per l'app**, quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="acdaf-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="acdaf-127">Seguire hello richieste toocreate un **applicazione Web** e/o **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="acdaf-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="acdaf-128">Hello **nome** di hello applicazione descrive toousers l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="acdaf-129">Hello **Sign-On URL** hello URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="acdaf-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="acdaf-130">Hello valore predefinito del scheletro è ' http://localhost:3000/Authentication/openid/restituito '.</span><span class="sxs-lookup"><span data-stu-id="acdaf-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="acdaf-131">Dopo la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="acdaf-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="acdaf-132">È necessario questo valore nella seguente hello sezioni, quindi copiarlo dalla pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="acdaf-133">Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App.</span><span class="sxs-lookup"><span data-stu-id="acdaf-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="acdaf-134">Hello **URI ID App** è un identificatore univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="acdaf-135">convenzione di Hello è formato hello toouse `https://<tenant-domain>/<app-name>`, ad esempio: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="acdaf-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="acdaf-136">Passaggio 2: Aggiungere directory tooyour prerequisiti</span><span class="sxs-lookup"><span data-stu-id="acdaf-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="acdaf-137">Dalla riga di comando hello, Modifica cartella radice di directory tooyour se non si è già presente, e quindi esecuzione hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="acdaf-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="acdaf-138">Inoltre, è necessario `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="acdaf-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="acdaf-139">Ciò consente di installare le librerie di hello che `passport-azure-ad` dipende.</span><span class="sxs-lookup"><span data-stu-id="acdaf-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="acdaf-140">Passaggio 3: Impostare la strategia di passport-nodo-js hello toouse app</span><span class="sxs-lookup"><span data-stu-id="acdaf-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="acdaf-141">In questo caso, è stato possibile configurare Express toouse hello OpenID Connect il protocollo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="acdaf-142">Passport è toodo utilizzato diversi elementi, incluse le richieste di accesso e disconnessione problema, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="acdaf-143">toobegin, aprire hello `config.js` file alla radice hello hello progetto e quindi immettere i valori di configurazione dell'applicazione in hello `exports.creds` sezione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="acdaf-144">Hello `clientID` è hello **Id applicazione** che viene assegnato tooyour app nel portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="acdaf-145">Hello `returnURL` è hello **Uri di reindirizzamento** immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="acdaf-146">Hello `clientSecret` segreto hello generato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="acdaf-147">Aprire quindi hello `app.js` file nella directory radice del progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="acdaf-148">Aggiungere quindi hello seguente chiamata tooinvoke hello `OIDCStrategy` strategia che prevede `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="acdaf-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="acdaf-149">Successivamente, utilizzare la strategia di hello è solo a cui fa riferimento toohandle nostri richieste di accesso.</span><span class="sxs-lookup"><span data-stu-id="acdaf-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="acdaf-150">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via) seguite dagli scrittori della strategia.</span><span class="sxs-lookup"><span data-stu-id="acdaf-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="acdaf-151">Esaminando la strategia di hello, vedrai che vengono passati una funzione che ha un token e un fatto come parametri hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="acdaf-152">strategia di Hello proviene toous nuovamente dopo che esegue il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="acdaf-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="acdaf-153">Quindi è importante utente hello toostore e token hello stash è necessario tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="acdaf-154">il codice precedente di Hello in tutti gli utenti che si verificano tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="acdaf-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="acdaf-155">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="acdaf-155">This is known as auto-registration.</span></span> <span data-ttu-id="acdaf-156">È consigliabile non consentire tutti gli utenti ad autenticare il server di produzione tooa senza prima li registrate tramite un processo che si decide in.</span><span class="sxs-lookup"><span data-stu-id="acdaf-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="acdaf-157">Si tratta in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere tooprovide ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="acdaf-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="acdaf-158">Se questo non sono stati di un'applicazione di esempio, è possibile estrarre indirizzo di posta elettronica dell'utente hello dall'oggetto token hello è restituito e quindi richiesto hello utente toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="acdaf-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="acdaf-159">Poiché si tratta di un server di prova, aggiungerli database in memoria toohello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="acdaf-160">Successivamente, aggiungere metodi hello che consentano di risalire tootrack hello utenti connessi come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="acdaf-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="acdaf-161">Questi metodi includono la serializzazione e deserializzazione hello le informazioni utente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="acdaf-162">Successivamente, aggiungere il motore Express hello di hello code tooload.</span><span class="sxs-lookup"><span data-stu-id="acdaf-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="acdaf-163">Qui utilizziamo /views predefinito hello e modello /routes che esprimono offre.</span><span class="sxs-lookup"><span data-stu-id="acdaf-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="acdaf-164">Infine, aggiungere hello instrada tale consegnare hello le richieste di accesso effettiva toohello `passport-azure-ad` motore:</span><span class="sxs-lookup"><span data-stu-id="acdaf-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="acdaf-165">Passaggio 4: Usare Passport tooissue Accedi e richieste di disconnessione tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="acdaf-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="acdaf-166">L'app è configurato correttamente toocommunicate con endpoint hello tramite protocollo di autenticazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="acdaf-167">`passport-azure-ad`ha preso in considerazione tutti i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione delle sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="acdaf-168">Che rimane garantisce agli utenti un modo toosign in sia di disconnessione e raccolto le informazioni aggiuntive sugli utenti connessi di hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="acdaf-169">In primo luogo, aggiungere predefinito hello, accesso, account e metodi disconnessione tooour `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="acdaf-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="acdaf-170">Esaminare nel dettaglio questi aspetti:</span><span class="sxs-lookup"><span data-stu-id="acdaf-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="acdaf-171">Hello `/`route reindirizza toohello index.ejs vista, passando utente hello richiesta hello (se presente).</span><span class="sxs-lookup"><span data-stu-id="acdaf-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="acdaf-172">Hello `/account` distribuito prima *assicura ci stiamo autenticate* (è implementare che nell'esempio seguente hello), e quindi passa hello utente nella richiesta di hello in modo che è possibile ottenere ulteriori informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="acdaf-173">Hello `/login` route chiama l'autenticatore azuread openidconnect da `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="acdaf-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="acdaf-174">Se che non hanno esito positivo, viene reindirizzato hello indietro troppo/account di accesso utente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="acdaf-175">Hello `/logout` route chiama semplicemente hello logout.ejs e route, che cancella cookie e quindi restituisce hello tooindex.ejs indietro utente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="acdaf-176">Per l'ultima parte di hello del `app.js`, aggiungere hello **EnsureAuthenticated** metodo utilizzato in `/account`, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="acdaf-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="acdaf-177">Infine, creare server hello in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="acdaf-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="acdaf-178">Passaggio 5: toodisplay l'utente nel sito Web di hello, creare visualizzazioni hello e route in Express</span><span class="sxs-lookup"><span data-stu-id="acdaf-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="acdaf-179">Ora il file `app.js` è completo.</span><span class="sxs-lookup"><span data-stu-id="acdaf-179">Now `app.js` is complete.</span></span> <span data-ttu-id="acdaf-180">È semplicemente necessario route hello tooadd e visualizzazioni che mostrano informazioni hello è ottenere toohello utente, nonché gestire hello `/logout` e `/login` route creata.</span><span class="sxs-lookup"><span data-stu-id="acdaf-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="acdaf-181">Creare hello `/routes/index.js` route nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="acdaf-182">Creare hello `/routes/user.js` route nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="acdaf-183">Questi passano hello richiesta tooour visualizzazioni, ad esempio utente hello se presente.</span><span class="sxs-lookup"><span data-stu-id="acdaf-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="acdaf-184">Creare hello `/views/index.ejs` visualizzazione nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="acdaf-185">Si tratta di una pagina semplice che chiama i metodi di accesso e disconnessione e consente di ottenere informazioni sull'account toograb.</span><span class="sxs-lookup"><span data-stu-id="acdaf-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="acdaf-186">Si noti che è possibile utilizzare hello condizionale `if (!user)` come utente hello passati tramite richiesta hello evidenza abbiamo un utente connesso.</span><span class="sxs-lookup"><span data-stu-id="acdaf-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="acdaf-187">Creare hello `/views/account.ejs` visualizzazione nella directory radice hello in modo che è possibile visualizzare informazioni aggiuntive che `passport-azuread` è inserito nella richiesta utente hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="acdaf-188">Ora viene aggiunto un layout per modificare l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="acdaf-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="acdaf-189">Creare hello ' / directory radice di visualizzazione degli views/layout.ejs in hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="acdaf-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acdaf-190">Next steps</span></span>
<span data-ttu-id="acdaf-191">Per finire, compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="acdaf-191">Finally, build and run your app.</span></span> <span data-ttu-id="acdaf-192">Eseguire `node app.js`, quindi andare troppo`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="acdaf-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="acdaf-193">Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione e notare come identità dell'utente hello si riflette nell'elenco /account hello.</span><span class="sxs-lookup"><span data-stu-id="acdaf-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="acdaf-194">È ora disponibile un'app Web protetta con protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="acdaf-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="acdaf-195">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="acdaf-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="acdaf-196">In alternativa, è possibile eseguire la clonazione da GitHub:</span><span class="sxs-lookup"><span data-stu-id="acdaf-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="acdaf-197">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="acdaf-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="acdaf-198">È possibile tootry:</span><span class="sxs-lookup"><span data-stu-id="acdaf-198">You might want tootry:</span></span>

[<span data-ttu-id="acdaf-199">Proteggere un'API Web con Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdaf-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
