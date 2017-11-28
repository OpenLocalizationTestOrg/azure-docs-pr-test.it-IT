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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="ceb54-103">Azure Active Directory B2C: Aggiungere app web di accesso tooa Node.js</span><span class="sxs-lookup"><span data-stu-id="ceb54-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="ceb54-104">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="ceb54-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="ceb54-105">Passport, estremamente flessibile e modulare, può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="ceb54-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="ceb54-106">Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ceb54-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="ceb54-107">È stata sviluppata una strategia per Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ceb54-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ceb54-108">Verranno installate in questo modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="ceb54-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="ceb54-109">toodo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="ceb54-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="ceb54-110">Registrare un'applicazione usando Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ceb54-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="ceb54-111">Impostare il hello toouse app `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="ceb54-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="ceb54-112">Usare Passport tooissue Accedi e richieste di disconnessione tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ceb54-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="ceb54-113">Stampare i dati utente.</span><span class="sxs-lookup"><span data-stu-id="ceb54-113">Print user data.</span></span>

<span data-ttu-id="ceb54-114">Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="ceb54-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="ceb54-115">toofollow lungo, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="ceb54-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="ceb54-116">È anche possibile clonare scheletro hello:</span><span class="sxs-lookup"><span data-stu-id="ceb54-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="ceb54-117">un'applicazione Hello completato viene fornita alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ceb54-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ceb54-118">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ceb54-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="ceb54-119">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="ceb54-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="ceb54-120">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="ceb54-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ceb54-121">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="ceb54-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ceb54-122">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="ceb54-122">Create an application</span></span>

<span data-ttu-id="ceb54-123">Successivamente, è necessario toocreate un'app nel servizio directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ceb54-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="ceb54-124">Vengono riportate informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="ceb54-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="ceb54-125">Entrambi hello app client e l'API web sarà rappresentato da un singolo **ID applicazione**, poiché comprendono una sola app logica.</span><span class="sxs-lookup"><span data-stu-id="ceb54-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="ceb54-126">toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ceb54-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ceb54-127">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="ceb54-127">Be sure to:</span></span>

- <span data-ttu-id="ceb54-128">Includere un **app web**/**web API** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="ceb54-129">Immettere `http://localhost:3000/auth/openid/return` come **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="ceb54-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="ceb54-130">È l'URL predefinito hello per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="ceb54-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="ceb54-131">Creare un **segreto applicazione** per l'applicazione e prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="ceb54-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="ceb54-132">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="ceb54-132">You will need it later.</span></span> <span data-ttu-id="ceb54-133">Si noti che questo valore deve toobe [XML sottoposto a escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) prima di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="ceb54-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="ceb54-134">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="ceb54-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="ceb54-135">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="ceb54-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ceb54-136">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="ceb54-136">Create your policies</span></span>

<span data-ttu-id="ceb54-137">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="ceb54-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ceb54-138">Questa app contiene tre esperienze di identità: iscrizione, accesso e accesso con Facebook.</span><span class="sxs-lookup"><span data-stu-id="ceb54-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="ceb54-139">È necessario toocreate questo criterio di ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="ceb54-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="ceb54-140">Durante la creazione dei tre criteri assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="ceb54-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="ceb54-141">Scegliere hello **nome visualizzato** e altri attributi per l'abbonamento nel criterio di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="ceb54-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="ceb54-142">Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="ceb54-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="ceb54-143">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="ceb54-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="ceb54-144">Hello copia **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="ceb54-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="ceb54-145">Devono contenere il prefisso hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="ceb54-146">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ceb54-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ceb54-147">Dopo aver creato i tre criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="ceb54-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="ceb54-148">Si noti che questo articolo non viene illustrata la modalità criteri hello toouse appena creato.</span><span class="sxs-lookup"><span data-stu-id="ceb54-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="ceb54-149">toolearn sul funzionamento dei criteri in Azure Active Directory B2C, iniziare con hello [.NET web app esercitazione introduttiva](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ceb54-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="ceb54-150">Aggiunta di prerequisiti tooyour directory</span><span class="sxs-lookup"><span data-stu-id="ceb54-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="ceb54-151">Dalla riga di comando hello, Modifica cartella radice tooyour di directory, se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="ceb54-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="ceb54-152">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="ceb54-152">Run hello following commands:</span></span>

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

<span data-ttu-id="ceb54-153">Inoltre, abbiamo utilizzato `passport-azure-ad` per l'anteprima scheletro hello di hello Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="ceb54-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="ceb54-154">Verranno installate le librerie di hello che `passport-azure-ad` dipende.</span><span class="sxs-lookup"><span data-stu-id="ceb54-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="ceb54-155">Impostare il hello toouse app strategia Passport Node.js</span><span class="sxs-lookup"><span data-stu-id="ceb54-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="ceb54-156">Configurare hello toouse di hello Express middleware OpenID Connect di protocollo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ceb54-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="ceb54-157">Passport verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire le sessioni utente e ottenere informazioni sugli utenti, tra le altre azioni.</span><span class="sxs-lookup"><span data-stu-id="ceb54-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="ceb54-158">Aprire hello `config.js` file nella directory radice del progetto hello hello e immettere i valori di configurazione dell'applicazione hello `exports.creds` sezione.</span><span class="sxs-lookup"><span data-stu-id="ceb54-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="ceb54-159">`clientID`: hello **ID applicazione** assegnato tooyour app nel portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="ceb54-160">`returnURL`: hello **URI di reindirizzamento** immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="ceb54-161">`tenantName`: nome del tenant hello dell'app, ad esempio, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="ceb54-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="ceb54-162">Aprire hello `app.js` file nella directory radice del progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="ceb54-163">Aggiungere hello seguente chiamata tooinvoke hello `OIDCStrategy` strategia che prevede `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="ceb54-164">Utilizzare la strategia di hello è stato fatto riferimento solo le richieste di accesso toohandle.</span><span class="sxs-lookup"><span data-stu-id="ceb54-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

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
<span data-ttu-id="ceb54-165">Passport usa un modello simile per tutte le strategie (inclusi Twitter e Facebook).</span><span class="sxs-lookup"><span data-stu-id="ceb54-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="ceb54-166">Tutti i writer strategia rispettare toothis modello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="ceb54-167">Quando si esamina la strategia di hello, è possibile vedere che si passa un `function()` che dispone di un token e un `done` come parametri hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="ceb54-168">strategia di Hello torna tooyou dopo che ha eseguito tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="ceb54-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="ceb54-169">Archivio utente hello e accantonare token hello in modo che non sia necessario tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="ceb54-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="ceb54-170">Hello precedente il codice in tutti gli utenti che esegue l'autenticazione server hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="ceb54-171">Questa operazione è la registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="ceb54-171">This is autoregistration.</span></span> <span data-ttu-id="ceb54-172">Quando si utilizzano server di produzione, non si desidera toolet gli utenti a meno che non che sono state registrate tramite un processo di registrazione che è stato impostato.</span><span class="sxs-lookup"><span data-stu-id="ceb54-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="ceb54-173">Questo modello è frequente nelle app consumer</span><span class="sxs-lookup"><span data-stu-id="ceb54-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="ceb54-174">Che consentono di tooregister con Facebook, ma quindi vengono chiesto toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ceb54-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="ceb54-175">Se l'applicazione non è un esempio, è stato possibile estrarre un indirizzo di posta elettronica da oggetto hello token restituito e quindi chiedere hello utente toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ceb54-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="ceb54-176">Poiché si tratta di un server di prova, è sufficiente aggiungere i database in memoria toohello di utenti.</span><span class="sxs-lookup"><span data-stu-id="ceb54-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="ceb54-177">Aggiungere metodi hello che consentono di tenere traccia di tookeep di utenti che hanno effettuato l'accesso, come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="ceb54-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="ceb54-178">Questa operazione include la serializzazione e la deserializzazione delle informazioni dell'utente:</span><span class="sxs-lookup"><span data-stu-id="ceb54-178">This includes serializing and deserializing user information:</span></span>

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

<span data-ttu-id="ceb54-179">Aggiungere il motore Express hello di hello code tooload.</span><span class="sxs-lookup"><span data-stu-id="ceb54-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="ceb54-180">Nella seguente hello, è possibile visualizzare l'utilizzo predefinito di hello `/views` e `/routes` modello che fornisce Express.</span><span class="sxs-lookup"><span data-stu-id="ceb54-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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

<span data-ttu-id="ceb54-181">Aggiungere hello `POST` route consegnare hello toohello le richieste di accesso effettiva `passport-azure-ad` motore:</span><span class="sxs-lookup"><span data-stu-id="ceb54-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="ceb54-182">Usare Passport tooissue Accedi e richieste di disconnessione tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="ceb54-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="ceb54-183">L'app è configurato correttamente toocommunicate con endpoint v 2.0 hello tramite protocollo di autenticazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="ceb54-184">`passport-azure-ad`ha preso in considerazione dei dettagli di hello relativi alla creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione della sessione utente.</span><span class="sxs-lookup"><span data-stu-id="ceb54-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="ceb54-185">Che rimane è toogive agli utenti un modo toosign in e accedere out e toogather ulteriori informazioni sugli utenti che hanno effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ceb54-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="ceb54-186">Aggiungere innanzitutto predefinito hello, accesso, account e metodi disconnessione tooyour `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="ceb54-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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

<span data-ttu-id="ceb54-187">tooreview questi metodi in modo dettagliato:</span><span class="sxs-lookup"><span data-stu-id="ceb54-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="ceb54-188">Hello `/` route reindirizza toohello `index.ejs` vista passando utente hello nella richiesta di hello (se presente).</span><span class="sxs-lookup"><span data-stu-id="ceb54-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="ceb54-189">Hello `/account` route verifica innanzitutto che sono autenticati (hello implementazione di questa situazione sotto).</span><span class="sxs-lookup"><span data-stu-id="ceb54-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="ceb54-190">Passa quindi utente hello nella richiesta di hello in modo che sia possibile ottenere ulteriori informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="ceb54-191">Hello `/login` route chiamate hello `azuread-openidconnect` autenticatore da `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="ceb54-192">Se non viene completato, route hello utente viene reindirizzato hello nuovamente troppo`/login`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="ceb54-193">`/logout` chiama semplicemente `logout.ejs` e la rispettiva route.</span><span class="sxs-lookup"><span data-stu-id="ceb54-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="ceb54-194">Ciò consente di cancellare i cookie e quindi restituisce hello utente nuovamente troppo`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="ceb54-195">Per l'ultima parte di hello del `app.js`, aggiungere hello `EnsureAuthenticated` metodo utilizzato in hello `/account` route.</span><span class="sxs-lookup"><span data-stu-id="ceb54-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

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

<span data-ttu-id="ceb54-196">Infine, creare server hello in `app.js`.</span><span class="sxs-lookup"><span data-stu-id="ceb54-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="ceb54-197">Creare visualizzazioni hello e instrada in Express toocall i criteri</span><span class="sxs-lookup"><span data-stu-id="ceb54-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="ceb54-198">`app.js` è stato completato.</span><span class="sxs-lookup"><span data-stu-id="ceb54-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="ceb54-199">È sufficiente route hello tooadd e visualizzazioni che consentono di criteri di accesso ed effettuare l'iscrizione hello toocall.</span><span class="sxs-lookup"><span data-stu-id="ceb54-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="ceb54-200">Questi anche gestire hello `/logout` e `/login` route creata.</span><span class="sxs-lookup"><span data-stu-id="ceb54-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="ceb54-201">Creare hello `/routes/index.js` route nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="ceb54-202">Creare hello `/routes/user.js` route nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="ceb54-203">Queste route semplice passano dalle visualizzazioni tooyour richieste.</span><span class="sxs-lookup"><span data-stu-id="ceb54-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="ceb54-204">Includono utente hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="ceb54-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="ceb54-205">Creare hello `/views/index.ejs` visualizzazione nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="ceb54-206">Si tratta di una semplice pagina che chiama i criteri per l'accesso e la disconnessione. È possibile inoltre utilizzare è toograb informazioni dell'account.</span><span class="sxs-lookup"><span data-stu-id="ceb54-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="ceb54-207">Si noti che è possibile utilizzare hello condizionale `if (!user)` come utente hello viene passata nella richiesta hello tooprovide evidenza utente hello è connesso.</span><span class="sxs-lookup"><span data-stu-id="ceb54-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="ceb54-208">Creare hello `/views/account.ejs` visualizzazione nella directory radice hello in modo che è possibile visualizzare informazioni aggiuntive che `passport-azure-ad` inserito nella richiesta utente hello.</span><span class="sxs-lookup"><span data-stu-id="ceb54-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="ceb54-209">Ora è possibile compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="ceb54-209">You can now build and run your app.</span></span>

<span data-ttu-id="ceb54-210">Eseguire `node app.js` e passare troppo`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="ceb54-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="ceb54-211">Iscriversi o accedere nell'app toohello tramite e-mail o Facebook.</span><span class="sxs-lookup"><span data-stu-id="ceb54-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="ceb54-212">Disconnettersi e accedere nuovamente come un utente diverso.</span><span class="sxs-lookup"><span data-stu-id="ceb54-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="ceb54-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ceb54-213">Next steps</span></span>

<span data-ttu-id="ceb54-214">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ceb54-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="ceb54-215">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="ceb54-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="ceb54-216">È possibile procedere con toomore argomenti avanzati.</span><span class="sxs-lookup"><span data-stu-id="ceb54-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="ceb54-217">È possibile provare a:</span><span class="sxs-lookup"><span data-stu-id="ceb54-217">You might try:</span></span>

[<span data-ttu-id="ceb54-218">Proteggere un'API web utilizzando il modello di hello B2C in Node.js</span><span class="sxs-lookup"><span data-stu-id="ceb54-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
