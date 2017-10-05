---
title: Proteggere un'API Web di Azure Active Directory versione 2.0 tramite Node.js | Microsoft Docs
description: Informazioni su come creare un'API Web Node.js che accetta token sia da un account Microsoft personale che da account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="b023a-103">Proteggere un'API Web usando node.js</span><span class="sxs-lookup"><span data-stu-id="b023a-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="b023a-104">Non tutti gli scenari e le funzionalità di Azure Active Directory usano l'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="b023a-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="b023a-105">Per determinare se è necessario usare l'endpoint v2.0 o l'endpoint v1.0, leggere le informazioni sulle [limitazioni della versione 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b023a-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="b023a-106">Quando si usa l'endpoint di Azure Active Directory (Azure AD) v 2.0, è possibile usare i token di accesso [OAuth 2.0](active-directory-v2-protocols.md) per proteggere l'API Web.</span><span class="sxs-lookup"><span data-stu-id="b023a-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="b023a-107">Con i token di accesso OAuth 2.0, gli utenti che dispongono sia di un account Microsoft personale che di un account aziendale o dell'istituto di istruzione possono accedere in modo sicuro all'API Web.</span><span class="sxs-lookup"><span data-stu-id="b023a-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="b023a-108">*Passport* è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="b023a-109">Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="b023a-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="b023a-110">In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="b023a-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="b023a-111">È stata sviluppata una strategia per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b023a-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="b023a-112">Questo articolo illustra come installare il modulo e quindi aggiungere il plug-in `passport-azure-ad` di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b023a-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="b023a-113">Scaricare</span><span class="sxs-lookup"><span data-stu-id="b023a-113">Download</span></span>
<span data-ttu-id="b023a-114">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="b023a-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="b023a-115">Per seguire l'esercitazione, è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="b023a-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="b023a-116">Al termine dell'esercitazione, è anche possibile ottenere l'applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="b023a-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="b023a-117">1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="b023a-117">1: Register an app</span></span>
<span data-ttu-id="b023a-118">Per registrare un'app creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b023a-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="b023a-119">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="b023a-119">Make sure you:</span></span>

* <span data-ttu-id="b023a-120">Copiare l'**ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="b023a-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="b023a-121">Per questa esercitazione occorre:</span><span class="sxs-lookup"><span data-stu-id="b023a-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="b023a-122">Aggiungere la piattaforma **Mobile** per l'app.</span><span class="sxs-lookup"><span data-stu-id="b023a-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="b023a-123">Copiare l' **URI di reindirizzamento** dal portale.</span><span class="sxs-lookup"><span data-stu-id="b023a-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="b023a-124">È necessario usare il valore URI predefinito `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="b023a-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="b023a-125">2: Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="b023a-125">2: Install Node.js</span></span>
<span data-ttu-id="b023a-126">Per usare l'esempio di questa esercitazione, è necessario [installare Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b023a-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="b023a-127">3: Installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="b023a-127">3: Install MongoDB</span></span>
<span data-ttu-id="b023a-128">Per usare correttamente questo esempio, è necessario [installare MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="b023a-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="b023a-129">Questo esempio usa MongoDB per rendere l'API REST persistente nelle istanze del server.</span><span class="sxs-lookup"><span data-stu-id="b023a-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b023a-130">In questo articolo si presuppone che si usino gli endpoint di server e di installazione predefiniti per MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="b023a-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="b023a-131">4: Installare i moduli Restify nell'API Web</span><span class="sxs-lookup"><span data-stu-id="b023a-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="b023a-132">Si usa Resitfy per compilare l'API REST.</span><span class="sxs-lookup"><span data-stu-id="b023a-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="b023a-133">Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express,</span><span class="sxs-lookup"><span data-stu-id="b023a-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="b023a-134">Restify è un set affidabile di funzionalità che è possibile usare per compilare API REST su Connect.</span><span class="sxs-lookup"><span data-stu-id="b023a-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="b023a-135">Installare Restify</span><span class="sxs-lookup"><span data-stu-id="b023a-135">Install restify</span></span>
1.  <span data-ttu-id="b023a-136">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="b023a-137">Se la directory **azuread** non esiste, crearla:</span><span class="sxs-lookup"><span data-stu-id="b023a-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="b023a-138">Installare Restify:</span><span class="sxs-lookup"><span data-stu-id="b023a-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="b023a-139">L'output di questo comando dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b023a-139">The output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="b023a-140">È stato visualizzato un errore?</span><span class="sxs-lookup"><span data-stu-id="b023a-140">Did you get an error?</span></span>
<span data-ttu-id="b023a-141">In alcuni sistemi operativi, quando si usa il comando `npm`, è possibile che venga visualizzato questo messaggio: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="b023a-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="b023a-142">Il messaggio di errore è seguito da una richiesta in cui è indicato di provare a eseguire l'account come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b023a-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="b023a-143">In tal caso, usare il comando `sudo` per eseguire `npm` a un livello di privilegi più elevato.</span><span class="sxs-lookup"><span data-stu-id="b023a-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="b023a-144">È stato visualizzato un errore relativo a DTrace?</span><span class="sxs-lookup"><span data-stu-id="b023a-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="b023a-145">Quando si installa Restify, è possibile che venga visualizzato questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="b023a-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="b023a-146">Restify dispone di un meccanismo efficace per tenere traccia delle chiamate REST usando DTrace.</span><span class="sxs-lookup"><span data-stu-id="b023a-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="b023a-147">Tuttavia, in molti sistemi operativi DTrace non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="b023a-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="b023a-148">È possibile ignorare questo messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="b023a-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="b023a-149">5: Installare Passport.js nell'API Web</span><span class="sxs-lookup"><span data-stu-id="b023a-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="b023a-150">Al prompt dei comandi passare alla directory **azuread**.</span><span class="sxs-lookup"><span data-stu-id="b023a-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="b023a-151">Installare Passport.js:</span><span class="sxs-lookup"><span data-stu-id="b023a-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="b023a-152">L'output di questo comando dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b023a-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="b023a-153">6: Aggiungere passport-azure-ad all'API Web</span><span class="sxs-lookup"><span data-stu-id="b023a-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="b023a-154">Quindi, aggiungere la strategia di OAuth, usando passport azuread.</span><span class="sxs-lookup"><span data-stu-id="b023a-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="b023a-155">`passport-azuread` è una suite di strategie che connettono Azure AD a Passport.</span><span class="sxs-lookup"><span data-stu-id="b023a-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="b023a-156">In questo esempio di API REST tale strategia viene usata per i token di connessione.</span><span class="sxs-lookup"><span data-stu-id="b023a-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="b023a-157">Anche se OAuth 2.0 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, sono comunemente usati alcuni tipi di token.</span><span class="sxs-lookup"><span data-stu-id="b023a-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="b023a-158">I token di connessione vengono comunemente usati per proteggere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="b023a-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="b023a-159">I token di connessione sono il tipo di token maggiormente rilasciato in OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b023a-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="b023a-160">Molte implementazioni di OAuth 2.0 presumono che i token di connessione siano l'unico tipo di token rilasciato.</span><span class="sxs-lookup"><span data-stu-id="b023a-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="b023a-161">Al prompt dei comandi passare alla directory **azuread**.</span><span class="sxs-lookup"><span data-stu-id="b023a-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-162">Installare il modulo `passport-azure-ad` di Passport.js:</span><span class="sxs-lookup"><span data-stu-id="b023a-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="b023a-163">L'output di questo comando dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b023a-163">The output of the command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="b023a-164">7: Aggiungere i moduli MongoDB all'API Web</span><span class="sxs-lookup"><span data-stu-id="b023a-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="b023a-165">Questo esempio usa MongoDB come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="b023a-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="b023a-166">Installare Mongoose, un plug-in diffuso per la gestione di modelli e schemi:</span><span class="sxs-lookup"><span data-stu-id="b023a-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="b023a-167">Installare il driver del database per MongoDB, anche questo denominato MongoDB:</span><span class="sxs-lookup"><span data-stu-id="b023a-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="b023a-168">8. Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="b023a-168">8: Install additional modules</span></span>
<span data-ttu-id="b023a-169">Installare gli altri moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="b023a-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="b023a-170">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-171">Immettere i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b023a-171">Enter the following commands.</span></span> <span data-ttu-id="b023a-172">I comandi installano i moduli seguenti nella directory node_modules:</span><span class="sxs-lookup"><span data-stu-id="b023a-172">The commands install the following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="b023a-173">9: Creare un file Server.js per le dipendenze</span><span class="sxs-lookup"><span data-stu-id="b023a-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="b023a-174">Il file Server.js fornirà la maggior parte della funzionalità per il server API Web.</span><span class="sxs-lookup"><span data-stu-id="b023a-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="b023a-175">Aggiungere la maggior parte del codice a questo file.</span><span class="sxs-lookup"><span data-stu-id="b023a-175">Add most of your code to this file.</span></span> <span data-ttu-id="b023a-176">Per la produzione, è possibile eseguire il refactoring della funzionalità in file più piccoli, come per route e controller distinti.</span><span class="sxs-lookup"><span data-stu-id="b023a-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="b023a-177">Questo articolo usa Server.js a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="b023a-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="b023a-178">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-179">Usando un editor di propria scelta, creare un file Server.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="b023a-180">Aggiungere al file le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b023a-180">Add the following information to the file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="b023a-181">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="b023a-181">Save the file.</span></span> <span data-ttu-id="b023a-182">Servirà ancora tra poco.</span><span class="sxs-lookup"><span data-stu-id="b023a-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="b023a-183">10: Creare un file config per archiviare le impostazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b023a-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="b023a-184">Questo file di codice passa i parametri di configurazione dal portale di Azure AD a Passport.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="b023a-185">Questi valori di configurazione sono stati creati quando si è aggiunta l'API Web al portale nella prima parte dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="b023a-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="b023a-186">Dopo aver copiato il codice, verrà spiegato che cosa inserire nei valori di questi parametri.</span><span class="sxs-lookup"><span data-stu-id="b023a-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="b023a-187">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-188">In un editor creare un file Config.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="b023a-189">Aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b023a-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="b023a-190">Valori richiesti</span><span class="sxs-lookup"><span data-stu-id="b023a-190">Required values</span></span>

*   <span data-ttu-id="b023a-191">**IdentityMetadata**: l'area in cui `passport-azure-ad` cercherà i dati di configurazione per il provider di identità (IDP), nonché le chiavi per la convalida dei token JSON Web (JWT).</span><span class="sxs-lookup"><span data-stu-id="b023a-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="b023a-192">Se si usa Azure AD, probabilmente non si desidera modificare questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="b023a-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="b023a-193">**audience**: URI di reindirizzamento dal portale.</span><span class="sxs-lookup"><span data-stu-id="b023a-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b023a-194">Le chiavi vengono registrate con una certa frequenza.</span><span class="sxs-lookup"><span data-stu-id="b023a-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="b023a-195">Assicurarsi di eseguire sempre il pull dall'URL "openid_keys" e che l'app possa accedere a Internet.</span><span class="sxs-lookup"><span data-stu-id="b023a-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="b023a-196">11: Aggiungere la configurazione al file Server.js</span><span class="sxs-lookup"><span data-stu-id="b023a-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="b023a-197">L'applicazione deve leggere questi valori dal file config appena creato.</span><span class="sxs-lookup"><span data-stu-id="b023a-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="b023a-198">Aggiungere il file config come risorsa necessaria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b023a-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="b023a-199">Impostare le variabili globali su quelle in Config.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="b023a-200">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-201">In un editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-201">In an editor, open Server.js.</span></span> <span data-ttu-id="b023a-202">Aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b023a-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="b023a-203">Aggiungere una nuova sezione a Server.js:</span><span class="sxs-lookup"><span data-stu-id="b023a-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="b023a-204">12: Aggiungere le informazioni su schemi e modelli MongoDB usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="b023a-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="b023a-205">Successivamente, connettere questi tre file in un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="b023a-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="b023a-206">Questo articolo usa MongoDB per archiviare le attività.</span><span class="sxs-lookup"><span data-stu-id="b023a-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="b023a-207">Questa operazione viene illustrata nel *passaggio 4*.</span><span class="sxs-lookup"><span data-stu-id="b023a-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="b023a-208">Nel file Config.js creato nel passaggio 11 il database è denominato *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="b023a-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="b023a-209">Questo database è stato inserito alla fine dell'URL di connessione mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="b023a-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="b023a-210">Non è necessario creare in anticipo il database in MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b023a-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="b023a-211">Il database viene creato alla prima esecuzione dell'applicazione server (presupponendo che il database non esista già).</span><span class="sxs-lookup"><span data-stu-id="b023a-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="b023a-212">Si è indicato al server quale database MongoDB usare.</span><span class="sxs-lookup"><span data-stu-id="b023a-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="b023a-213">Successivamente, è necessario scrivere codice aggiuntivo per creare il modello e lo schema per le attività del server.</span><span class="sxs-lookup"><span data-stu-id="b023a-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="b023a-214">Il modello</span><span class="sxs-lookup"><span data-stu-id="b023a-214">The model</span></span>
<span data-ttu-id="b023a-215">Il modello dello schema è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="b023a-215">The schema model is very basic.</span></span> <span data-ttu-id="b023a-216">Se necessario, è possibile espanderlo.</span><span class="sxs-lookup"><span data-stu-id="b023a-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="b023a-217">Il modello dello schema presenta questi valori:</span><span class="sxs-lookup"><span data-stu-id="b023a-217">The schema model has these values:</span></span>

*   <span data-ttu-id="b023a-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="b023a-218">**NAME**.</span></span> <span data-ttu-id="b023a-219">Persona assegnata all'attività.</span><span class="sxs-lookup"><span data-stu-id="b023a-219">The person assigned to the task.</span></span> <span data-ttu-id="b023a-220">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="b023a-220">This is a **string** value.</span></span>
*   <span data-ttu-id="b023a-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="b023a-221">**TASK**.</span></span> <span data-ttu-id="b023a-222">Nome dell'attività.</span><span class="sxs-lookup"><span data-stu-id="b023a-222">The name of the task.</span></span> <span data-ttu-id="b023a-223">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="b023a-223">This is a **string** value.</span></span>
*   <span data-ttu-id="b023a-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="b023a-224">**DATE**.</span></span> <span data-ttu-id="b023a-225">Data di scadenza dell'attività.</span><span class="sxs-lookup"><span data-stu-id="b023a-225">The date that the task is due.</span></span> <span data-ttu-id="b023a-226">Valore **datetime**.</span><span class="sxs-lookup"><span data-stu-id="b023a-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="b023a-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="b023a-227">**COMPLETED**.</span></span> <span data-ttu-id="b023a-228">Indica se l'attività è stata completata o meno.</span><span class="sxs-lookup"><span data-stu-id="b023a-228">Whether the task is completed.</span></span> <span data-ttu-id="b023a-229">Valore **booleano**.</span><span class="sxs-lookup"><span data-stu-id="b023a-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="b023a-230">Creare lo schema nel codice</span><span class="sxs-lookup"><span data-stu-id="b023a-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="b023a-231">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-232">Nell'editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-232">In your editor, open Server.js.</span></span> <span data-ttu-id="b023a-233">Sotto la voce di configurazione, aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b023a-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="b023a-234">Questo codice si connette al server MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b023a-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="b023a-235">Restituisce inoltre un oggetto schema.</span><span class="sxs-lookup"><span data-stu-id="b023a-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="b023a-236">Usando lo schema, creare il modello nel codice</span><span class="sxs-lookup"><span data-stu-id="b023a-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="b023a-237">Sotto il codice precedente aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b023a-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="b023a-238">Come si può vedere dal codice, per prima cosa viene creato lo schema.</span><span class="sxs-lookup"><span data-stu-id="b023a-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="b023a-239">Si crea quindi un oggetto modello.</span><span class="sxs-lookup"><span data-stu-id="b023a-239">Next, you create a model object.</span></span> <span data-ttu-id="b023a-240">Usare l'oggetto modello per archiviare i dati in tutto il codice quando si definiscono le **route**.</span><span class="sxs-lookup"><span data-stu-id="b023a-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="b023a-241">13: Aggiungere le route per il server API REST delle attività</span><span class="sxs-lookup"><span data-stu-id="b023a-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="b023a-242">Ora che è disponibile un modello di database con cui lavorare, aggiungere le route che verranno usate per il server API REST.</span><span class="sxs-lookup"><span data-stu-id="b023a-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="b023a-243">Informazioni sulle route in Restify</span><span class="sxs-lookup"><span data-stu-id="b023a-243">About routes in restify</span></span>
<span data-ttu-id="b023a-244">Le route in Restify funzionano esattamente come avviene quando si usa lo stack di Express.</span><span class="sxs-lookup"><span data-stu-id="b023a-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="b023a-245">Definire le route usando l'URI che si prevede verrà chiamato dalle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="b023a-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="b023a-246">Le route si definiscono di solito in un file separato.</span><span class="sxs-lookup"><span data-stu-id="b023a-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="b023a-247">In questa esercitazione, le route sono inserite in Server.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="b023a-248">È consigliabile fattorizzarle nel relativo file per usarle in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="b023a-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="b023a-249">Un modello tipico per una route Restify è:</span><span class="sxs-lookup"><span data-stu-id="b023a-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="b023a-250">Questo è il modello più semplice.</span><span class="sxs-lookup"><span data-stu-id="b023a-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="b023a-251">Restify ed Express offrono funzionalità molto più avanzate come la definizione di tipi di applicazione e il routing complesso tra endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="b023a-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="b023a-252">Aggiungere le route predefinite al server</span><span class="sxs-lookup"><span data-stu-id="b023a-252">Add default routes to your server</span></span>
<span data-ttu-id="b023a-253">Aggiungere le route CRUD di base: **creazione**, **recupero**, **aggiornamento** ed **eliminazione**.</span><span class="sxs-lookup"><span data-stu-id="b023a-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="b023a-254">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b023a-255">In un editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="b023a-255">In an editor, open Server.js.</span></span> <span data-ttu-id="b023a-256">Aggiungere le informazioni seguenti sotto le voci di database create in precedenza:</span><span class="sxs-lookup"><span data-stu-id="b023a-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable to save');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable to delete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in the database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="b023a-257">Aggiungere la gestione di errori per le route</span><span class="sxs-lookup"><span data-stu-id="b023a-257">Add error handling for the routes</span></span>
<span data-ttu-id="b023a-258">Aggiungere la gestione di errori per poter comunicare al client il problema che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="b023a-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="b023a-259">Aggiungere il codice seguente sotto il codice già scritto:</span><span class="sxs-lookup"><span data-stu-id="b023a-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="b023a-260">14: Creare il server</span><span class="sxs-lookup"><span data-stu-id="b023a-260">14: Create your server</span></span>
<span data-ttu-id="b023a-261">L'ultima operazione da eseguire consiste nell'aggiungere l'istanza del server.</span><span class="sxs-lookup"><span data-stu-id="b023a-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="b023a-262">L'istanza del server gestisce le chiamate.</span><span class="sxs-lookup"><span data-stu-id="b023a-262">The server instance manages your calls.</span></span>

<span data-ttu-id="b023a-263">Restify ed Express hanno un elevato livello di personalizzazione che è possibile usare con un server API REST.</span><span class="sxs-lookup"><span data-stu-id="b023a-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="b023a-264">Per questa esercitazione si userà la configurazione più semplice.</span><span class="sxs-lookup"><span data-stu-id="b023a-264">In this tutorial, we use the most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst to 10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="b023a-265">15: Aggiungere le route (per ora senza autenticazione)</span><span class="sxs-lookup"><span data-stu-id="b023a-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="b023a-266">16: Eseguire il server</span><span class="sxs-lookup"><span data-stu-id="b023a-266">16: Run the server</span></span>
<span data-ttu-id="b023a-267">È consigliabile eseguire il test del server prima di aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b023a-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="b023a-268">Il modo più semplice per farlo consiste nell'usare Curl al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b023a-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="b023a-269">È necessaria una semplice utilità che consente di analizzare l'output come JSON.</span><span class="sxs-lookup"><span data-stu-id="b023a-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="b023a-270">Installare lo strumento JSON usato negli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b023a-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="b023a-271">Questo comando installa lo strumento JSON a livello globale.</span><span class="sxs-lookup"><span data-stu-id="b023a-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="b023a-272">Assicurarsi che l'istanza di MongoDB sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b023a-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="b023a-273">Passare alla directory **azuread** e quindi eseguire Curl:</span><span class="sxs-lookup"><span data-stu-id="b023a-273">Change the directory to **azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="b023a-274">Per aggiungere un'attività:</span><span class="sxs-lookup"><span data-stu-id="b023a-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="b023a-275">La risposta dovrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="b023a-275">The response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="b023a-276">Elenco delle attività Brandon:</span><span class="sxs-lookup"><span data-stu-id="b023a-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="b023a-277">Se tutti questi comandi vengono eseguiti senza errori, è possibile aggiungere OAuth al server dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="b023a-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="b023a-278">*Ora si dispone di un server API REST con MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="b023a-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="b023a-279">17: Aggiungere l'autenticazione al server API REST</span><span class="sxs-lookup"><span data-stu-id="b023a-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="b023a-280">Ora che l'API REST è in esecuzione, è possibile configurarla per usarla in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b023a-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="b023a-281">Al prompt dei comandi passare alla directory **azuread**:</span><span class="sxs-lookup"><span data-stu-id="b023a-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="b023a-282">Usare l'oggetto oidcbearerstrategy incluso in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="b023a-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="b023a-283">Nei passaggi precedenti è stato creato un tipico server REST TODO senza alcun tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b023a-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="b023a-284">Aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b023a-284">Now, add authentication.</span></span>

<span data-ttu-id="b023a-285">In primo luogo, indicare che si desidera usare Passport.</span><span class="sxs-lookup"><span data-stu-id="b023a-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="b023a-286">Inserire il codice subito dopo la configurazione del server precedente:</span><span class="sxs-lookup"><span data-stu-id="b023a-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="b023a-287">Durante la scrittura delle API è sempre consigliabile collegare i dati a un elemento univoco del token di cui l'utente non può eseguire lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="b023a-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="b023a-288">Quando archivia gli elementi TODO, il server esegue questa operazione in base all'ID sottoscrizione dell'utente nel token (chiamato mediante token.sub).</span><span class="sxs-lookup"><span data-stu-id="b023a-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="b023a-289">Inserire il token.sub nel campo "owner".</span><span class="sxs-lookup"><span data-stu-id="b023a-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="b023a-290">In questo modo, solo l'utente può accedere ai propri elementi TODO.</span><span class="sxs-lookup"><span data-stu-id="b023a-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="b023a-291">Nessun altro può accedere agli elementi TODO immessi.</span><span class="sxs-lookup"><span data-stu-id="b023a-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="b023a-292">Nell'API di "owner" non è presente alcuna esposizione.</span><span class="sxs-lookup"><span data-stu-id="b023a-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="b023a-293">Un utente esterno può richiedere gli elementi TODO di altri utenti, anche se sono autenticati.</span><span class="sxs-lookup"><span data-stu-id="b023a-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="b023a-294">Usare quindi la strategia Open ID Connect Bearer fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="b023a-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="b023a-295">Inserire il codice seguente dopo quanto inserito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="b023a-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying the user');
log.info(token, 'was the token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="b023a-296">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via).</span><span class="sxs-lookup"><span data-stu-id="b023a-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="b023a-297">Tutti i writer di strategie rispettano questo modello.</span><span class="sxs-lookup"><span data-stu-id="b023a-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="b023a-298">Passare alla strategia un elemento `function()` che usa un token e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="b023a-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="b023a-299">La strategia viene restituita dopo l'esecuzione di tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="b023a-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="b023a-300">Archiviare l'utente e mettere da parte il token per non doverlo richiedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b023a-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b023a-301">Il codice precedente accetta qualsiasi utente che può eseguire l'autenticazione al server.</span><span class="sxs-lookup"><span data-stu-id="b023a-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="b023a-302">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="b023a-302">This is known as auto-registration.</span></span> <span data-ttu-id="b023a-303">Nei server di produzione è preferibile non consentire l'accesso a chiunque senza prima prevedere un processo di registrazione a scelta.</span><span class="sxs-lookup"><span data-stu-id="b023a-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="b023a-304">Questo è il modello in genere adottato per le app consumer.</span><span class="sxs-lookup"><span data-stu-id="b023a-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="b023a-305">L'app potrebbe consentire di eseguire la registrazione con Facebook, ma poi richiede di inserire informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b023a-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="b023a-306">Se per questa esercitazione non è stato usato un programma della riga di comando, è possibile estrarre il messaggio di posta elettronica dall'oggetto token restituito.</span><span class="sxs-lookup"><span data-stu-id="b023a-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="b023a-307">Quindi, è possibile chiedere all'utente di inserire informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b023a-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="b023a-308">Trattandosi di un server di test, è possibile aggiungere l'utente direttamente al database in-memory.</span><span class="sxs-lookup"><span data-stu-id="b023a-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="b023a-309">Proteggere gli endpoint</span><span class="sxs-lookup"><span data-stu-id="b023a-309">Protect endpoints</span></span>
<span data-ttu-id="b023a-310">Proteggere gli endpoint, specificando la chiamata a **passport.authenticate()** con il protocollo preferito.</span><span class="sxs-lookup"><span data-stu-id="b023a-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="b023a-311">È possibile modificare la route nel codice del server per un'opzione più avanzata:</span><span class="sxs-lookup"><span data-stu-id="b023a-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="b023a-312">18: Eseguire nuovamente l'applicazione server</span><span class="sxs-lookup"><span data-stu-id="b023a-312">18: Run your server application again</span></span>
<span data-ttu-id="b023a-313">Per verificare se la protezione OAuth 2.0 per gli endpoint è attiva, usare nuovamente Curl.</span><span class="sxs-lookup"><span data-stu-id="b023a-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="b023a-314">Eseguire questa operazione prima di usare uno qualsiasi degli SDK client in questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="b023a-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="b023a-315">Le intestazioni restituite dovrebbero indicare se l'autenticazione funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="b023a-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="b023a-316">Assicurarsi che l'istanza di MongoDB sia in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="b023a-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="b023a-317">Passare alla directory **azuread**, quindi usare Curl:</span><span class="sxs-lookup"><span data-stu-id="b023a-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="b023a-318">Provare un'operazione POST di base:</span><span class="sxs-lookup"><span data-stu-id="b023a-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="b023a-319">Una risposta 401 indica che il livello Passport sta tentando il reindirizzamento all'endpoint di autorizzazione, ovvero il comportamento voluto.</span><span class="sxs-lookup"><span data-stu-id="b023a-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="b023a-320">*Ora è disponibile un servizio API REST che usa OAuth 2.0*.</span><span class="sxs-lookup"><span data-stu-id="b023a-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="b023a-321">Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b023a-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="b023a-322">A tale scopo, è necessario esaminare un'esercitazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="b023a-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b023a-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b023a-323">Next steps</span></span>
<span data-ttu-id="b023a-324">Come riferimento viene fornito l'esempio completato, senza i valori di configurazione, [come file zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b023a-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="b023a-325">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="b023a-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="b023a-326">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="b023a-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="b023a-327">Si potrebbe volere [proteggere un'app Web Node.js usando l'endpoint v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="b023a-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="b023a-328">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="b023a-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="b023a-329">Guida per sviluppatori Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="b023a-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b023a-330">StackOverflow: tag "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="b023a-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b023a-331">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="b023a-331">Get security updates for our products</span></span>
<span data-ttu-id="b023a-332">È consigliabile eseguire l'iscrizione per ricevere una notifica quando si verificano problemi di protezione.</span><span class="sxs-lookup"><span data-stu-id="b023a-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="b023a-333">Nella pagina [Notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) effettuare la sottoscrizione agli advisory sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b023a-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

