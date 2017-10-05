---
title: Introduzione alle procedure di accesso e disconnessione di Azure AD con Node.js | Microsoft Docs
description: Informazioni sulla compilazione di un'app Web Express MVC di Node.js che si integra con Azure AD per l'accesso.
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="a2328-103">Accesso e disconnessione all'app Web di Node. js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2328-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="a2328-104">Passport viene usato per:</span><span class="sxs-lookup"><span data-stu-id="a2328-104">Here we use Passport to:</span></span>

* <span data-ttu-id="a2328-105">Far accedere l'utente all'app con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2328-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="a2328-106">Visualizzare informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-106">Display information about the user.</span></span>
* <span data-ttu-id="a2328-107">Disconnettere l'utente dall'app.</span><span class="sxs-lookup"><span data-stu-id="a2328-107">Sign the user out of the app.</span></span>

<span data-ttu-id="a2328-108">Passport è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2328-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="a2328-109">Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o restify.</span><span class="sxs-lookup"><span data-stu-id="a2328-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="a2328-110">Una gamma completa di strategie supporta l'autenticazione mediante nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="a2328-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="a2328-111">È stata sviluppata una strategia per Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2328-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="a2328-112">Dopo l'installazione di questo modulo, verrà aggiunto il plug-in `passport-azure-ad` di Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2328-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="a2328-113">Per effettuare questa operazione, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2328-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="a2328-114">Registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="a2328-114">Register an app.</span></span>
2. <span data-ttu-id="a2328-115">Configurare l'app in modo che usi la strategia `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a2328-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="a2328-116">Usare Passport per inviare le richieste di accesso e disconnessione ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2328-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="a2328-117">Stampare dati relativi all'utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-117">Print data about the user.</span></span>

<span data-ttu-id="a2328-118">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="a2328-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="a2328-119">Per seguire la procedura, è possibile [scaricare la struttura dell'app come file .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="a2328-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="a2328-120">Al termine dell'esercitazione, verrà fornita anche l'applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="a2328-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="a2328-121">Passaggio 1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="a2328-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="a2328-122">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2328-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a2328-123">Dal menu nella parte superiore della pagina selezionare il proprio account.</span><span class="sxs-lookup"><span data-stu-id="a2328-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="a2328-124">Nell'elenco **Directory** scegliere il tenant di Active Directory in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2328-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="a2328-125">Selezionare **More services** (Altri servizi) nel menu a sinistra della schermata, quindi scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a2328-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="a2328-126">Selezionare **Registrazioni per l'app**, quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a2328-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="a2328-127">Seguire le istruzioni e creare una nuova **applicazione Web** e/o **API Web**.</span><span class="sxs-lookup"><span data-stu-id="a2328-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="a2328-128">Il **nome** dell'applicazione descrive l'applicazione agli utenti.</span><span class="sxs-lookup"><span data-stu-id="a2328-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="a2328-129">L' **URL accesso** è l'URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="a2328-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="a2328-130">Il valore predefinito della struttura è `http://localhost:3000/auth/openid/return`\`.</span><span class="sxs-lookup"><span data-stu-id="a2328-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="a2328-131">Dopo la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="a2328-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="a2328-132">Poiché questo valore sarà necessario nelle sezioni successive, è necessario copiarlo dalla pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2328-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="a2328-133">Dalla pagina **Impostazioni** -> **Proprietà** dell'applicazione aggiornare l'URI dell'ID app.</span><span class="sxs-lookup"><span data-stu-id="a2328-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="a2328-134">L' **URI ID app** è un identificatore univoco dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2328-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="a2328-135">La convenzione consiste nell'usare il formato `https://<tenant-domain>/<app-name>`, ad esempio: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="a2328-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="a2328-136">Passaggio 2: Aggiungere prerequisiti alla directory</span><span class="sxs-lookup"><span data-stu-id="a2328-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="a2328-137">Dalla riga di comando passare dalle directory alla cartella radice, se non è già stato fatto, ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2328-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="a2328-138">Inoltre, è necessario `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="a2328-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="a2328-139">Verranno installate le librerie da cui dipende `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a2328-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="a2328-140">Passaggio 3: Configurare l'app in modo che usi la strategia passport-node-js</span><span class="sxs-lookup"><span data-stu-id="a2328-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="a2328-141">In questo caso, verrà configurato Express in modo che usi il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a2328-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="a2328-142">Passport verrà usato, tra le altre cose, per inviare richieste di accesso e disconnessione, gestire la sessione dell'utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="a2328-143">Per iniziare, aprire il file `config.js` nella radice del progetto e immettere i valori di configurazione dell'app nella sezione `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="a2328-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="a2328-144">`clientID` rappresenta l'**ID applicazione** assegnato all'app nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a2328-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="a2328-145">`returnURL` rappresenta l'**URI di reindirizzamento** immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="a2328-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="a2328-146">`clientSecret` rappresenta il segreto generato nel portale.</span><span class="sxs-lookup"><span data-stu-id="a2328-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="a2328-147">In seguito, aprire il file `app.js` nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="a2328-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="a2328-148">Quindi, aggiungere la chiamata seguente per richiamare la strategia `OIDCStrategy` fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="a2328-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="a2328-149">Successivamente, usare la strategia a cui è stato fatto riferimento per gestire le richieste di accesso.</span><span class="sxs-lookup"><span data-stu-id="a2328-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="a2328-150">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via) seguite dagli scrittori della strategia.</span><span class="sxs-lookup"><span data-stu-id="a2328-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="a2328-151">Osservando la strategia, è possibile notare che a quest'ultima è stata passata una funzione con parametri token e done.</span><span class="sxs-lookup"><span data-stu-id="a2328-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="a2328-152">La strategia torna indietro dopo eseguito il suo lavoro.</span><span class="sxs-lookup"><span data-stu-id="a2328-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="a2328-153">A questo punto è necessario archiviare l'utente e accantonare il token in modo che non sia necessario richiederlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a2328-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="a2328-154">Il codice precedente accetta qualsiasi utente che esegue l'autenticazione al server.</span><span class="sxs-lookup"><span data-stu-id="a2328-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="a2328-155">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="a2328-155">This is known as auto-registration.</span></span> <span data-ttu-id="a2328-156">Si consiglia di non consentire agli utenti di eseguire l'autenticazione per un server di produzione senza prima prevedere un processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a2328-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="a2328-157">Questo è il criterio usato in genere per le app consumer, che consentono di eseguire la registrazione con Facebook ma poi chiedono di immettere informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a2328-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="a2328-158">Se non si trattasse di un'applicazione di esempio, sarebbe stato possibile estrarre l'indirizzo e-mail dell'utente dall'oggetto token restituito e chiedere all'utente di immettere le informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a2328-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="a2328-159">Poiché si tratta di un server di test, le informazioni vengono aggiunte al database in memoria.</span><span class="sxs-lookup"><span data-stu-id="a2328-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="a2328-160">Successivamente, aggiungere i metodi che consentiranno di tenere traccia degli utenti connessi come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="a2328-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="a2328-161">Questi metodi includono la serializzazione e deserializzazione delle informazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="a2328-162">Quindi aggiungere il codice per caricare il motore Express.</span><span class="sxs-lookup"><span data-stu-id="a2328-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="a2328-163">Qui usiamo i modelli /views e /routes predefiniti forniti da Express.</span><span class="sxs-lookup"><span data-stu-id="a2328-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="a2328-164">Infine aggiungere le route che trasferiscono le richieste di accesso effettive al motore `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="a2328-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="a2328-165">Passaggio 4: Usare Passport per inviare le richieste di accesso e disconnessione ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2328-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="a2328-166">L'app ora è configurata correttamente per comunicare con l'endpoint mediante il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a2328-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="a2328-167">`passport-azure-ad` ha gestito tutti i dettagli relativi alla creazione dei messaggi di autenticazione, alla convalida dei token da Azure AD e alla gestione delle sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="a2328-168">A questo punto è sufficiente offrire agli utenti un modo per accedere e disconnettersi e per raccogliere informazioni aggiuntive sugli utenti connessi.</span><span class="sxs-lookup"><span data-stu-id="a2328-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="a2328-169">Aggiungere prima di tutto i metodi predefinito, di accesso, account e disconnessione al file `app.js`:</span><span class="sxs-lookup"><span data-stu-id="a2328-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="a2328-170">Esaminare nel dettaglio questi aspetti:</span><span class="sxs-lookup"><span data-stu-id="a2328-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="a2328-171">Il percorso `/` reindirizza alla vista index.ejs passando l'utente nella richiesta (se presente).</span><span class="sxs-lookup"><span data-stu-id="a2328-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="a2328-172">Il percorso `/account` prima di tutto *verifica che l'autenticazione sia stata eseguita* (l'implementazione nell'esempio di seguito), quindi passa l'utente nella richiesta in modo da ottenere informazioni aggiuntive su quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="a2328-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="a2328-173">Il percorso `/login` richiama l'autenticatore azuread-openidconnect da `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="a2328-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="a2328-174">Se l'operazione ha esito negativo, il percorso reindirizza di nuovo l'utente a /login.</span><span class="sxs-lookup"><span data-stu-id="a2328-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="a2328-175">Il percorso `/logout` chiama logout.ejs (e il percorso), consentendo di cancellare i cookie e riportando quindi l'utente a index.ejs.</span><span class="sxs-lookup"><span data-stu-id="a2328-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="a2328-176">Per l'ultima parte di `app.js`, aggiungere il metodo **EnsureAuthenticated** usato in `/account`, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a2328-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="a2328-177">Infine, creare il server stesso in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="a2328-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="a2328-178">Passaggio 5: Creare le viste e i percorsi in Express per visualizzare l'utente nel sito Web</span><span class="sxs-lookup"><span data-stu-id="a2328-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="a2328-179">Ora il file `app.js` è completo.</span><span class="sxs-lookup"><span data-stu-id="a2328-179">Now `app.js` is complete.</span></span> <span data-ttu-id="a2328-180">È sufficiente aggiungere i percorsi e le viste che mostrano all'utente le informazioni ottenute e gestire i percorsi `/logout` e `/login` creati.</span><span class="sxs-lookup"><span data-stu-id="a2328-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="a2328-181">Creare la route `/routes/index.js` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="a2328-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="a2328-182">Creare la route `/routes/user.js` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="a2328-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="a2328-183">Queste passeranno la richiesta alle viste, incluso l'utente se presente.</span><span class="sxs-lookup"><span data-stu-id="a2328-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="a2328-184">Creare la vista `/views/index.ejs` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="a2328-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="a2328-185">Si tratta di una pagina semplice che chiama i metodi di accesso e disconnessione e consente di ottenere informazioni sull'account.</span><span class="sxs-lookup"><span data-stu-id="a2328-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="a2328-186">Si noti che è possibile usare il parametro condizionale `if (!user)` in quanto l'utente passato nella richiesta dimostra che c'è un utente che ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a2328-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="a2328-187">Creare la vista `/views/account.ejs` nella directory radice affinché sia possibile visualizzare informazioni aggiuntive che `passport-azuread` ha inserito nella richiesta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2328-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="a2328-188">Ora viene aggiunto un layout per modificare l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="a2328-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="a2328-189">Creare la vista '/views/layout.ejs' nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="a2328-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="a2328-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2328-190">Next steps</span></span>
<span data-ttu-id="a2328-191">Per finire, compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="a2328-191">Finally, build and run your app.</span></span> <span data-ttu-id="a2328-192">Eseguire `node app.js`, quindi passare a `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="a2328-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="a2328-193">Accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione e osservare come l'identità dell'utente è indicata nell'elenco /account.</span><span class="sxs-lookup"><span data-stu-id="a2328-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="a2328-194">È ora disponibile un'app Web protetta con protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a2328-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="a2328-195">Come riferimento viene fornito l'esempio completato, senza i valori di configurazione, [come file con estensione zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a2328-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="a2328-196">In alternativa, è possibile eseguire la clonazione da GitHub:</span><span class="sxs-lookup"><span data-stu-id="a2328-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="a2328-197">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="a2328-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="a2328-198">È consigliabile provare:</span><span class="sxs-lookup"><span data-stu-id="a2328-198">You might want to try:</span></span>

[<span data-ttu-id="a2328-199">Proteggere un'API Web con Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2328-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
