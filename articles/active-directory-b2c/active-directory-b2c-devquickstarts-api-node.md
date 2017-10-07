---
title: 'Azure AD B2C: proteggere un''API Web usando Node.js | Microsoft Docs'
description: Come toobuild un Node.js web API che accetta i token da un tenant B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="6b0ff-103">Azure AD B2C: proteggere un'API Web usando Node.js</span><span class="sxs-lookup"><span data-stu-id="6b0ff-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="6b0ff-104">Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="6b0ff-105">Questi token consentono le app client che usano Azure Active Directory B2C tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="6b0ff-106">Questo articolo illustra come toocreate un'API "elenco" che consente agli utenti tooadd ed elenco attività.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="6b0ff-107">API web Hello sia protetta con Azure Active Directory B2C e consente solo agli utenti autenticati toomanage proprio elenco di attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="6b0ff-108">In questo esempio è stata scritta utilizzando tooby toobe connesso il nostro [iOS B2C applicazione di esempio](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="6b0ff-109">Hello prima procedura dettagliata corrente e quindi proseguire con l'esempio in questione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="6b0ff-110">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="6b0ff-111">Estremamente flessibile e modulare, Passport può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="6b0ff-112">Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6b0ff-113">È stata sviluppata una strategia per Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6b0ff-114">Installare il modulo e quindi aggiungere hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="6b0ff-115">toodo in questo esempio, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="6b0ff-116">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="6b0ff-117">Configurare l'applicazione toouse Passport `azure-ad-passport` plug-in.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="6b0ff-118">Configurare un client applicazione toocall hello "elenco" API web.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="6b0ff-119">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6b0ff-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="6b0ff-120">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="6b0ff-121">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="6b0ff-122">Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="6b0ff-123">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="6b0ff-123">Create an application</span></span>
<span data-ttu-id="6b0ff-124">Successivamente, è necessario toocreate un'app nella directory B2C che offre Azure AD alcune informazioni che toosecurely deve comunicare con l'app.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="6b0ff-125">In questo caso, le app client hello e API web sono rappresentati da un singolo **ID applicazione**, poiché comprendono una sola app logica.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="6b0ff-126">toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="6b0ff-127">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-127">Be sure to:</span></span>

* <span data-ttu-id="6b0ff-128">Includere un **web app web e api** in un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="6b0ff-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="6b0ff-129">Immettere `http://localhost/TodoListService` come **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="6b0ff-130">È l'URL predefinito hello per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="6b0ff-131">Creare un **segreto applicazione** per l'applicazione e prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="6b0ff-132">Questi dati saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-132">You need this data later.</span></span> <span data-ttu-id="6b0ff-133">Si noti che questo valore deve toobe [XML sottoposto a escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) prima di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="6b0ff-134">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="6b0ff-135">Questi dati saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="6b0ff-136">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="6b0ff-136">Create your policies</span></span>
<span data-ttu-id="6b0ff-137">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6b0ff-138">Questa app contiene due esperienze di identità: iscrizione e accesso.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="6b0ff-139">È necessario toocreate un criterio di ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="6b0ff-140">Durante la creazione dei tre criteri assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="6b0ff-141">Scegliere hello **nome visualizzato** e altri attributi per l'abbonamento nel criterio di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="6b0ff-142">Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="6b0ff-143">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="6b0ff-144">Copia verso il basso hello **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="6b0ff-145">Devono contenere il prefisso hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="6b0ff-146">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="6b0ff-147">Dopo aver creato i tre criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="6b0ff-148">toolearn sul funzionamento dei criteri in Azure Active Directory B2C, iniziare con hello [.NET web app esercitazione introduttiva](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="6b0ff-149">Scaricare codice hello</span><span class="sxs-lookup"><span data-stu-id="6b0ff-149">Download hello code</span></span>
<span data-ttu-id="6b0ff-150">Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="6b0ff-151">esempio hello toobuild come si go, è possibile [scaricare un progetto di base come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="6b0ff-152">È anche possibile clonare scheletro hello:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="6b0ff-153">è anche l'applicazione Hello completato [disponibile come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) o hello `complete` ramo di hello stesso repository.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="6b0ff-154">Scaricare node.js per la piattaforma corrente</span><span class="sxs-lookup"><span data-stu-id="6b0ff-154">Download Node.js for your platform</span></span>
<span data-ttu-id="6b0ff-155">toosuccessfully usare questo esempio, è necessario un'installazione funzionante di Node.js.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="6b0ff-156">Installare Node.js da [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="6b0ff-157">Installare MongoDB per la piattaforma corrente</span><span class="sxs-lookup"><span data-stu-id="6b0ff-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="6b0ff-158">toosuccessfully usare questo esempio, è necessario un'installazione funzionante di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="6b0ff-159">Utilizziamo MongoDB toomake l'API REST persistente tra istanze del server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="6b0ff-160">Installare MongoDB da [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="6b0ff-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="6b0ff-161">Questa procedura dettagliata si presuppone che si gli endpoint di installazione e il server predefinito hello per MongoDB, ovvero al momento hello `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="6b0ff-162">Installare i moduli Restify hello in web API</span><span class="sxs-lookup"><span data-stu-id="6b0ff-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="6b0ff-163">Utilizziamo Restify toobuild l'API REST.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="6b0ff-164">Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express,</span><span class="sxs-lookup"><span data-stu-id="6b0ff-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="6b0ff-165">che include una gamma completa di funzionalità per la compilazione di API REST basate su Connect.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="6b0ff-166">Installare Restify</span><span class="sxs-lookup"><span data-stu-id="6b0ff-166">Install Restify</span></span>
<span data-ttu-id="6b0ff-167">Dalla riga di comando hello, impostare la directory troppo`azuread`.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="6b0ff-168">Se hello `azuread` directory non esiste, crearla.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="6b0ff-169">`cd azuread` oppure `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="6b0ff-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="6b0ff-170">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="6b0ff-171">Questo comando installa Restify.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="6b0ff-172">È stato visualizzato un errore?</span><span class="sxs-lookup"><span data-stu-id="6b0ff-172">Did you get an error?</span></span>
<span data-ttu-id="6b0ff-173">In alcuni sistemi operativi, quando si utilizza `npm`, è possibile che venga visualizzato l'errore hello `Error: EPERM, chmod '/usr/local/bin/..'` e una richiesta di account hello eseguire come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="6b0ff-174">Se si verifica questo problema, utilizzare hello `sudo` toorun comando `npm` a un livello di privilegio superiore.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="6b0ff-175">È stato visualizzato un errore di DTrace?</span><span class="sxs-lookup"><span data-stu-id="6b0ff-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="6b0ff-176">Durante l'installazione di Restify potrebbe essere visualizzato un testo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="6b0ff-177">Restify offre un meccanismo efficace per tenere traccia delle chiamate REST usando DTrace.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="6b0ff-178">Tuttavia, per molti sistemi operativi DTrace non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="6b0ff-179">È possibile ignorare questi errori.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="6b0ff-180">testo toothis simile viene visualizzato un output di Hello del comando hello:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="6b0ff-181">Installare Passport nell'API Web</span><span class="sxs-lookup"><span data-stu-id="6b0ff-181">Install Passport in your web API</span></span>
<span data-ttu-id="6b0ff-182">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="6b0ff-183">Installare Passport utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="6b0ff-184">output di Hello del comando hello deve essere un testo simile toothis:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="6b0ff-185">Aggiungere passport azuread tooyour web API</span><span class="sxs-lookup"><span data-stu-id="6b0ff-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="6b0ff-186">Successivamente, aggiungere strategia OAuth hello utilizzando `passport-azuread`, una suite di strategie che si connettono AD Azure con Passport.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="6b0ff-187">Usare questa strategia per i token di connessione di esempio di API REST hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="6b0ff-188">Anche se OAuth2 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, solo determinati tipi di token sono usati su larga scala.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="6b0ff-189">i token di Hello per la protezione di endpoint sono token di connessione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="6b0ff-190">Questi tipi di token sono hello maggiormente emesso in OAuth2.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="6b0ff-191">Molte implementazioni presuppongono che i token di connessione sono hello unico tipo di token rilasciato.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="6b0ff-192">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="6b0ff-193">Installare hello Passport `passport-azure-ad` modulo tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="6b0ff-194">output di Hello del comando hello deve essere un testo simile toothis:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="6b0ff-195">Aggiungere MongoDB moduli tooyour web API</span><span class="sxs-lookup"><span data-stu-id="6b0ff-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="6b0ff-196">Questo esempio usa MongoDB come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="6b0ff-197">A tale scopo installare Mongoose, un plug-in diffuso per la gestione di modelli e schemi.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="6b0ff-198">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="6b0ff-198">Install additional modules</span></span>
<span data-ttu-id="6b0ff-199">Installare quindi hello rimanenti moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="6b0ff-200">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-201">Installare i moduli hello il `node_modules` directory:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="6b0ff-202">Creare un file server.js con le dipendenze</span><span class="sxs-lookup"><span data-stu-id="6b0ff-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="6b0ff-203">Hello `server.js` file fornisce la maggior parte hello funzionalità hello per il server Web API.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="6b0ff-204">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-205">Creare un file `server.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="6b0ff-206">Aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="6b0ff-207">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-207">Save hello file.</span></span> <span data-ttu-id="6b0ff-208">Tornare tooit in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="6b0ff-209">Creare un toostore file config.js le impostazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0ff-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="6b0ff-210">Questo file di codice passa i parametri di configurazione hello da toohello il portale di Azure AD `Passport.js` file.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="6b0ff-211">Questi valori di configurazione è stato creato quando si aggiunta portale toohello API web di hello nella prima parte di hello di dimostrativo hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="6b0ff-212">Viene descritto il tooput in valori hello di questi parametri dopo aver copiato il codice hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="6b0ff-213">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-214">Creare un file `config.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="6b0ff-215">Aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="6b0ff-216">Valori richiesti</span><span class="sxs-lookup"><span data-stu-id="6b0ff-216">Required values</span></span>
<span data-ttu-id="6b0ff-217">`clientID`: hello ID client dell'applicazione Web API.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="6b0ff-218">`IdentityMetadata`: Questa opzione è quando `passport-azure-ad` cerca i dati di configurazione per il provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="6b0ff-219">Cerca anche hello chiavi toovalidate hello i token web JSON.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="6b0ff-220">`audience`: hello identificatore uniform resource identifier (URI) dal portale hello che identifica l'applicazione chiamante.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="6b0ff-221">`tenantName`: nome del tenant, ad esempio **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="6b0ff-222">`policyName`: hello criteri che si desidera token hello toovalidate entrano tooyour server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="6b0ff-223">Questo criterio deve essere hello stesso criterio usato in un'applicazione hello client per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="6b0ff-224">Per il momento, utilizzare hello stesso criteri attraverso il programma di installazione client e server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="6b0ff-225">Se sono stati già completati una panoramica e creato questi criteri, non è necessario toodo così nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="6b0ff-226">Poiché è stata completata la procedura dettagliata hello, occorre non deve tooset i nuovi criteri per procedure client nel sito di hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="6b0ff-227">Aggiungere file di configurazione tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="6b0ff-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="6b0ff-228">i valori hello tooread hello `config.js` file creata, aggiungere hello `.config` file come una risorsa necessaria nell'applicazione e quindi impostare toothose variabili globali hello in hello `config.js` documento.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="6b0ff-229">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-230">Aprire hello `server.js` file in un editor.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6b0ff-231">Aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="6b0ff-232">Aggiungere una nuova sezione troppo`server.js` che include hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="6b0ff-233">Successivamente, aggiungere alcuni segnaposto per gli utenti di hello riceviamo le applicazioni di chiamata.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="6b0ff-234">Creare anche il logger.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="6b0ff-235">Aggiungere le informazioni di modello e dello schema di MongoDB hello utilizzando Mongoose</span><span class="sxs-lookup"><span data-stu-id="6b0ff-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="6b0ff-236">Hello preparazione precedenti ripaga come connettere questi tre file in un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="6b0ff-237">Per questa procedura dettagliata, utilizzare MongoDB toostore le attività, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="6b0ff-238">In hello `config.js` file, è stato chiamato il database **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="6b0ff-239">Tale nome è stato anche gli elementi da inserire alla fine hello hello `mongoose_auth_local` URL di connessione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="6b0ff-240">Non è necessario toocreate questo database in anticipo in MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="6b0ff-241">Database di hello viene creato automaticamente alla prima esecuzione di hello dell'applicazione server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="6b0ff-242">Dopo che è indicare il server di hello quali toouse database MongoDB, è necessario toowrite alcuni modelli di codice aggiuntivo toocreate hello e dello schema per le attività del server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="6b0ff-243">Espandere il modello di hello</span><span class="sxs-lookup"><span data-stu-id="6b0ff-243">Expand hello model</span></span>
<span data-ttu-id="6b0ff-244">Questo modello di schema è semplice</span><span class="sxs-lookup"><span data-stu-id="6b0ff-244">This schema model is simple.</span></span> <span data-ttu-id="6b0ff-245">ed è possibile espanderlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-245">You can expand it as required.</span></span>

<span data-ttu-id="6b0ff-246">`owner`: Assegnato toohello attività.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="6b0ff-247">Questo oggetto è di tipo **stringa**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-247">This object is a **string**.</span></span>  

<span data-ttu-id="6b0ff-248">`Text`: attività hello stessa.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-248">`Text`: hello task itself.</span></span> <span data-ttu-id="6b0ff-249">Questo oggetto è di tipo **stringa**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-249">This object is a **string**.</span></span>

<span data-ttu-id="6b0ff-250">`date`: data hello tale attività hello è scadenza.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="6b0ff-251">Questo oggetto è di tipo **datetime**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-251">This object is a **datetime**.</span></span>

<span data-ttu-id="6b0ff-252">`completed`: Se l'attività hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="6b0ff-253">Questo oggetto è di tipo **booleano**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="6b0ff-254">Creare uno schema di hello codice hello</span><span class="sxs-lookup"><span data-stu-id="6b0ff-254">Create hello schema in hello code</span></span>
<span data-ttu-id="6b0ff-255">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-256">Aprire hello `server.js` file in un editor.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6b0ff-257">Aggiungere le seguenti informazioni di sotto la voce di configurazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="6b0ff-258">Creare innanzitutto schema hello e quindi si crea un oggetto modello che si utilizza toostore i dati in tutto hello codice quando si definisce il **route**.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="6b0ff-259">Aggiungere le route per il server delle attività dell'API REST</span><span class="sxs-lookup"><span data-stu-id="6b0ff-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="6b0ff-260">Dopo aver creato un toowork del modello di database con, aggiungere le route hello che è utilizzata per il server API REST.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="6b0ff-261">Informazioni sulle route in Restify</span><span class="sxs-lookup"><span data-stu-id="6b0ff-261">About routes in Restify</span></span>
<span data-ttu-id="6b0ff-262">Le route funzionano in Restify in hello stesso modo in cui operano quando utilizzano stack Express hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="6b0ff-263">Per definire le route tramite URI che si prevede di hello client applicazioni toocall hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="6b0ff-264">Un modello tipico per una route Restify è:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="6b0ff-265">Restify ed Express offrono funzionalità molto più avanzate, ad esempio la definizione di tipi di applicazione e l'esecuzione di un routing complesso tra endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="6b0ff-266">Ai fini di hello di questa esercitazione, è semplice queste route.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="6b0ff-267">Aggiungere server tooyour di route predefinita</span><span class="sxs-lookup"><span data-stu-id="6b0ff-267">Add default routes tooyour server</span></span>
<span data-ttu-id="6b0ff-268">È ora aggiungere route CRUD di base hello **creare** e **elenco** per API REST.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="6b0ff-269">Sono disponibili altre route in hello `complete` ramo dell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="6b0ff-270">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6b0ff-271">Aprire hello `server.js` file in un editor.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6b0ff-272">Di sotto di voci di database hello apportate sopra aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="6b0ff-273">Aggiungere la gestione di route hello</span><span class="sxs-lookup"><span data-stu-id="6b0ff-273">Add error handling for hello routes</span></span>
<span data-ttu-id="6b0ff-274">Aggiungere alcuni gestione degli errori in modo che è possibile comunicare eventuali problemi riscontrati toohello indietro client in modo che è in grado di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="6b0ff-275">Aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="6b0ff-276">Creare il server</span><span class="sxs-lookup"><span data-stu-id="6b0ff-276">Create your server</span></span>
<span data-ttu-id="6b0ff-277">Dopo aver definito il database e inserito le route,</span><span class="sxs-lookup"><span data-stu-id="6b0ff-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="6b0ff-278">ultima operazione di Hello per si toodo è tooadd hello server dell'istanza che gestisce le chiamate.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="6b0ff-279">Restify ed Express forniscono personalizzazione completa per un server API REST, ma è utilizzare il programma di installazione di base hello qui.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="6b0ff-280">Aggiungere hello route toohello server (senza autenticazione)</span><span class="sxs-lookup"><span data-stu-id="6b0ff-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="6b0ff-281">Aggiungi server di autenticazione tooyour API REST</span><span class="sxs-lookup"><span data-stu-id="6b0ff-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="6b0ff-282">A questo punto, il server API REST in esecuzione può essere usato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="6b0ff-283">Dalla riga di comando hello, impostare la directory troppo`azuread`, se non è già presente:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="6b0ff-284">Utilizzare hello OIDCBearerStrategy inclusa passport-azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b0ff-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="6b0ff-285">Quando si scrivono le API, è consigliabile collegare sempre toosomething dati hello univoco da token hello hello utente non può effettuare lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="6b0ff-286">Server hello Archivia elementi di attività, esegue quindi in base a hello **oid** dell'utente hello nel token hello (chiamati tramite token.oid), che passa nel campo proprietario"hello".</span><span class="sxs-lookup"><span data-stu-id="6b0ff-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="6b0ff-287">Questo valore assicura che solo tale utente possa accedere i propri elementi ToDo.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="6b0ff-288">Non è non presenti rischi in hello API di "proprietario", un utente esterno può richiedere attività di altri utenti, anche se vengono autenticati.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="6b0ff-289">Successivamente, utilizzare strategia connessione hello fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="6b0ff-290">Passport utilizza hello stesso modello per tutte le relative strategie.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="6b0ff-291">Viene passato un oggetto `function()` con `token` e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="6b0ff-292">strategia di Hello torna tooyou dopo che ha eseguito tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="6b0ff-293">Archivio utente hello quindi salvare il token di hello in modo che non sia necessario tooask per tale nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b0ff-294">codice Hello precedente accetta qualsiasi utente che si verifica tooauthenticate tooyour server.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="6b0ff-295">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-295">This process is known as autoregistration.</span></span> <span data-ttu-id="6b0ff-296">Nel server di produzione, non lasciare in qualsiasi API hello di accesso agli utenti senza prima li passare attraverso un processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="6b0ff-297">Questo processo è in genere hello modello di App consumer che consentono di tooregister con Facebook ma quindi chiedere toofill informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="6b0ff-298">Se il programma non è un programma della riga di comando, è possibile estrarre posta elettronica hello dall'oggetto token hello è restituito e quindi richiesto toofill agli utenti informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="6b0ff-299">Poiché si tratta di un campione, aggiungerli database in memoria tooan.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="6b0ff-300">Eseguire il tooverify applicazione server che rifiuta è</span><span class="sxs-lookup"><span data-stu-id="6b0ff-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="6b0ff-301">È possibile utilizzare `curl` toosee se si dispone ora OAuth2 protezione contro gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="6b0ff-302">Hello intestazioni restituite devono essere sufficiente tootell si presenti nel percorso corretto hello.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="6b0ff-303">Assicurarsi che l'istanza di MongoDB sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="6b0ff-304">Modificare la directory toohello e server hello esecuzione:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="6b0ff-305">In una nuova finestra del terminale eseguire `curl`</span><span class="sxs-lookup"><span data-stu-id="6b0ff-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="6b0ff-306">Provare un'operazione POST di base:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="6b0ff-307">L'errore 401 è risposta hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="6b0ff-308">Indica il livello di Passport hello sta tentando di tooredirect toohello autorizza un endpoint.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="6b0ff-309">Ora è disponibile un servizio API REST che usa OAuth2</span><span class="sxs-lookup"><span data-stu-id="6b0ff-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="6b0ff-310">È stata implementata un'API REST usando Restify e OAuth.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="6b0ff-311">È ora sufficiente codice in modo da poter continuare toodevelop il servizio e compilare questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="6b0ff-312">Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="6b0ff-313">Per il passaggio successivo, utilizzare una procedura dettagliata aggiuntiva come la [connettersi tooa web API con iOS B2C](active-directory-b2c-devquickstarts-ios.md) procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="6b0ff-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b0ff-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b0ff-314">Next steps</span></span>
<span data-ttu-id="6b0ff-315">È possibile spostare argomenti toomore avanzate, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6b0ff-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="6b0ff-316">Connettersi con iOS con B2C tooa web API</span><span class="sxs-lookup"><span data-stu-id="6b0ff-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
