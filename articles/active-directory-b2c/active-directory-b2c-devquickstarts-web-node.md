---
title: Aggiungere l'accesso a un'app Web Node.js per Azure AD B2C | Documentazione Microsoft
description: Come compilare un'app Web Node.js che esegua l'accesso degli utenti usando un tenant B2C.
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
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="0332d-103">Azure AD B2C: aggiungere l'accesso a un'app Web Node.js</span><span class="sxs-lookup"><span data-stu-id="0332d-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="0332d-104">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="0332d-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="0332d-105">Passport, estremamente flessibile e modulare, può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="0332d-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="0332d-106">Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="0332d-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="0332d-107">È stata sviluppata una strategia per Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0332d-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0332d-108">Dopo l'installazione di questo modulo, aggiungere il plug-in `passport-azure-ad` di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0332d-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="0332d-109">A questo scopo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0332d-109">To do this, you need to:</span></span>

1. <span data-ttu-id="0332d-110">Registrare un'applicazione usando Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0332d-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="0332d-111">Configurare l'app per usare il plug-in `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="0332d-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="0332d-112">Usare Passport per inviare le richieste di accesso e disconnessione ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0332d-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="0332d-113">Stampare i dati utente.</span><span class="sxs-lookup"><span data-stu-id="0332d-113">Print user data.</span></span>

<span data-ttu-id="0332d-114">Il codice per questa esercitazione è [disponibile in GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="0332d-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="0332d-115">Per seguire la procedura, è possibile [scaricare la struttura dell'app come file ZIP](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="0332d-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="0332d-116">È anche possibile clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="0332d-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="0332d-117">Al termine dell'esercitazione, verrà fornita l'applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="0332d-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="0332d-118">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0332d-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="0332d-119">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="0332d-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="0332d-120">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="0332d-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="0332d-121">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="0332d-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="0332d-122">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="0332d-122">Create an application</span></span>

<span data-ttu-id="0332d-123">Successivamente, è necessario creare un'app nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0332d-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="0332d-124">In questo modo Azure AD acquisisce le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="0332d-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="0332d-125">Sia l'app client che l'API Web saranno rappresentate da un unico **ID applicazione**, perché includono un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0332d-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="0332d-126">Per creare un'app, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="0332d-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="0332d-127">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="0332d-127">Be sure to:</span></span>

- <span data-ttu-id="0332d-128">Includere un'**app Web**/**API Web** nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0332d-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="0332d-129">Immettere `http://localhost:3000/auth/openid/return` come **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="0332d-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="0332d-130">Si tratta dell'URL predefinito per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="0332d-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="0332d-131">Creare un **segreto applicazione** per l'applicazione e prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="0332d-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="0332d-132">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="0332d-132">You will need it later.</span></span> <span data-ttu-id="0332d-133">Si noti che prima di usare questo valore è necessario [inserire un carattere di escape XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) .</span><span class="sxs-lookup"><span data-stu-id="0332d-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="0332d-134">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="0332d-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="0332d-135">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="0332d-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="0332d-136">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="0332d-136">Create your policies</span></span>

<span data-ttu-id="0332d-137">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="0332d-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="0332d-138">Questa app contiene tre esperienze di identità: iscrizione, accesso e accesso con Facebook.</span><span class="sxs-lookup"><span data-stu-id="0332d-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="0332d-139">È necessario creare i criteri per ogni tipo, come descritto nell' [articolo di riferimento per i criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="0332d-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="0332d-140">Durante la creazione dei tre criteri assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="0332d-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="0332d-141">Scegliere **Nome visualizzato** e altri attributi nei criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="0332d-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="0332d-142">Scegliere le attestazioni dell'applicazione **Nome visualizzato** e **ID oggetto** in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="0332d-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="0332d-143">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="0332d-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="0332d-144">Copiare il **Nome** di ogni criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="0332d-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="0332d-145">Dovrebbero mostrare il prefisso `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="0332d-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="0332d-146">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="0332d-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="0332d-147">Dopo aver creato i tre criteri, è possibile passare alla compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0332d-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="0332d-148">Si noti che questo articolo non illustra come usare i criteri appena creati.</span><span class="sxs-lookup"><span data-stu-id="0332d-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="0332d-149">Per informazioni sul funzionamento dei criteri in Azure AD B2C, iniziare dall' [esercitazione introduttiva per la compilazione di un'app Web .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0332d-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="0332d-150">Aggiungere prerequisiti alla directory</span><span class="sxs-lookup"><span data-stu-id="0332d-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="0332d-151">Dalla riga di comando passare alla cartella radice, se necessario.</span><span class="sxs-lookup"><span data-stu-id="0332d-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="0332d-152">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0332d-152">Run the following commands:</span></span>

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

<span data-ttu-id="0332d-153">È stato anche usato `passport-azure-ad` per l'anteprima nella struttura di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="0332d-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="0332d-154">Verranno installate le librerie da cui dipende `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="0332d-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="0332d-155">Configurare l'app per l'uso della strategia Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="0332d-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="0332d-156">Configurare il middleware Express per l'uso del protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0332d-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="0332d-157">Passport verrà usato, tra le altre azioni, per inviare le richieste di accesso e disconnessione, gestire le sessioni degli utenti e ottenere informazioni sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="0332d-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="0332d-158">Aprire il file `config.js` nella radice del progetto e immettere i valori di configurazione dell'app nella sezione `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="0332d-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="0332d-159">`clientID`: **ID applicazione** assegnato all'app nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="0332d-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="0332d-160">`returnURL`: **URI di reindirizzamento** immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="0332d-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="0332d-161">`tenantName`: nome del tenant dell'app, ad esempio, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="0332d-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="0332d-162">Aprire il file `app.js` nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="0332d-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="0332d-163">Aggiungere la chiamata seguente per richiamare la strategia `OIDCStrategy` fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="0332d-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="0332d-164">Usare la strategia a cui si è appena fatto riferimento per gestire le richieste di accesso.</span><span class="sxs-lookup"><span data-stu-id="0332d-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
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
<span data-ttu-id="0332d-165">Passport usa un modello simile per tutte le strategie (inclusi Twitter e Facebook).</span><span class="sxs-lookup"><span data-stu-id="0332d-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="0332d-166">Tutti i writer di strategie rispettano questo modello.</span><span class="sxs-lookup"><span data-stu-id="0332d-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="0332d-167">Quando si esamina la strategia, è possibile osservare che le si passa un oggetto `function()` che ha come parametri un token e un oggetto `done`.</span><span class="sxs-lookup"><span data-stu-id="0332d-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="0332d-168">La strategia risponde dopo avere eseguito tutte le relative operazioni.</span><span class="sxs-lookup"><span data-stu-id="0332d-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="0332d-169">Archiviare l'utente e accantonare il token per non doverlo richiedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="0332d-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="0332d-170">Il codice precedente accetta tutti gli utenti autenticati dal server.</span><span class="sxs-lookup"><span data-stu-id="0332d-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="0332d-171">Questa operazione è la registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="0332d-171">This is autoregistration.</span></span> <span data-ttu-id="0332d-172">Quando si usano server di produzione, si consente l'accesso solo agli utenti che abbiano eseguito un processo di registrazione configurato.</span><span class="sxs-lookup"><span data-stu-id="0332d-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="0332d-173">Questo modello è frequente nelle app consumer</span><span class="sxs-lookup"><span data-stu-id="0332d-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="0332d-174">che consentono di eseguire la registrazione usando Facebook, ma che chiedono anche di inserire altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="0332d-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="0332d-175">Se non si trattasse di un'applicazione di esempio, si estrarrebbe un indirizzo di posta elettronica dall'oggetto token restituito e si chiederebbe all'utente di immettere informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="0332d-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="0332d-176">Trattandosi di un server di test, è sufficiente aggiungere gli utenti al database in memoria.</span><span class="sxs-lookup"><span data-stu-id="0332d-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="0332d-177">Aggiungere i metodi che consentono di tenere traccia degli utenti che hanno eseguito l'accesso, come richiesto da Passport.</span><span class="sxs-lookup"><span data-stu-id="0332d-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="0332d-178">Questa operazione include la serializzazione e la deserializzazione delle informazioni dell'utente:</span><span class="sxs-lookup"><span data-stu-id="0332d-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
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

<span data-ttu-id="0332d-179">Aggiungere il codice per caricare il motore di Express.</span><span class="sxs-lookup"><span data-stu-id="0332d-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="0332d-180">Nel codice seguente è possibile notare che vengono usati i modelli `/views` e `/routes` predefiniti forniti da Express.</span><span class="sxs-lookup"><span data-stu-id="0332d-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

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
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="0332d-181">Aggiungere le route `POST` che trasferiscono le richieste di accesso effettive al motore `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="0332d-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="0332d-182">Usare Passport per inviare le richieste di accesso e disconnessione ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="0332d-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="0332d-183">L'app ora è configurata correttamente per comunicare con l'endpoint 2.0 mediante il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0332d-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="0332d-184">`passport-azure-ad` ha gestito i dettagli relativi alla creazione dei messaggi di autenticazione, alla convalida dei token da Azure AD e alla gestione della sessione utente.</span><span class="sxs-lookup"><span data-stu-id="0332d-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="0332d-185">A questo punto, è sufficiente offrire agli utenti un modo per accedere e disconnettersi e per raccogliere informazioni aggiuntive sugli utenti connessi.</span><span class="sxs-lookup"><span data-stu-id="0332d-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="0332d-186">Aggiungere prima di tutto i metodi predefinito, di accesso, account e disconnessione al file `app.js`:</span><span class="sxs-lookup"><span data-stu-id="0332d-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

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
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="0332d-187">Per esaminare questi metodi in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="0332d-187">To review these methods in detail:</span></span>
- <span data-ttu-id="0332d-188">La route `/` viene reindirizzata alla visualizzazione `index.ejs` passando l'utente nella richiesta (se presente).</span><span class="sxs-lookup"><span data-stu-id="0332d-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="0332d-189">La route `/account` verifica prima di tutto che l'utente sia autenticato. L'implementazione per questo passaggio è disponibile più avanti.</span><span class="sxs-lookup"><span data-stu-id="0332d-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="0332d-190">quindi passa l'utente nella richiesta per poter ottenere altre informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="0332d-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="0332d-191">La route `/login` chiama l'autenticatore `azuread-openidconnect` da `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="0332d-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="0332d-192">Se l'esito è negativo, la route reindirizza di nuovo l'utente a `/login`.</span><span class="sxs-lookup"><span data-stu-id="0332d-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="0332d-193">`/logout` chiama semplicemente `logout.ejs` e la rispettiva route.</span><span class="sxs-lookup"><span data-stu-id="0332d-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="0332d-194">I cookie vengono cancellati e quindi l'utente torna a `index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="0332d-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="0332d-195">Per l'ultima parte di `app.js`, aggiungere il metodo `EnsureAuthenticated` usato nella route `/account`.</span><span class="sxs-lookup"><span data-stu-id="0332d-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="0332d-196">Creare infine il server stesso in `app.js`.</span><span class="sxs-lookup"><span data-stu-id="0332d-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="0332d-197">Creare le visualizzazioni e le route in Express per chiamare i criteri</span><span class="sxs-lookup"><span data-stu-id="0332d-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="0332d-198">`app.js` è stato completato.</span><span class="sxs-lookup"><span data-stu-id="0332d-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="0332d-199">È sufficiente aggiungere le route e le visualizzazioni che consentono di chiamare i criteri di accesso e di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="0332d-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="0332d-200">In questo modo vengono gestite anche le route `/logout` e `/login` create.</span><span class="sxs-lookup"><span data-stu-id="0332d-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="0332d-201">Creare la route `/routes/index.js` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="0332d-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="0332d-202">Creare la route `/routes/user.js` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="0332d-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="0332d-203">Queste semplici route passano le richieste alle visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="0332d-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="0332d-204">Includono l'utente, se è presente.</span><span class="sxs-lookup"><span data-stu-id="0332d-204">They include the user, if one is present.</span></span>

<span data-ttu-id="0332d-205">Creare la vista `/views/index.ejs` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="0332d-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="0332d-206">Si tratta di una semplice pagina che chiama i criteri per l'accesso e la disconnessione.</span><span class="sxs-lookup"><span data-stu-id="0332d-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="0332d-207">È possibile usarla anche per ottenere informazioni account.</span><span class="sxs-lookup"><span data-stu-id="0332d-207">You can also use it to grab account information.</span></span> <span data-ttu-id="0332d-208">Si noti che è possibile usare `if (!user)` condizionale quando l'utente viene passato nella richiesta per fornire la prova che l'utente ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="0332d-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

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

<span data-ttu-id="0332d-209">Creare la visualizzazione `/views/account.ejs` nella directory radice per poter visualizzare informazioni aggiuntive che `passport-azure-ad` ha inserito nella richiesta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0332d-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

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

<span data-ttu-id="0332d-210">Ora è possibile compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="0332d-210">You can now build and run your app.</span></span>

<span data-ttu-id="0332d-211">Eseguire `node app.js` e passare a `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="0332d-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="0332d-212">Iscriversi o accedere all'app usando la posta elettronica o Facebook.</span><span class="sxs-lookup"><span data-stu-id="0332d-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="0332d-213">Disconnettersi e accedere nuovamente come un utente diverso.</span><span class="sxs-lookup"><span data-stu-id="0332d-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="0332d-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0332d-214">Next steps</span></span>

<span data-ttu-id="0332d-215">Come riferimento viene fornito l'esempio completato, senza i valori di configurazione, [come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0332d-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="0332d-216">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="0332d-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="0332d-217">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="0332d-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="0332d-218">È possibile provare a:</span><span class="sxs-lookup"><span data-stu-id="0332d-218">You might try:</span></span>

[<span data-ttu-id="0332d-219">Proteggere un'API Web usando il modello B2C in Node.js</span><span class="sxs-lookup"><span data-stu-id="0332d-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
