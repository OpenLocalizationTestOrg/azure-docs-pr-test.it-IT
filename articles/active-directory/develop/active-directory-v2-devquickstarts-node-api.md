---
title: aaaSecure un'API web v 2.0 di Azure Active Directory con Node.js | Documenti Microsoft
description: Informazioni su come toobuild un Node.js web API che accetta i token da un account Microsoft personale e dagli account aziendale o dell'istituto di istruzione.
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
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="cb572-103">Proteggere un'API Web usando node.js</span><span class="sxs-lookup"><span data-stu-id="cb572-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="cb572-104">Non tutti gli scenari di Azure Active Directory e le funzionalità di lavoro con endpoint v 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="cb572-105">toodetermine se è necessario utilizzare hello v 2.0 endpoint o hello v 1.0, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="cb572-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="cb572-106">Quando si utilizza l'endpoint di hello Azure Active Directory (Azure AD) v 2.0, è possibile utilizzare [OAuth 2.0](active-directory-v2-protocols.md) token di accesso tooprotect l'API web.</span><span class="sxs-lookup"><span data-stu-id="cb572-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="cb572-107">Con i token di accesso OAuth 2.0, gli utenti che dispongono sia di un account Microsoft personale che di un account aziendale o dell'istituto di istruzione possono accedere in modo sicuro all'API Web.</span><span class="sxs-lookup"><span data-stu-id="cb572-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="cb572-108">*Passport* è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="cb572-109">Passport, flessibile e modulare, può essere rilasciato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="cb572-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="cb572-110">In Passport una gamma completa di strategie supporta l'autenticazione usando un nome utente e password, Facebook, Twitter o altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="cb572-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="cb572-111">È stata sviluppata una strategia per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb572-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="cb572-112">In questo articolo è illustrato come tooinstall hello modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="cb572-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="cb572-113">Scaricare</span><span class="sxs-lookup"><span data-stu-id="cb572-113">Download</span></span>
<span data-ttu-id="cb572-114">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="cb572-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="cb572-115">esercitazione di hello toofollow, è possibile [scheletro dell'applicazione hello come file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="cb572-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="cb572-116">È anche possibile ottenere un'applicazione hello completata alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="cb572-117">1: Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="cb572-117">1: Register an app</span></span>
<span data-ttu-id="cb572-118">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire [questi passaggi dettagliati](active-directory-v2-app-registration.md) tooregister un'app.</span><span class="sxs-lookup"><span data-stu-id="cb572-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="cb572-119">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="cb572-119">Make sure you:</span></span>

* <span data-ttu-id="cb572-120">Hello copia **Id applicazione** assegnato tooyour app.</span><span class="sxs-lookup"><span data-stu-id="cb572-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="cb572-121">Per questa esercitazione occorre:</span><span class="sxs-lookup"><span data-stu-id="cb572-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="cb572-122">Aggiungere hello **Mobile** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="cb572-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="cb572-123">Hello copia **URI di reindirizzamento** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="cb572-124">È necessario utilizzare hello URI valore predefinito `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="cb572-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="cb572-125">2: Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="cb572-125">2: Install Node.js</span></span>
<span data-ttu-id="cb572-126">esempio di hello toouse per questa esercitazione, è necessario [installare Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="cb572-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="cb572-127">3: Installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="cb572-127">3: Install MongoDB</span></span>
<span data-ttu-id="cb572-128">toosuccessfully usare questo esempio, è necessario [installare MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="cb572-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="cb572-129">In questo esempio, si utilizza MongoDB toomake l'API REST persistente tra istanze di server.</span><span class="sxs-lookup"><span data-stu-id="cb572-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="cb572-130">In questo articolo si presuppone che si utilizzino gli endpoint di installazione e il server predefinito hello per MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="cb572-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="cb572-131">4: installazione hello restify moduli in web API</span><span class="sxs-lookup"><span data-stu-id="cb572-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="cb572-132">Utilizziamo Resitfy toobuild API REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="cb572-133">Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express,</span><span class="sxs-lookup"><span data-stu-id="cb572-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="cb572-134">Restify dispone di un set affidabile di funzionalità che è possibile usare le API REST su Connect toobuild.</span><span class="sxs-lookup"><span data-stu-id="cb572-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="cb572-135">Installare Restify</span><span class="sxs-lookup"><span data-stu-id="cb572-135">Install restify</span></span>
1.  <span data-ttu-id="cb572-136">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="cb572-137">Se hello **azuread** directory non esiste, crearla:</span><span class="sxs-lookup"><span data-stu-id="cb572-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="cb572-138">Installare Restify:</span><span class="sxs-lookup"><span data-stu-id="cb572-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="cb572-139">output di Hello di questo comando dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cb572-139">hello output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="cb572-140">È stato visualizzato un errore?</span><span class="sxs-lookup"><span data-stu-id="cb572-140">Did you get an error?</span></span>
<span data-ttu-id="cb572-141">In alcuni sistemi operativi, quando si utilizza hello `npm` comando, è possibile che questo messaggio: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="cb572-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="cb572-142">Errore Hello è seguito da una richiesta che si tenta di account hello in esecuzione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cb572-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="cb572-143">In questo caso, utilizzare il comando hello `sudo` toorun `npm` a un livello di privilegio superiore.</span><span class="sxs-lookup"><span data-stu-id="cb572-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="cb572-144">È stato si verifica un errore correlato tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="cb572-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="cb572-145">Quando si installa Restify, è possibile che venga visualizzato questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="cb572-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="cb572-146">Restify ha tootrace un meccanismo avanzato tramite /DTRACE le chiamate REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="cb572-147">Tuttavia, in molti sistemi operativi DTrace non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="cb572-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="cb572-148">È possibile ignorare questo messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="cb572-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="cb572-149">5: Installare Passport.js nell'API Web</span><span class="sxs-lookup"><span data-stu-id="cb572-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="cb572-150">Al prompt dei comandi di hello, modificare la directory hello troppo**azuread**.</span><span class="sxs-lookup"><span data-stu-id="cb572-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="cb572-151">Installare Passport.js:</span><span class="sxs-lookup"><span data-stu-id="cb572-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="cb572-152">output di Hello del comando hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cb572-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="cb572-153">6: aggiungere le API web tooyour passport-azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb572-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="cb572-154">Successivamente, aggiungere strategia OAuth hello, utilizzando passport azuread.</span><span class="sxs-lookup"><span data-stu-id="cb572-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="cb572-155">`passport-azuread` è una suite di strategie che connettono Azure AD a Passport.</span><span class="sxs-lookup"><span data-stu-id="cb572-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="cb572-156">In questo esempio di API REST tale strategia viene usata per i token di connessione.</span><span class="sxs-lookup"><span data-stu-id="cb572-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="cb572-157">Anche se OAuth 2.0 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, sono comunemente usati alcuni tipi di token.</span><span class="sxs-lookup"><span data-stu-id="cb572-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="cb572-158">I token di connessione sono endpoint tooprotect comunemente utilizzati.</span><span class="sxs-lookup"><span data-stu-id="cb572-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="cb572-159">I token di connessione sono tipo hello maggiormente emesso del token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb572-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="cb572-160">Molte implementazioni di OAuth 2.0 si presuppongono che i token di connessione sono hello unico tipo di token rilasciato.</span><span class="sxs-lookup"><span data-stu-id="cb572-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="cb572-161">Al prompt dei comandi, modificare la directory hello troppo**azuread**.</span><span class="sxs-lookup"><span data-stu-id="cb572-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-162">Installare hello Passport.js `passport-azure-ad` modulo:</span><span class="sxs-lookup"><span data-stu-id="cb572-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="cb572-163">output di Hello del comando hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cb572-163">hello output of hello command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="cb572-164">7: aggiungere MongoDB moduli tooyour web API</span><span class="sxs-lookup"><span data-stu-id="cb572-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="cb572-165">Questo esempio usa MongoDB come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="cb572-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="cb572-166">Installare Mongoose, ampiamente usati plug-in, i modelli di toomanage e gli schemi:</span><span class="sxs-lookup"><span data-stu-id="cb572-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="cb572-167">Installare i driver di database hello per MongoDB, denominato anche MongoDB:</span><span class="sxs-lookup"><span data-stu-id="cb572-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="cb572-168">8. Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="cb572-168">8: Install additional modules</span></span>
<span data-ttu-id="cb572-169">Installare hello rimanenti moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="cb572-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="cb572-170">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-171">Immettere i seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-171">Enter hello following commands.</span></span> <span data-ttu-id="cb572-172">i comandi di Hello installano hello moduli nella cartella node_modules di seguito:</span><span class="sxs-lookup"><span data-stu-id="cb572-172">hello commands install hello following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="cb572-173">9: Creare un file Server.js per le dipendenze</span><span class="sxs-lookup"><span data-stu-id="cb572-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="cb572-174">Un file Server.js contiene la maggior parte hello funzionalità hello del server web API.</span><span class="sxs-lookup"><span data-stu-id="cb572-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="cb572-175">Aggiungere la maggior parte dei file toothis del codice.</span><span class="sxs-lookup"><span data-stu-id="cb572-175">Add most of your code toothis file.</span></span> <span data-ttu-id="cb572-176">Ai fini della produzione, è possibile effettuare il refactoring funzionalità hello in file più piccoli, come per i controller e route distinte.</span><span class="sxs-lookup"><span data-stu-id="cb572-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="cb572-177">Questo articolo usa Server.js a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="cb572-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="cb572-178">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-179">Usando un editor di propria scelta, creare un file Server.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="cb572-180">Aggiungere i seguenti file di informazioni toohello hello:</span><span class="sxs-lookup"><span data-stu-id="cb572-180">Add hello following information toohello file:</span></span>

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

3.  <span data-ttu-id="cb572-181">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-181">Save hello file.</span></span> <span data-ttu-id="cb572-182">Si tornerà tooit a breve.</span><span class="sxs-lookup"><span data-stu-id="cb572-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="cb572-183">10: creare un toostore di file di configurazione delle impostazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb572-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="cb572-184">Questo file di codice passa i parametri di configurazione hello dal tooPassport.js del portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb572-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="cb572-185">Portale di hello web API toohello è stato aggiunto all'inizio di hello dell'articolo hello creato questi valori di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="cb572-186">Dopo aver copiato il codice hello, spiega quali tooput in valori hello di questi parametri.</span><span class="sxs-lookup"><span data-stu-id="cb572-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="cb572-187">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-188">In un editor creare un file Config.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="cb572-189">Aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb572-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="cb572-190">Valori richiesti</span><span class="sxs-lookup"><span data-stu-id="cb572-190">Required values</span></span>

*   <span data-ttu-id="cb572-191">**IdentityMetadata**: questa opzione è quando `passport-azure-ad` cerca i dati di configurazione per il provider di identità hello (IDP) e hello chiavi toovalidate hello token Web JSON (Jwt).</span><span class="sxs-lookup"><span data-stu-id="cb572-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="cb572-192">Se si utilizza Azure AD, è inoltre possibile nascondere toochange questo.</span><span class="sxs-lookup"><span data-stu-id="cb572-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="cb572-193">**gruppo di destinatari**: l'URI di reindirizzamento dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cb572-194">Le chiavi vengono registrate con una certa frequenza.</span><span class="sxs-lookup"><span data-stu-id="cb572-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="cb572-195">Assicurarsi che sempre possibile mettere dall'URL "openid_keys" hello, e tale applicazione hello può accedere hello Internet.</span><span class="sxs-lookup"><span data-stu-id="cb572-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="cb572-196">11: aggiungere hello configurazione tooyour Server.js file</span><span class="sxs-lookup"><span data-stu-id="cb572-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="cb572-197">L'applicazione richiede valori hello tooread dal file di configurazione hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="cb572-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="cb572-198">Aggiungere i file con estensione config hello come una risorsa necessaria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="cb572-199">Impostare toothose variabili globali hello in Config.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="cb572-200">Al prompt dei comandi di hello, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-201">In un editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-201">In an editor, open Server.js.</span></span> <span data-ttu-id="cb572-202">Aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb572-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="cb572-203">Aggiungere un nuovo tooServer.js sezione:</span><span class="sxs-lookup"><span data-stu-id="cb572-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="cb572-204">12: aggiungere informazioni di modello e lo schema di MongoDB hello utilizzando Mongoose</span><span class="sxs-lookup"><span data-stu-id="cb572-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="cb572-205">Successivamente, connettere questi tre file in un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="cb572-206">In questo articolo, si usa MongoDB toostore l'attività.</span><span class="sxs-lookup"><span data-stu-id="cb572-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="cb572-207">Questa operazione viene illustrata nel *passaggio 4*.</span><span class="sxs-lookup"><span data-stu-id="cb572-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="cb572-208">Nel file Config.js hello creato nel passaggio 11, il database è denominato *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="cb572-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="cb572-209">Che è stato inserito alla fine di hello dell'URL di connessione mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="cb572-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="cb572-210">Non è necessario toocreate questo database in anticipo in MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb572-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="cb572-211">Hello database viene creato in hello prima esecuzione dell'applicazione server (supponendo hello database non esiste già).</span><span class="sxs-lookup"><span data-stu-id="cb572-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="cb572-212">Si è indicato server hello quali toouse database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb572-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="cb572-213">Successivamente, è necessario toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.</span><span class="sxs-lookup"><span data-stu-id="cb572-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="cb572-214">modello Hello</span><span class="sxs-lookup"><span data-stu-id="cb572-214">hello model</span></span>
<span data-ttu-id="cb572-215">modello di schema Hello è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="cb572-215">hello schema model is very basic.</span></span> <span data-ttu-id="cb572-216">Se necessario, è possibile espanderlo.</span><span class="sxs-lookup"><span data-stu-id="cb572-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="cb572-217">modello di schema Hello presenta questi valori:</span><span class="sxs-lookup"><span data-stu-id="cb572-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="cb572-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="cb572-218">**NAME**.</span></span> <span data-ttu-id="cb572-219">attività di Hello persona toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="cb572-219">hello person assigned toohello task.</span></span> <span data-ttu-id="cb572-220">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="cb572-220">This is a **string** value.</span></span>
*   <span data-ttu-id="cb572-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="cb572-221">**TASK**.</span></span> <span data-ttu-id="cb572-222">nome di Hello dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-222">hello name of hello task.</span></span> <span data-ttu-id="cb572-223">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="cb572-223">This is a **string** value.</span></span>
*   <span data-ttu-id="cb572-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="cb572-224">**DATE**.</span></span> <span data-ttu-id="cb572-225">Data di Hello tale attività hello è scadenza.</span><span class="sxs-lookup"><span data-stu-id="cb572-225">hello date that hello task is due.</span></span> <span data-ttu-id="cb572-226">Valore **datetime**.</span><span class="sxs-lookup"><span data-stu-id="cb572-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="cb572-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="cb572-227">**COMPLETED**.</span></span> <span data-ttu-id="cb572-228">Se viene completata l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-228">Whether hello task is completed.</span></span> <span data-ttu-id="cb572-229">Valore **booleano**.</span><span class="sxs-lookup"><span data-stu-id="cb572-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="cb572-230">Creare uno schema di hello codice hello</span><span class="sxs-lookup"><span data-stu-id="cb572-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="cb572-231">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-232">Nell'editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-232">In your editor, open Server.js.</span></span> <span data-ttu-id="cb572-233">Sotto la voce di configurazione hello aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb572-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="cb572-234">Questo codice si connette toohello MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="cb572-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="cb572-235">Restituisce inoltre un oggetto schema.</span><span class="sxs-lookup"><span data-stu-id="cb572-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="cb572-236">Usa schema hello, creare il modello nel codice hello</span><span class="sxs-lookup"><span data-stu-id="cb572-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="cb572-237">Di sotto di hello codice precedente, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="cb572-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="cb572-238">Come si può vedere dal codice hello, prima creare uno schema.</span><span class="sxs-lookup"><span data-stu-id="cb572-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="cb572-239">Si crea quindi un oggetto modello.</span><span class="sxs-lookup"><span data-stu-id="cb572-239">Next, you create a model object.</span></span> <span data-ttu-id="cb572-240">Utilizzare hello modello oggetto toostore i dati in tutto hello codice quando si definisce il **route**.</span><span class="sxs-lookup"><span data-stu-id="cb572-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="cb572-241">13: Aggiungere le route per il server API REST delle attività</span><span class="sxs-lookup"><span data-stu-id="cb572-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="cb572-242">Dopo aver creato un toowork del modello di database con, aggiungere le route hello da usare per il server API REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="cb572-243">Informazioni sulle route in Restify</span><span class="sxs-lookup"><span data-stu-id="cb572-243">About routes in restify</span></span>
<span data-ttu-id="cb572-244">Route nella restify lavoro esattamente hello esattamente come quando si utilizza hello stack Express.</span><span class="sxs-lookup"><span data-stu-id="cb572-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="cb572-245">Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="cb572-246">Le route si definiscono di solito in un file separato.</span><span class="sxs-lookup"><span data-stu-id="cb572-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="cb572-247">In questa esercitazione, le route sono inserite in Server.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="cb572-248">È consigliabile fattorizzarle nel relativo file per usarle in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="cb572-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="cb572-249">Un modello tipico per una route Restify è:</span><span class="sxs-lookup"><span data-stu-id="cb572-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="cb572-250">Si tratta hello modello al livello più elementare di hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="cb572-251">Restify (ed Express) fornisce funzionalità molto più approfondita, ad esempio i tipi di applicazione hello possibilità toodefine e routing complessa in diversi endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb572-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="cb572-252">Aggiungere server tooyour di route predefinita</span><span class="sxs-lookup"><span data-stu-id="cb572-252">Add default routes tooyour server</span></span>
<span data-ttu-id="cb572-253">Aggiungere le route CRUD di base hello: **creare**, **recuperare**, **aggiornare**, e **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="cb572-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="cb572-254">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cb572-255">In un editor aprire Server.js.</span><span class="sxs-lookup"><span data-stu-id="cb572-255">In an editor, open Server.js.</span></span> <span data-ttu-id="cb572-256">Di seguito hello voci del database eseguite in precedenza, aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb572-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
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
    req.log.warn(err, 'createTask: unable toosave');
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
    'removeTask: unable toodelete %s',
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
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
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
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="cb572-257">Aggiungere la gestione di route hello</span><span class="sxs-lookup"><span data-stu-id="cb572-257">Add error handling for hello routes</span></span>
<span data-ttu-id="cb572-258">Aggiungere alcuni errori affinché si possa comunicare client toohello indietro problema hello che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="cb572-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="cb572-259">Aggiungere hello seguente di codice riportato di seguito codice hello, che è già scritto:</span><span class="sxs-lookup"><span data-stu-id="cb572-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="cb572-260">14: Creare il server</span><span class="sxs-lookup"><span data-stu-id="cb572-260">14: Create your server</span></span>
<span data-ttu-id="cb572-261">ultima operazione toodo Hello è tooadd l'istanza del server.</span><span class="sxs-lookup"><span data-stu-id="cb572-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="cb572-262">istanza del server Hello gestisce le chiamate.</span><span class="sxs-lookup"><span data-stu-id="cb572-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="cb572-263">Restify ed Express hanno un elevato livello di personalizzazione che è possibile usare con un server API REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="cb572-264">In questa esercitazione, si usa il programma di installazione di base hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-264">In this tutorial, we use hello most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst too10.
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
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="cb572-265">15: aggiungere le route hello (senza autenticazione, per ora)</span><span class="sxs-lookup"><span data-stu-id="cb572-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="cb572-266">16: eseguire hello server</span><span class="sxs-lookup"><span data-stu-id="cb572-266">16: Run hello server</span></span>
<span data-ttu-id="cb572-267">È una buona idea tootest il server prima di aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="cb572-268">tootest modo più semplice Hello del server è tramite curl un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="cb572-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="cb572-269">toodo, è necessario una semplice utilità che è possibile utilizzare tooparse output in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cb572-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="cb572-270">Installare utilità JSON hello usata in hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="cb572-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="cb572-271">Vengono installati lo strumento JSON hello a livello globale.</span><span class="sxs-lookup"><span data-stu-id="cb572-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="cb572-272">Assicurarsi che l'istanza di MongoDB sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cb572-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="cb572-273">Modificare anche le directory hello**azuread**, quindi eseguire curl:</span><span class="sxs-lookup"><span data-stu-id="cb572-273">Change hello directory too**azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="cb572-274">tooadd un'attività:</span><span class="sxs-lookup"><span data-stu-id="cb572-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="cb572-275">risposta Hello deve essere:</span><span class="sxs-lookup"><span data-stu-id="cb572-275">hello response should be:</span></span>

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

5.  <span data-ttu-id="cb572-276">Elenco delle attività Brandon:</span><span class="sxs-lookup"><span data-stu-id="cb572-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="cb572-277">Se tutti questi comandi vengono eseguiti senza errori, si è pronti tooadd OAuth toohello server dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="cb572-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="cb572-278">*Ora si dispone di un server API REST con MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="cb572-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="cb572-279">17: Aggiungi server di autenticazione tooyour API REST</span><span class="sxs-lookup"><span data-stu-id="cb572-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="cb572-280">Dopo aver creato un'API REST in esecuzione, configurarlo toouse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb572-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="cb572-281">Al prompt dei comandi, modificare la directory hello troppo**azuread**:</span><span class="sxs-lookup"><span data-stu-id="cb572-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="cb572-282">Utilizzare oidcbearerstrategy hello che è incluso con passport-azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb572-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="cb572-283">Nei passaggi precedenti è stato creato un tipico server REST TODO senza alcun tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="cb572-284">Aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="cb572-284">Now, add authentication.</span></span>

<span data-ttu-id="cb572-285">Innanzitutto, consente di indicare che si desidera toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="cb572-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="cb572-286">Inserire il codice subito dopo la configurazione del server precedente:</span><span class="sxs-lookup"><span data-stu-id="cb572-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="cb572-287">Quando si scrivono le API, è hello di collegamento tooalways una buona idea toosomething dati univoco da token hello hello utente non può effettuare lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="cb572-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="cb572-288">Quando il server archivia elementi TODO, li archivia in base all'ID di sottoscrizione utente hello nel token hello (chiamati tramite token.sub).</span><span class="sxs-lookup"><span data-stu-id="cb572-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="cb572-289">Nel campo "proprietario" hello, inserire token.sub hello.</span><span class="sxs-lookup"><span data-stu-id="cb572-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="cb572-290">In questo modo si garantisce che solo tale utente può accedere TODOs hello utente.</span><span class="sxs-lookup"><span data-stu-id="cb572-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="cb572-291">Nessun utente può accedere TODOs hello che sono state immesse.</span><span class="sxs-lookup"><span data-stu-id="cb572-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="cb572-292">È non presenti rischi in hello API per il "proprietario".</span><span class="sxs-lookup"><span data-stu-id="cb572-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="cb572-293">Un utente esterno può richiedere gli elementi TODO di altri utenti, anche se sono autenticati.</span><span class="sxs-lookup"><span data-stu-id="cb572-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="cb572-294">Successivamente, utilizzare strategia Open ID connessione connessione hello fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="cb572-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="cb572-295">Inserire il codice seguente dopo quanto inserito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="cb572-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
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

<span data-ttu-id="cb572-296">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via).</span><span class="sxs-lookup"><span data-stu-id="cb572-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="cb572-297">Tutti i writer strategia rispettare toohello modello.</span><span class="sxs-lookup"><span data-stu-id="cb572-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="cb572-298">Passare la strategia di hello un `function()` che utilizza un token e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="cb572-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="cb572-299">strategia di Hello viene restituito dopo esegue automaticamente tutte le relative operazioni.</span><span class="sxs-lookup"><span data-stu-id="cb572-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="cb572-300">Archivio utente hello e token hello stash pertanto non è necessario tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="cb572-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb572-301">Hello precedente il codice in tutti gli utenti possono eseguire l'autenticazione server tooyour.</span><span class="sxs-lookup"><span data-stu-id="cb572-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="cb572-302">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="cb572-302">This is known as auto-registration.</span></span> <span data-ttu-id="cb572-303">In un server di produzione, è preferibile toolet chiunque senza prima li passare attraverso un processo di registrazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="cb572-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="cb572-304">Si tratta in genere hello modello di App consumer.</span><span class="sxs-lookup"><span data-stu-id="cb572-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="cb572-305">app Hello potrebbero consentire di tooregister con Facebook, ma viene chiesto di tooenter ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cb572-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="cb572-306">Se non è stato utilizzato un programma della riga di comando per questa esercitazione, è stato possibile estrarre posta elettronica hello dall'oggetto hello token restituito.</span><span class="sxs-lookup"><span data-stu-id="cb572-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="cb572-307">Quindi, è possibile chiedere informazioni aggiuntive di hello utente tooenter.</span><span class="sxs-lookup"><span data-stu-id="cb572-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="cb572-308">Poiché si tratta di un server di prova, aggiungere l'utente hello toohello direttamente i database di in memoria.</span><span class="sxs-lookup"><span data-stu-id="cb572-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="cb572-309">Proteggere gli endpoint</span><span class="sxs-lookup"><span data-stu-id="cb572-309">Protect endpoints</span></span>
<span data-ttu-id="cb572-310">Proteggere gli endpoint specificando hello **passport.authenticate()** chiamata con protocollo hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="cb572-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="cb572-311">È possibile modificare la route nel codice del server per un'opzione più avanzata:</span><span class="sxs-lookup"><span data-stu-id="cb572-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="cb572-312">18: Eseguire nuovamente l'applicazione server</span><span class="sxs-lookup"><span data-stu-id="cb572-312">18: Run your server application again</span></span>
<span data-ttu-id="cb572-313">Usare curl nuovamente toosee se si dispone di OAuth 2.0 protezione contro gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb572-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="cb572-314">Eseguire questa operazione prima di usare uno qualsiasi degli SDK client in questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb572-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="cb572-315">intestazioni Hello restituite dovrebbero essere se l'autenticazione funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="cb572-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="cb572-316">Assicurarsi che l'istanza di MongoDB sia in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="cb572-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="cb572-317">Modificare toohello **azuread** directory, quindi usare curl:</span><span class="sxs-lookup"><span data-stu-id="cb572-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="cb572-318">Provare un'operazione POST di base:</span><span class="sxs-lookup"><span data-stu-id="cb572-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="cb572-319">Una risposta 401 indica il livello di Passport hello tenta tooredirect toohello autorizza un endpoint, che è esattamente quello desiderato.</span><span class="sxs-lookup"><span data-stu-id="cb572-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="cb572-320">*Ora è disponibile un servizio API REST che usa OAuth 2.0*.</span><span class="sxs-lookup"><span data-stu-id="cb572-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="cb572-321">Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb572-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="cb572-322">A tale scopo, sarà necessario tooreview un'esercitazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="cb572-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb572-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb572-323">Next steps</span></span>
<span data-ttu-id="cb572-324">Per riferimento, l'esempio hello completata (senza i valori di configurazione) viene fornito come [un file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cb572-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="cb572-325">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="cb572-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="cb572-326">A questo punto, è possibile passare argomenti avanzati toomore.</span><span class="sxs-lookup"><span data-stu-id="cb572-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="cb572-327">Potrebbe essere necessario tootry [proteggere un'app web Node. js utilizzando hello v 2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="cb572-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="cb572-328">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="cb572-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="cb572-329">Guida per sviluppatori Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="cb572-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="cb572-330">StackOverflow: tag "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="cb572-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="cb572-331">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="cb572-331">Get security updates for our products</span></span>
<span data-ttu-id="cb572-332">Che incoraggia la collaborazione toosign backup toobe notificate quando si verificano eventi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="cb572-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="cb572-333">In hello [notifiche sulla sicurezza Microsoft](https://technet.microsoft.com/security/dd252948) pagina, la sottoscrizione di avvisi advisory tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="cb572-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

