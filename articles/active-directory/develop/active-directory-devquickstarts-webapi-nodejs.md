---
title: aaaAzure AD Node.js introduzione | Documenti Microsoft
description: Come toobuild un'API web Node. js REST che si integra con Azure AD per l'autenticazione.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="6de88-103">Introduzione alle API Web per Node.js</span><span class="sxs-lookup"><span data-stu-id="6de88-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6de88-104">*Passport* è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="6de88-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="6de88-105">Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o Restify applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6de88-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="6de88-106">Una gamma completa di strategie supporta l'autenticazione con nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="6de88-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6de88-107">È stata sviluppata una strategia per Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6de88-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6de88-108">È installare il modulo e quindi aggiungere hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="6de88-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="6de88-109">toodo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6de88-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="6de88-110">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6de88-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="6de88-111">Configurare l'app toouse Passport `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="6de88-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="6de88-112">Configurare un client applicazione toocall hello tooDo API web elenco.</span><span class="sxs-lookup"><span data-stu-id="6de88-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="6de88-113">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="6de88-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="6de88-114">In questo articolo non copre come tooimplement Accedi, effettua l'iscrizione, o profilo di gestione con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="6de88-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="6de88-115">Si concentra sulle API web chiamante dopo hello è già autenticato.</span><span class="sxs-lookup"><span data-stu-id="6de88-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="6de88-116">È consigliabile iniziare con [come toointegrate con documenti di Azure Active Directory](active-directory-how-to-integrate.md) toolearn sui concetti di base di hello di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="6de88-117">È stato rilasciato tutto il codice sorgente hello per questo esempio in esecuzione in GitHub in base a una licenza MIT, pertanto è possibile tooclone disponibile (o ancora meglio, divisione) e fornire commenti e suggerimenti e le richieste pull.</span><span class="sxs-lookup"><span data-stu-id="6de88-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="6de88-118">Informazioni sui moduli Node.js</span><span class="sxs-lookup"><span data-stu-id="6de88-118">About Node.js modules</span></span>
<span data-ttu-id="6de88-119">In questa procedura dettagliata vengono usati i moduli Node.js.</span><span class="sxs-lookup"><span data-stu-id="6de88-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="6de88-120">I moduli sono pacchetti JavaScript caricabili che forniscono funzionalità specifiche per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="6de88-121">È in genere installare moduli utilizzando uno strumento da riga di comando di NPM Node.js hello nella directory di installazione NPM hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="6de88-122">Tuttavia, alcuni moduli, ad esempio modulo HTTP hello, sono inclusi nel pacchetto di Node.js di hello core.</span><span class="sxs-lookup"><span data-stu-id="6de88-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="6de88-123">I moduli installati vengono salvati in hello **node_modules** directory principale di hello della directory di installazione di Node.js.</span><span class="sxs-lookup"><span data-stu-id="6de88-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="6de88-124">Ogni modulo in hello **node_modules** directory mantiene il proprio **node_modules** directory che contiene tutti i moduli da cui dipende.</span><span class="sxs-lookup"><span data-stu-id="6de88-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="6de88-125">Ogni modulo necessario ha una directory **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="6de88-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="6de88-126">Questa struttura di directory ricorsiva rappresenta la catena di dipendenze hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="6de88-127">Questa struttura della catena di dipendenze comporta un footprint maggiore delle applicazioni,</span><span class="sxs-lookup"><span data-stu-id="6de88-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="6de88-128">Tuttavia, garantisce inoltre che tutte le dipendenze siano soddisfatti e che tale versione di hello dei moduli hello utilizzato in fase di sviluppo viene utilizzato anche nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6de88-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="6de88-129">Questo rende più prevedibile un comportamento dell'app produzione hello ed evita i problemi di controllo delle versioni che potrebbero interessare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="6de88-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="6de88-130">Passaggio 1: Registrare un tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6de88-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="6de88-131">toouse questo esempio, è necessario un tenant Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="6de88-132">Se non si conosce il tenant è o tooget uno, vedere [come tooget un Azure AD tenant](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6de88-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="6de88-133">Passaggio 2:Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="6de88-133">Step 2: Create an application</span></span>
<span data-ttu-id="6de88-134">Successivamente si crea un'applicazione nella directory di Azure AD offre informazioni talmente toosecurely di comunicare con l'app.</span><span class="sxs-lookup"><span data-stu-id="6de88-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="6de88-135">App client hello sia API web sono rappresentate da una singola **ID applicazione** in questo caso, poiché comprendono una sola app logica.</span><span class="sxs-lookup"><span data-stu-id="6de88-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="6de88-136">toocreate un'app, seguire [queste istruzioni](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="6de88-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="6de88-137">Se si compila un'app line-of-business, [queste istruzioni aggiuntive](../active-directory-applications-guiding-developers-for-lob-applications.md) possono risultare utili.</span><span class="sxs-lookup"><span data-stu-id="6de88-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="6de88-138">toocreate un'applicazione:</span><span class="sxs-lookup"><span data-stu-id="6de88-138">toocreate an application:</span></span>

1. <span data-ttu-id="6de88-139">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6de88-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6de88-140">Nel menu superiore hello, selezionare l'account.</span><span class="sxs-lookup"><span data-stu-id="6de88-140">On hello top menu, select your account.</span></span> <span data-ttu-id="6de88-141">Quindi, in hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="6de88-142">Dal menu hello hello sinistra, selezionare **più servizi**, quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6de88-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="6de88-143">Selezionare **Registrazioni per l'app**, quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6de88-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="6de88-144">Seguire hello richieste toocreate un **applicazione Web e/o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="6de88-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="6de88-145">Hello **nome** di hello applicazione descrive tooend utenti applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="6de88-146">Hello **Sign-On URL** hello URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="6de88-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="6de88-147">URL del codice di esempio hello predefinito è Hello `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="6de88-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="6de88-148">Dopo la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="6de88-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="6de88-149">Questo valore è necessario in hello nelle sezioni seguenti, quindi copiarlo dalla pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="6de88-150">Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App.</span><span class="sxs-lookup"><span data-stu-id="6de88-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="6de88-151">Hello **URI ID App** è un identificatore univoco per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="6de88-152">convenzione di Hello è toouse `https://<tenant-domain>/<app-name>`, ad esempio: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="6de88-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="6de88-153">Creare un **chiave** per l'applicazione dalla hello **impostazioni** pagina e quindi copiarlo in un punto.</span><span class="sxs-lookup"><span data-stu-id="6de88-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="6de88-154">perché verrà richiesta a breve.</span><span class="sxs-lookup"><span data-stu-id="6de88-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="6de88-155">Passaggio 3: Scaricare Node.js per la piattaforma corrente</span><span class="sxs-lookup"><span data-stu-id="6de88-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="6de88-156">toosuccessfully usare questo esempio, è necessario disporre di un'installazione funzionante di Node.js.</span><span class="sxs-lookup"><span data-stu-id="6de88-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="6de88-157">Installare Node.js da [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6de88-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="6de88-158">Passaggio 4: Installare MongoDB nella piattaforma</span><span class="sxs-lookup"><span data-stu-id="6de88-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="6de88-159">toosuccessfully usare questo esempio, è necessario disporre di un'installazione funzionante di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6de88-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="6de88-160">Utilizzare MongoDB toomake hello API REST persistente tra istanze del server.</span><span class="sxs-lookup"><span data-stu-id="6de88-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="6de88-161">Installare MongoDB da [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="6de88-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="6de88-162">Questa procedura dettagliata si presuppone che si gli endpoint di installazione e il server predefinito hello per MongoDB, che in fase di hello di questo articolo è mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="6de88-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="6de88-163">Passaggio 5: Installare i moduli Restify hello in web API</span><span class="sxs-lookup"><span data-stu-id="6de88-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="6de88-164">Si sta usando Restify toobuild API REST.</span><span class="sxs-lookup"><span data-stu-id="6de88-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="6de88-165">Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express,</span><span class="sxs-lookup"><span data-stu-id="6de88-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="6de88-166">che include una gamma completa di funzionalità per la compilazione di API REST basate su Connect.</span><span class="sxs-lookup"><span data-stu-id="6de88-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="6de88-167">Installare Restify</span><span class="sxs-lookup"><span data-stu-id="6de88-167">Install Restify</span></span>
1. <span data-ttu-id="6de88-168">Dalla riga di comando hello, modificare le directory toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="6de88-169">Se hello **azuread** directory non esiste, crearla.</span><span class="sxs-lookup"><span data-stu-id="6de88-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="6de88-170">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6de88-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="6de88-171">Questo comando installa Restify.</span><span class="sxs-lookup"><span data-stu-id="6de88-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="6de88-172">È stato visualizzato un errore?</span><span class="sxs-lookup"><span data-stu-id="6de88-172">Did you get an error?</span></span>
<span data-ttu-id="6de88-173">Quando si usa NPM in alcuni sistemi operativi, potrebbe essere visualizzato il messaggio di errore **Error: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="6de88-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="6de88-174">e un suggerimento che si tenta di account hello in esecuzione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6de88-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="6de88-175">In questo caso, è possibile utilizzare hello sudo comando toorun NPM a un livello di privilegio superiore.</span><span class="sxs-lookup"><span data-stu-id="6de88-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="6de88-176">È stato visualizzato un errore relativo a DTrace?</span><span class="sxs-lookup"><span data-stu-id="6de88-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="6de88-177">Durante l'installazione di Restify, potrebbe essere visualizzato un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6de88-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="6de88-178">Restify offre un meccanismo efficace per tenere traccia delle chiamate REST usando DTrace.</span><span class="sxs-lookup"><span data-stu-id="6de88-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="6de88-179">Tuttavia, per molti sistemi operativi DTrace non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6de88-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="6de88-180">È possibile ignorare questi errori.</span><span class="sxs-lookup"><span data-stu-id="6de88-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="6de88-181">output di Hello di questo comando dovrebbe essere simile toohello seguente output:</span><span class="sxs-lookup"><span data-stu-id="6de88-181">hello output of this command should look similar toohello following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="6de88-182">Passaggio 6: Installare Passport.js nell'API Web</span><span class="sxs-lookup"><span data-stu-id="6de88-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="6de88-183">[Passport](http://passportjs.org/) è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="6de88-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="6de88-184">Flessibile e modulari, Passport possono essere eliminati in modo discreto in tooany basati su Express o Restify applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6de88-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="6de88-185">Una gamma completa di strategie supporta l'autenticazione con nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="6de88-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="6de88-186">È stata sviluppata una strategia per Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="6de88-187">Si installa il modulo e quindi aggiunta strategia di Azure Active Directory hello plug-in.</span><span class="sxs-lookup"><span data-stu-id="6de88-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="6de88-188">Dalla riga di comando hello, modificare le directory toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="6de88-189">passport.js tooinstall, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6de88-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="6de88-190">output di Hello del comando hello dovrebbe essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6de88-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="6de88-191">Passaggio 7: Aggiungere AD di Azure di Passport tooyour web API</span><span class="sxs-lookup"><span data-stu-id="6de88-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="6de88-192">Questo punto verranno aggiunte strategia OAuth hello utilizzando `passport-azure-ad`, una suite di strategie che si connettono tooPassport Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="6de88-193">In questo esempio di API REST tale strategia viene usata per i token di connessione.</span><span class="sxs-lookup"><span data-stu-id="6de88-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="6de88-194">Anche se OAuth2 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, i più diffusi sono solo alcuni.</span><span class="sxs-lookup"><span data-stu-id="6de88-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="6de88-195">I token di connessione sono token di hello più comunemente usato per la protezione di endpoint.</span><span class="sxs-lookup"><span data-stu-id="6de88-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="6de88-196">Si tratta di tipo hello maggiormente emesso del token in OAuth2.</span><span class="sxs-lookup"><span data-stu-id="6de88-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="6de88-197">Molte implementazioni presuppongono che i token di connessione sono hello unico tipo di token rilasciati.</span><span class="sxs-lookup"><span data-stu-id="6de88-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="6de88-198">Dalla riga di comando hello, modificare le directory toohello **azuread** directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="6de88-199">Comando che segue hello di tipo hello tooinstall Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="6de88-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="6de88-200">output di Hello del comando hello dovrebbe essere simile toohello seguente output:</span><span class="sxs-lookup"><span data-stu-id="6de88-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="6de88-201">Passaggio 8: Aggiungere MongoDB moduli tooyour web API</span><span class="sxs-lookup"><span data-stu-id="6de88-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="6de88-202">MongoDB viene usato come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="6de88-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="6de88-203">Per questo motivo, è necessario tooinstall hello ampiamente utilizzato nei modelli di plug-in chiamati Mongoose toomanage e schemi.</span><span class="sxs-lookup"><span data-stu-id="6de88-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="6de88-204">È anche necessario driver di database hello tooinstall per MongoDB (denominato anche MongoDB).</span><span class="sxs-lookup"><span data-stu-id="6de88-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="6de88-205">Passaggio 9: Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="6de88-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="6de88-206">È quindi possibile installare hello rimanenti moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="6de88-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="6de88-207">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-208">Immettere hello seguenti comandi tooinstall questi moduli nel **node_modules** directory:</span><span class="sxs-lookup"><span data-stu-id="6de88-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="6de88-209">Passaggio 10: Creare un file server.js con le dipendenze</span><span class="sxs-lookup"><span data-stu-id="6de88-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="6de88-210">file server.js Hello fornisce la maggior parte delle funzionalità di hello per l'API del server web.</span><span class="sxs-lookup"><span data-stu-id="6de88-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="6de88-211">Aggiungere la maggior parte dei file di toothis il nostro codice.</span><span class="sxs-lookup"><span data-stu-id="6de88-211">We add most of our code toothis file.</span></span> <span data-ttu-id="6de88-212">Ai fini della produzione, è consigliabile eseguire il refactoring funzionalità hello in file più piccoli, ad esempio route distinte e controller.</span><span class="sxs-lookup"><span data-stu-id="6de88-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="6de88-213">In questa dimostrazione si usa server.js per questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6de88-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="6de88-214">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-215">Creare un `server.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6de88-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="6de88-216">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-216">Save hello file.</span></span> <span data-ttu-id="6de88-217">Tooit sarà restituiamo a breve.</span><span class="sxs-lookup"><span data-stu-id="6de88-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="6de88-218">Passaggio 11: Creare un toostore di file di configurazione delle impostazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6de88-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="6de88-219">Questo file di codice passa i parametri di configurazione hello dal tooPassport.js del portale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6de88-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="6de88-220">Questi valori di configurazione è stato creato quando è stato aggiunto portale toohello API web di hello nella prima parte di hello della procedura dettagliata hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="6de88-221">Viene descritto il tooput in valori hello di questi parametri dopo aver copiato il codice hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="6de88-222">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-223">Creare un `config.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6de88-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="6de88-224">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="6de88-225">Passaggio 12: Aggiunta di file di configurazione valori tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="6de88-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="6de88-226">È necessario tooread questi valori dal file config hello creato attraverso l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="6de88-227">toodo, aggiungiamo file hello. config come una risorsa necessaria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="6de88-228">Quindi impostiamo hello globale toomatch hello variabili nel documento config.js hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="6de88-229">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-230">Aprire il `server.js` file in un editor qualsiasi e quindi aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6de88-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="6de88-231">Quindi aggiungere una nuova sezione troppo`server.js` con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="6de88-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="6de88-232">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="6de88-233">Passaggio 13: Aggiunta di hello MongoDB modello e le informazioni tramite Mongoose</span><span class="sxs-lookup"><span data-stu-id="6de88-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="6de88-234">Ora tutti questa preparazione in corso toostart estinzione come questi tre file vengono combinati in un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="6de88-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="6de88-235">Questa procedura dettagliata, utilizziamo MongoDB toostore l'attività come descritto nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="6de88-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="6de88-236">In hello `config.js` file che abbiamo creato nel passaggio 11, viene chiamato dal database `tasklist`, perché questo è ciò che è stato inserito alla fine di hello del nostro **mogoose_auth_local** URL di connessione.</span><span class="sxs-lookup"><span data-stu-id="6de88-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="6de88-237">Non è necessario toocreate questo database in anticipo in MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6de88-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="6de88-238">Al contrario, MongoDB crea questo per noi in hello prima esecuzione dell'applicazione server (supponendo che il database hello non esiste già).</span><span class="sxs-lookup"><span data-stu-id="6de88-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="6de88-239">Ora che è stato indicato server hello quale database MongoDB desideriamo toouse, abbiamo bisogno di toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.</span><span class="sxs-lookup"><span data-stu-id="6de88-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="6de88-240">Descrizione del modello di hello</span><span class="sxs-lookup"><span data-stu-id="6de88-240">Discussion of hello model</span></span>
<span data-ttu-id="6de88-241">Questo modello di schema è semplice</span><span class="sxs-lookup"><span data-stu-id="6de88-241">Our schema model is simple.</span></span> <span data-ttu-id="6de88-242">ed è possibile espanderlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="6de88-242">You expand it as required.</span></span>

<span data-ttu-id="6de88-243">NOME: il nome di hello della persona hello toohello attività assegnata.</span><span class="sxs-lookup"><span data-stu-id="6de88-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="6de88-244">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="6de88-244">A **String**.</span></span>

<span data-ttu-id="6de88-245">: Hello attività stessa.</span><span class="sxs-lookup"><span data-stu-id="6de88-245">TASK: hello task itself.</span></span> <span data-ttu-id="6de88-246">Valore **stringa**.</span><span class="sxs-lookup"><span data-stu-id="6de88-246">A **String**.</span></span>

<span data-ttu-id="6de88-247">: Hello Data attività hello viene scadenza.</span><span class="sxs-lookup"><span data-stu-id="6de88-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="6de88-248">Valore **datetime**.</span><span class="sxs-lookup"><span data-stu-id="6de88-248">A **DATETIME**.</span></span>

<span data-ttu-id="6de88-249">COMPLETATA: Se l'attività hello è completata o non.</span><span class="sxs-lookup"><span data-stu-id="6de88-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="6de88-250">Valore **booleano**.</span><span class="sxs-lookup"><span data-stu-id="6de88-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="6de88-251">Creazione di schema hello in codice hello</span><span class="sxs-lookup"><span data-stu-id="6de88-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="6de88-252">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-253">Aprire il `server.js` file in un editor qualsiasi e quindi aggiungere le seguenti informazioni di sotto la voce di configurazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="6de88-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="6de88-254">Come si può vedere dal codice hello, abbiamo creato prima il nostro schema.</span><span class="sxs-lookup"><span data-stu-id="6de88-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="6de88-255">Quindi si crea un oggetto modello utilizziamo toostore i dati in tutto hello codice quando si definisce il nostro **route**.</span><span class="sxs-lookup"><span data-stu-id="6de88-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="6de88-256">Passaggio 14: Aggiungere le route per il server API REST delle attività</span><span class="sxs-lookup"><span data-stu-id="6de88-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="6de88-257">Ora che è disponibile un toowork del modello di database con, aggiungere route hello è in corso utilizzare per i server API REST.</span><span class="sxs-lookup"><span data-stu-id="6de88-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="6de88-258">Informazioni sulle route in Restify</span><span class="sxs-lookup"><span data-stu-id="6de88-258">About routes in Restify</span></span>
<span data-ttu-id="6de88-259">Le route funzionano in hello Restify stesso modo che in hello Express dello stack.</span><span class="sxs-lookup"><span data-stu-id="6de88-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="6de88-260">Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="6de88-261">Le route si definiscono di solito in un file separato.</span><span class="sxs-lookup"><span data-stu-id="6de88-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="6de88-262">A questo scopo, la route è inserito nel file server.js hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="6de88-263">È consigliabile inserirle in un file a parte per usarle in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="6de88-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="6de88-264">Di seguito è riportato un modello tipico per una route Restify:</span><span class="sxs-lookup"><span data-stu-id="6de88-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="6de88-265">Si tratta hello modello al livello più elementare.</span><span class="sxs-lookup"><span data-stu-id="6de88-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="6de88-266">Restify ed Express offrono funzionalità molto più avanzate, ad esempio la definizione di tipi di applicazione e l'esecuzione di un routing complesso tra endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="6de88-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="6de88-267">Ai fini di questa procedura dettagliata, vengono usate route semplici.</span><span class="sxs-lookup"><span data-stu-id="6de88-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="6de88-268">Aggiungere server tooour di route predefinita</span><span class="sxs-lookup"><span data-stu-id="6de88-268">Add default routes tooour server</span></span>
<span data-ttu-id="6de88-269">È ora aggiungere hello route CRUD di base di creazione, recupero, aggiornamento ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="6de88-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="6de88-270">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente:</span><span class="sxs-lookup"><span data-stu-id="6de88-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="6de88-271">Aprire hello `server.js` file in un editor qualsiasi e quindi aggiungere le seguenti informazioni di sotto di voci del database precedente hello apportate hello:</span><span class="sxs-lookup"><span data-stu-id="6de88-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="6de88-272">Aggiungere la gestione degli errori nelle API</span><span class="sxs-lookup"><span data-stu-id="6de88-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="6de88-273">Passaggio 15: Creare il server</span><span class="sxs-lookup"><span data-stu-id="6de88-273">Step 15: Create your server</span></span>
<span data-ttu-id="6de88-274">Ora che il database è stato definito e le route sono state aggiunte,</span><span class="sxs-lookup"><span data-stu-id="6de88-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="6de88-275">Hello ultima operazione toodo aggiungere istanza hello del server che gestisce delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="6de88-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="6de88-276">Restify (e Express) è possibile eseguire una grande quantità di personalizzazione per un server API REST, ma verrà nuovamente il programma di installazione di toouse hello più semplice a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="6de88-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="6de88-277">Passaggio 16: Aggiungere server di toohello route hello (senza autenticazione per il momento)</span><span class="sxs-lookup"><span data-stu-id="6de88-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="6de88-278">Passaggio 17: Eseguire server hello (prima dell'aggiunta del supporto di OAuth)</span><span class="sxs-lookup"><span data-stu-id="6de88-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="6de88-279">Testare il server prima di aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="6de88-280">tootest modo più semplice Hello del server è tramite curl in una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6de88-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="6de88-281">Prima di procedere è dobbiamo un'utilità che consente di elaborare tooparse output in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6de88-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="6de88-282">Installare hello strumento JSON (hello tutti i seguenti esempi di questo strumento) seguenti:</span><span class="sxs-lookup"><span data-stu-id="6de88-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="6de88-283">Vengono installati lo strumento JSON hello a livello globale.</span><span class="sxs-lookup"><span data-stu-id="6de88-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="6de88-284">Ora che è stato portato a termine che, di seguito riprodurre con server hello:</span><span class="sxs-lookup"><span data-stu-id="6de88-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="6de88-285">Assicurarsi prima di tutto che l'istanza di MongoDB sia in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="6de88-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="6de88-286">Quindi, modificare la directory toohello e avviare per:</span><span class="sxs-lookup"><span data-stu-id="6de88-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="6de88-287">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="6de88-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="6de88-288">Ora è possibile aggiungere un'attività in questo modo:</span><span class="sxs-lookup"><span data-stu-id="6de88-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="6de88-289">risposta Hello deve essere:</span><span class="sxs-lookup"><span data-stu-id="6de88-289">hello response should be:</span></span>

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
    <span data-ttu-id="6de88-290">È anche possibile elencare le attività di Brandon in questo modo:</span><span class="sxs-lookup"><span data-stu-id="6de88-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="6de88-291">Se tutto funziona, siamo tooadd pronto OAuth toohello API REST del server.</span><span class="sxs-lookup"><span data-stu-id="6de88-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="6de88-292">Ora si dispone di un'API REST con MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6de88-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="6de88-293">Passaggio 18: Aggiunta di server API REST di autenticazione tooour</span><span class="sxs-lookup"><span data-stu-id="6de88-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="6de88-294">Ora che l'API REST è in esecuzione è possibile iniziare a usarla con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6de88-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="6de88-295">Dalla riga di comando hello, modificare le directory toohello **azuread** cartella se non si è già presente.</span><span class="sxs-lookup"><span data-stu-id="6de88-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="6de88-296">Utilizzare hello OIDCBearerStrategy inclusa passport-azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6de88-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="6de88-297">Nei passaggi precedenti è stato creato un tipico server REST TODO senza alcun tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="6de88-298">Questa operazione è stata eseguita nel modo indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6de88-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="6de88-299">Innanzitutto, è necessario che si desidera toouse Passport tooindicate.</span><span class="sxs-lookup"><span data-stu-id="6de88-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="6de88-300">Inserire il codice subito dopo la configurazione dell'altro server:</span><span class="sxs-lookup"><span data-stu-id="6de88-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="6de88-301">Quando si scrivono le API, è consigliabile collegare sempre toosomething dati hello univoco da token hello hello utente non può effettuare lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="6de88-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="6de88-302">Quando il server archivia elementi TODO, li archivia in base all'ID di oggetto hello dell'utente hello nel token hello (chiamati tramite token.oid), che è stato inserito nel campo "proprietario" hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="6de88-303">In questo modo, solo l'utente può accedere ai relativi elementi TODO.</span><span class="sxs-lookup"><span data-stu-id="6de88-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="6de88-304">Non è non presenti rischi in hello API di "proprietario", un utente esterno può richiedere hello TODOs di altri utenti, anche se vengono autenticati.</span><span class="sxs-lookup"><span data-stu-id="6de88-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="6de88-305">Avanti utilizziamo strategia connessione hello fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="6de88-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="6de88-306">Esaminare il codice hello per il momento e spiega rest hello a breve.</span><span class="sxs-lookup"><span data-stu-id="6de88-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="6de88-307">Inserire il codice seguente dopo quanto incollato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="6de88-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="6de88-308">Passport usa un modello simile per tutte le strategie (Twitter, Facebook e così via) seguite dagli scrittori della strategia.</span><span class="sxs-lookup"><span data-stu-id="6de88-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="6de88-309">Esaminando la strategia di hello, vedere che vengono passati una funzione che ha un token e un fatto come parametri hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="6de88-310">strategia di Hello proviene toous nuovamente dopo che esegue il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="6de88-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="6de88-311">Dopo questo caso, vengono archiviati utente hello e token hello stash in modo non dobbiamo tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6de88-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6de88-312">il codice precedente di Hello in tutti gli utenti che si verificano tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="6de88-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="6de88-313">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="6de88-313">This is known as auto-registration.</span></span> <span data-ttu-id="6de88-314">Nei server di produzione è preferibile non consentire l'accesso a chiunque senza prima prevedere un processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="6de88-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="6de88-315">Si tratta in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6de88-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="6de88-316">Se questo non è un programma della riga di comando, è possibile estrarre posta elettronica hello dall'oggetto token hello è restituito e quindi richiesto hello utente toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6de88-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="6de88-317">Poiché si tratta di un server di prova, è sufficiente aggiungerli database in memoria toohello.</span><span class="sxs-lookup"><span data-stu-id="6de88-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="6de88-318">Proteggere alcuni endpoint</span><span class="sxs-lookup"><span data-stu-id="6de88-318">Protect some endpoints</span></span>
<span data-ttu-id="6de88-319">Proteggere gli endpoint specificando hello `passport.authenticate()` chiamata con protocollo hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="6de88-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="6de88-320">il codice server effettuare ulteriori qualcosa di interessante, toomake Modifica route hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="6de88-321">Passaggio 19: Eseguire nuovamente l'applicazione server e assicurarsi che rifiuti l'utente</span><span class="sxs-lookup"><span data-stu-id="6de88-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="6de88-322">Consente di usare `curl` nuovamente toosee se OAuth2 protection è ora disponibile su questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="6de88-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="6de88-323">Eseguire il test prima di eseguire qualsiasi SDK client in questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="6de88-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="6de88-324">Hello intestazioni che vengono restituite devono essere sufficiente tootell ci se verrà percorso corretto hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="6de88-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="6de88-325">Assicurarsi prima di tutto che l'istanza di MongoDB sia in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="6de88-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="6de88-326">Quindi, modificare la directory toohello e avviare per.</span><span class="sxs-lookup"><span data-stu-id="6de88-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="6de88-327">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="6de88-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="6de88-328">Provare un'operazione POST di base.</span><span class="sxs-lookup"><span data-stu-id="6de88-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="6de88-329">401 è risposta hello che si sta cercando di seguito.</span><span class="sxs-lookup"><span data-stu-id="6de88-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="6de88-330">Questa risposta indica che il livello di Passport hello sta cercando tooredirect toohello autorizzato endpoint, che è esattamente quello desiderato.</span><span class="sxs-lookup"><span data-stu-id="6de88-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6de88-331">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6de88-331">Next steps</span></span>
<span data-ttu-id="6de88-332">Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="6de88-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="6de88-333">Sarà necessario toogo tramite una procedura dettagliata di aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="6de88-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="6de88-334">Dopo avere appreso come tooimplement un'API REST tramite Restify e OAuth2.</span><span class="sxs-lookup"><span data-stu-id="6de88-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="6de88-335">È inoltre più che sufficiente tookeep codice lo sviluppo del servizio e di apprendimento come toobuild in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6de88-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="6de88-336">Se si è interessati in passaggi successivi hello in consentirti di ADAL, ecco alcuni client ADAL supportati, è consigliabile che continuare a lavorare con.</span><span class="sxs-lookup"><span data-stu-id="6de88-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="6de88-337">Clonare computer dello sviluppatore tooyour verso il basso e configurare come descritto nella procedura dettagliata hello.</span><span class="sxs-lookup"><span data-stu-id="6de88-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="6de88-338">ADAL per iOS</span><span class="sxs-lookup"><span data-stu-id="6de88-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="6de88-339">ADAL per Android</span><span class="sxs-lookup"><span data-stu-id="6de88-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
