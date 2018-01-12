---
title: 'Azure AD B2C: proteggere un''API Web usando Node.js | Microsoft Docs'
description: Come compilare un'API Web Node.js che accetta token da un tenant B2C
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="ecb3a-103">Azure AD B2C: proteggere un'API Web usando Node.js</span><span class="sxs-lookup"><span data-stu-id="ecb3a-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="ecb3a-104">Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="ecb3a-105">I token di accesso consentono alle app client che usano Azure AD B2C di eseguire l'autenticazione all'API.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="ecb3a-106">Questo articolo illustra come creare un'API di elenco attività che consenta agli utenti di aggiungere ed elencare attività.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="ecb3a-107">L'API Web è protetta con Azure AD B2C e consente soltanto agli utenti autenticati di gestire il proprio elenco attività.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="ecb3a-108">Questo esempio è stato scritto per l' [applicazione di esempio iOS B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="ecb3a-109">Eseguire prima questa procedura dettagliata e quindi proseguire con l'esempio.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="ecb3a-110">**Passport** è il middleware di autenticazione per Node.js.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="ecb3a-111">Estremamente flessibile e modulare, Passport può essere installato in modo non invadente in qualsiasi applicazione Web basata su Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="ecb3a-112">Un set completo di strategie supporta l'autenticazione tramite nome utente e password, Facebook, Twitter e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="ecb3a-113">È stata sviluppata una strategia per Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ecb3a-114">Dopo l'installazione di questo modulo, aggiungere il plug-in `passport-azure-ad` di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="ecb3a-115">Per questo esempio è necessario:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="ecb3a-116">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ecb3a-117">Configurare l'applicazione per l'uso del plug-in `azure-ad-passport` di Passport.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="ecb3a-118">Configurare un'applicazione client per chiamare l'API Web To Do List.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ecb3a-119">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ecb3a-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="ecb3a-120">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="ecb3a-121">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="ecb3a-122">Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ecb3a-123">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="ecb3a-123">Create an application</span></span>
<span data-ttu-id="ecb3a-124">A questo punto è necessario creare un'app nella directory B2C, che fornisce ad Azure AD alcune informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="ecb3a-125">In questo caso, sia l'app client che l'API Web sono rappresentate da un unico **ID applicazione** perché includono una sola app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="ecb3a-126">Per creare un'app, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ecb3a-127">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-127">Be sure to:</span></span>

* <span data-ttu-id="ecb3a-128">Includere un' **app Web/API Web** nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ecb3a-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="ecb3a-129">Immettere `http://localhost/TodoListService` come **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="ecb3a-130">Si tratta dell'URL predefinito per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="ecb3a-131">Creare un **segreto applicazione** per l'applicazione e prenderne nota.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="ecb3a-132">Questi dati saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-132">You need this data later.</span></span> <span data-ttu-id="ecb3a-133">Si noti che prima di usare questo valore è necessario [inserire un carattere di escape XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) .</span><span class="sxs-lookup"><span data-stu-id="ecb3a-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="ecb3a-134">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="ecb3a-135">Questi dati saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ecb3a-136">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="ecb3a-136">Create your policies</span></span>
<span data-ttu-id="ecb3a-137">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ecb3a-138">Questa app contiene due esperienze di identità: iscrizione e accesso.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="ecb3a-139">È necessario creare i criteri per ogni tipo, come descritto nell' [articolo di riferimento per i criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="ecb3a-140">Durante la creazione dei tre criteri assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="ecb3a-141">Scegliere **Nome visualizzato** e altri attributi nei criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="ecb3a-142">Scegliere le attestazioni dell'applicazione **Nome visualizzato** e **ID oggetto** in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="ecb3a-143">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="ecb3a-144">Copiare il **Nome** di ciascun criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="ecb3a-145">Dovrebbero mostrare il prefisso `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="ecb3a-146">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ecb3a-147">Dopo aver creato i tre criteri, è possibile passare alla compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="ecb3a-148">Per informazioni sul funzionamento dei criteri in Azure AD B2C, iniziare dall' [esercitazione introduttiva per la compilazione di un'app Web .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="ecb3a-149">Scaricare il codice</span><span class="sxs-lookup"><span data-stu-id="ecb3a-149">Download the code</span></span>
<span data-ttu-id="ecb3a-150">Il codice per questa esercitazione è [disponibile in GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="ecb3a-151">Per compilare l'esempio passo dopo passo, è possibile [scaricare un progetto bozza come file ZIP](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="ecb3a-152">È anche possibile clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="ecb3a-153">L'app completata è anche [disponibile come file ZIP](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) o nel ramo `complete` dello stesso repository.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="ecb3a-154">Scaricare node.js per la piattaforma corrente</span><span class="sxs-lookup"><span data-stu-id="ecb3a-154">Download Node.js for your platform</span></span>
<span data-ttu-id="ecb3a-155">Per usare correttamente questo esempio è necessaria un'installazione funzionante di Node.js.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="ecb3a-156">Installare Node.js da [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="ecb3a-157">Installare MongoDB per la piattaforma corrente</span><span class="sxs-lookup"><span data-stu-id="ecb3a-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="ecb3a-158">Per usare correttamente questo esempio è necessaria un'installazione funzionante di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="ecb3a-159">MongoDB viene usato per rendere l'API REST persistente nelle istanze del server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="ecb3a-160">Installare MongoDB da [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="ecb3a-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="ecb3a-161">In questa procedura dettagliata si presume che si usino gli endpoint server e di installazione predefiniti per MongoDB, al momento della stesura di questo articolo `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="ecb3a-162">Installare i moduli Restify nell'API Web</span><span class="sxs-lookup"><span data-stu-id="ecb3a-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="ecb3a-163">Restify verrà usato per compilare l'API REST.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="ecb3a-164">Restify è un framework applicazioni di Node.js minimo e flessibile derivato da Express,</span><span class="sxs-lookup"><span data-stu-id="ecb3a-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="ecb3a-165">che include una gamma completa di funzionalità per la compilazione di API REST basate su Connect.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="ecb3a-166">Installare Restify</span><span class="sxs-lookup"><span data-stu-id="ecb3a-166">Install Restify</span></span>
<span data-ttu-id="ecb3a-167">Dalla riga di comando passare alla directory `azuread`.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="ecb3a-168">Se la directory `azuread` non esiste, crearla.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="ecb3a-169">`cd azuread` oppure `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="ecb3a-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="ecb3a-170">Immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="ecb3a-171">Questo comando installa Restify.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="ecb3a-172">È STATO VISUALIZZATO UN ERRORE?</span><span class="sxs-lookup"><span data-stu-id="ecb3a-172">Did you get an error?</span></span>
<span data-ttu-id="ecb3a-173">In alcuni sistemi operativi, quando si usa `npm` potrebbero essere visualizzati l'errore `Error: EPERM, chmod '/usr/local/bin/..'` e una richiesta di eseguire l'account come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="ecb3a-174">In tal caso, usare il comando `sudo` per eseguire `npm` a un livello di privilegi più elevato.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="ecb3a-175">È stato visualizzato un errore di DTrace?</span><span class="sxs-lookup"><span data-stu-id="ecb3a-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="ecb3a-176">Durante l'installazione di Restify potrebbe essere visualizzato un testo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="ecb3a-177">Restify offre un meccanismo efficace per tenere traccia delle chiamate REST usando DTrace.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="ecb3a-178">Tuttavia, per molti sistemi operativi DTrace non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="ecb3a-179">È possibile ignorare questi errori.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="ecb3a-180">L'output del comando avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="ecb3a-181">Installare Passport nell'API Web</span><span class="sxs-lookup"><span data-stu-id="ecb3a-181">Install Passport in your web API</span></span>
<span data-ttu-id="ecb3a-182">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="ecb3a-183">Installare Passport usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="ecb3a-184">L'output del comando sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="ecb3a-185">Aggiungere passport-azuread all'API Web</span><span class="sxs-lookup"><span data-stu-id="ecb3a-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="ecb3a-186">A questo punto aggiungere la strategia di OAuth usando `passport-azuread`, una suite di strategie che connettono Azure AD a Passport.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="ecb3a-187">Usare questa strategia per i token di connessione nell'esempio di API REST.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="ecb3a-188">Anche se OAuth2 fornisce un framework in cui è possibile rilasciare qualsiasi tipo di token noto, solo determinati tipi di token sono usati su larga scala.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="ecb3a-189">I token per la protezione degli endpoint sono token di connessione</span><span class="sxs-lookup"><span data-stu-id="ecb3a-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="ecb3a-190">e sono i tipi di token maggiormente rilasciati in OAuth2.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="ecb3a-191">Molte implementazioni presumono che i token di connessione sono l'unico tipo di token rilasciato.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="ecb3a-192">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="ecb3a-193">Immettere il comando seguente per installare il modulo Passport `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="ecb3a-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="ecb3a-194">L'output del comando sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="ecb3a-195">Aggiungere i moduli MongoDB all'API Web</span><span class="sxs-lookup"><span data-stu-id="ecb3a-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="ecb3a-196">Questo esempio usa MongoDB come archivio dati.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="ecb3a-197">A tale scopo installare Mongoose, un plug-in diffuso per la gestione di modelli e schemi.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="ecb3a-198">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="ecb3a-198">Install additional modules</span></span>
<span data-ttu-id="ecb3a-199">A questo punto, installare gli altri moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="ecb3a-200">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-201">Installare i moduli nella directory `node_modules` :</span><span class="sxs-lookup"><span data-stu-id="ecb3a-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="ecb3a-202">Creare un file server.js con le dipendenze</span><span class="sxs-lookup"><span data-stu-id="ecb3a-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="ecb3a-203">Il file `server.js` offre la maggior parte della funzionalità per il server API Web.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="ecb3a-204">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-205">Creare un file `server.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="ecb3a-206">Aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-206">Add the following information:</span></span>

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

<span data-ttu-id="ecb3a-207">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-207">Save the file.</span></span> <span data-ttu-id="ecb3a-208">Servirà ancora successivamente.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="ecb3a-209">Creare un file config.js per archiviare le impostazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecb3a-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="ecb3a-210">Questo file di codice passa i parametri di configurazione dal portale di Azure AD al file `Passport.js` .</span><span class="sxs-lookup"><span data-stu-id="ecb3a-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="ecb3a-211">Questi valori di configurazione sono stati creati quando si è aggiunta l'API Web al portale nella prima parte della procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="ecb3a-212">Dopo aver copiato il codice, verrà spiegato che cosa inserire nei valori di questi parametri.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="ecb3a-213">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-214">Creare un file `config.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="ecb3a-215">Aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="ecb3a-216">Valori richiesti</span><span class="sxs-lookup"><span data-stu-id="ecb3a-216">Required values</span></span>
<span data-ttu-id="ecb3a-217">`clientID`: ID client dell'applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="ecb3a-218">`IdentityMetadata`: qui `passport-azure-ad` cerca i dati di configurazione per il provider di identità</span><span class="sxs-lookup"><span data-stu-id="ecb3a-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="ecb3a-219">e le chiavi di convalida dei token JSON Web.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="ecb3a-220">`audience`: URI (Uniform Resource Identifier) dal portale che identifica l'applicazione chiamante.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="ecb3a-221">`tenantName`: nome del tenant, ad esempio **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="ecb3a-222">`policyName`: criteri da usare per convalidare i token in ingresso nel server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="ecb3a-223">Usare gli stessi criteri usati nell'applicazione client per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="ecb3a-224">Per questo esempio, usare gli stessi i criteri per entrambe le configurazioni client e server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="ecb3a-225">Se è già stata completata una procedura dettagliata in cui sono stati creati questi criteri, non è necessario crearli di nuovo.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="ecb3a-226">Dal momento che la procedura dettagliata è stata completata, non è necessario impostare nuovi criteri per procedure dettagliate relative ai client nel sito.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="ecb3a-227">Aggiungere la configurazione al file server.js</span><span class="sxs-lookup"><span data-stu-id="ecb3a-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="ecb3a-228">Per leggere i valori dal file `config.js` creato, aggiungere il file `.config` come risorsa necessaria nell'applicazione e quindi impostare le variabili globali su quelle del documento `config.js`.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="ecb3a-229">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-230">Aprire il file `server.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="ecb3a-231">Aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="ecb3a-232">Aggiungere una nuova sezione a `server.js` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="ecb3a-233">Aggiungere quindi alcuni segnaposto per gli utenti ricevuti dalle applicazioni chiamanti.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="ecb3a-234">Creare anche il logger.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="ecb3a-235">Aggiungere le informazioni su schemi e modelli MongoDB usando Moongoose</span><span class="sxs-lookup"><span data-stu-id="ecb3a-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="ecb3a-236">Le attività preliminari risulteranno utili quando si riuniranno questi tre file in un servizio API REST.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="ecb3a-237">Per questa procedura dettagliata, usare MongoDB per archiviare le attività, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="ecb3a-238">Nel file `config.js` , il database è stato denominato **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="ecb3a-239">Questo nome è stato anche inserito alla fine dell'URL di connessione `mongoose_auth_local` .</span><span class="sxs-lookup"><span data-stu-id="ecb3a-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="ecb3a-240">Non è necessario creare in anticipo il database in MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="ecb3a-241">Il database verrà creato automaticamente alla prima esecuzione dell'applicazione server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="ecb3a-242">Dopo aver indicato al server quale database MongoDB usare, è necessario scrivere del codice aggiuntivo per creare il modello e lo schema per le attività del server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="ecb3a-243">Espandere il modello</span><span class="sxs-lookup"><span data-stu-id="ecb3a-243">Expand the model</span></span>
<span data-ttu-id="ecb3a-244">Questo modello di schema è semplice</span><span class="sxs-lookup"><span data-stu-id="ecb3a-244">This schema model is simple.</span></span> <span data-ttu-id="ecb3a-245">ed è possibile espanderlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-245">You can expand it as required.</span></span>

<span data-ttu-id="ecb3a-246">`owner`: utente assegnato all'attività.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="ecb3a-247">Questo oggetto è di tipo **stringa**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-247">This object is a **string**.</span></span>  

<span data-ttu-id="ecb3a-248">`Text`: l'attività stessa.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-248">`Text`: The task itself.</span></span> <span data-ttu-id="ecb3a-249">Questo oggetto è di tipo **stringa**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-249">This object is a **string**.</span></span>

<span data-ttu-id="ecb3a-250">`date`: data di scadenza dell'attività.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="ecb3a-251">Questo oggetto è di tipo **datetime**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-251">This object is a **datetime**.</span></span>

<span data-ttu-id="ecb3a-252">`completed`: indica se l'attività è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="ecb3a-253">Questo oggetto è di tipo **booleano**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="ecb3a-254">Creare lo schema nel codice</span><span class="sxs-lookup"><span data-stu-id="ecb3a-254">Create the schema in the code</span></span>
<span data-ttu-id="ecb3a-255">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-256">Aprire il file `server.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="ecb3a-257">Aggiungere le informazioni seguenti sotto la voce di configurazione:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="ecb3a-258">Creare prima lo schema e quindi creare un oggetto modello da usare per l'archiviazione dei dati nel codice quando si definiscono le **route**.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="ecb3a-259">Aggiungere le route per il server delle attività dell'API REST</span><span class="sxs-lookup"><span data-stu-id="ecb3a-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="ecb3a-260">Ora che è disponibile un modello di database, aggiungere le route da usare per il server API REST.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="ecb3a-261">Informazioni sulle route in Restify</span><span class="sxs-lookup"><span data-stu-id="ecb3a-261">About routes in Restify</span></span>
<span data-ttu-id="ecb3a-262">Il funzionamento delle route in Restify è identico al funzionamento nello stack di Express.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="ecb3a-263">Definire le route usando l'URI che si prevede verrà chiamato dalle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="ecb3a-264">Un modello tipico per una route Restify è:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="ecb3a-265">Restify ed Express offrono funzionalità molto più avanzate, ad esempio la definizione di tipi di applicazione e l'esecuzione di un routing complesso tra endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="ecb3a-266">Ai fini di questa esercitazione verranno usate route semplici.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="ecb3a-267">Aggiungere le route predefinite al server</span><span class="sxs-lookup"><span data-stu-id="ecb3a-267">Add default routes to your server</span></span>
<span data-ttu-id="ecb3a-268">Verranno ora aggiunte le route CRUD di base **create** e **list** per l'API REST.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="ecb3a-269">Sono disponibili altre route nel ramo `complete` dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="ecb3a-270">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="ecb3a-271">Aprire il file `server.js` in un editor.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="ecb3a-272">Aggiungere le informazioni seguenti sotto le voci di database create in precedenza:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="ecb3a-273">Aggiungere la gestione di errori per le route</span><span class="sxs-lookup"><span data-stu-id="ecb3a-273">Add error handling for the routes</span></span>
<span data-ttu-id="ecb3a-274">Aggiungere la gestione di errori per poter comunicare al client eventuali problemi riscontrati in un modo comprensibile per il client stesso.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="ecb3a-275">Aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="ecb3a-276">Creare il server</span><span class="sxs-lookup"><span data-stu-id="ecb3a-276">Create your server</span></span>
<span data-ttu-id="ecb3a-277">Dopo aver definito il database e inserito le route,</span><span class="sxs-lookup"><span data-stu-id="ecb3a-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="ecb3a-278">resta solo da aggiungere l'istanza del server che gestirà le chiamate.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="ecb3a-279">Restify ed Express offrono un livello elevato di personalizzazione per un server API REST, ma in questo caso si userà la configurazione più semplice.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="ecb3a-280">Aggiungere le route al server (senza autenticazione)</span><span class="sxs-lookup"><span data-stu-id="ecb3a-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="ecb3a-281">Aggiungere l'autenticazione al server API REST</span><span class="sxs-lookup"><span data-stu-id="ecb3a-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="ecb3a-282">A questo punto, il server API REST in esecuzione può essere usato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="ecb3a-283">Dalla riga di comando passare alla directory `azuread`, se non è già la posizione corrente:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="ecb3a-284">Usare l'oggetto OIDCBearerStrategy incluso in passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="ecb3a-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="ecb3a-285">Durante la scrittura delle API è sempre necessario collegare i dati a un elemento univoco dal token in modo che l'utente non possa eseguire lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="ecb3a-286">Quando archivia gli elementi ToDo, il server si basa sull' **OID** dell'utente nel token, chiamato tramite token.oid, da inserire nel campo "owner".</span><span class="sxs-lookup"><span data-stu-id="ecb3a-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="ecb3a-287">Questo valore assicura che solo tale utente possa accedere i propri elementi ToDo.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="ecb3a-288">Il valore di "owner" non viene esposto nell'API, così che un utente esterno può richiedere elementi TODO di altri anche se sono autenticati.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="ecb3a-289">Usare quindi la strategia di connessione fornita con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="ecb3a-290">Passport usa lo stesso modello per tutte le strategie.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="ecb3a-291">Viene passato un oggetto `function()` con `token` e `done` come parametri.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="ecb3a-292">La strategia risponde dopo avere eseguito tutte le relative operazioni.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="ecb3a-293">Archiviare quindi l'utente e salvare il token per non doverlo richiedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecb3a-294">Il codice precedente accetta qualsiasi utente che esegue l'autenticazione al server.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="ecb3a-295">Questa operazione è nota come registrazione automatica.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-295">This process is known as autoregistration.</span></span> <span data-ttu-id="ecb3a-296">Nei server di produzione non consentire l'accesso degli utenti all'API senza prima un processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="ecb3a-297">Questo processo è il modello in genere adottato per le app consumer che consentono di eseguire la registrazione usando Facebook, ma che chiedono di immettere informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="ecb3a-298">Se non si trattasse di un programma della riga di comando, sarebbe possibile estrarre il messaggio di posta elettronica dall'oggetto token restituito e chiedere agli utenti di immettere informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="ecb3a-299">Trattandosi di un esempio, le informazioni verranno aggiunte a un database in memoria.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="ecb3a-300">Eseguire l'applicazione server per verificare che rifiuti l'utente</span><span class="sxs-lookup"><span data-stu-id="ecb3a-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="ecb3a-301">Per verificare se la protezione OAuth2 per gli endpoint è attiva, usare `curl` .</span><span class="sxs-lookup"><span data-stu-id="ecb3a-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="ecb3a-302">Le intestazioni restituite dovrebbero essere sufficienti a capire se si sta procedendo nel modo corretto.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="ecb3a-303">Assicurarsi che l'istanza di MongoDB sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="ecb3a-304">Passare alla directory ed eseguire il server:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="ecb3a-305">In una nuova finestra del terminale eseguire `curl`</span><span class="sxs-lookup"><span data-stu-id="ecb3a-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="ecb3a-306">Provare un'operazione POST di base:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="ecb3a-307">L'errore 401 è la risposta prevista.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-307">A 401 error is the response you want.</span></span> <span data-ttu-id="ecb3a-308">Indica che il livello Passport sta provando a eseguire il reindirizzamento all'endpoint di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="ecb3a-309">Ora è disponibile un servizio API REST che usa OAuth2</span><span class="sxs-lookup"><span data-stu-id="ecb3a-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="ecb3a-310">È stata implementata un'API REST usando Restify e OAuth.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="ecb3a-311">Il codice ora disponibile consente di continuare a sviluppare il servizio sulla base di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="ecb3a-312">Sono state eseguite tutte le operazioni possibili con questo server senza usare un client compatibile con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="ecb3a-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="ecb3a-313">Per il passaggio successivo usare una procedura dettagliata aggiuntiva come [Azure AD B2C: chiamare un'API Web da un'applicazione iOS con una libreria di terze parti](active-directory-b2c-devquickstarts-ios.md) .</span><span class="sxs-lookup"><span data-stu-id="ecb3a-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecb3a-314">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ecb3a-314">Next steps</span></span>
<span data-ttu-id="ecb3a-315">Ora è possibile passare ad argomenti più avanzati, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ecb3a-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="ecb3a-316">Connettersi a un'API Web usando iOS con B2C &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="ecb3a-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
