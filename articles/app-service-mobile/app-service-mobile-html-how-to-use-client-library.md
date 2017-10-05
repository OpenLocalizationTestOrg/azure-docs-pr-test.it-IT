---
title: Come usare JavaScript SDK per le app per dispositivi mobili di Azure
description: Come usare v per le app per dispositivi mobili di Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="08f39-103">Come usare la libreria client JavaScript per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="08f39-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="08f39-104">Questa guida descrive come eseguire scenari comuni usando il più recente [JavaScript SDK per le app per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="08f39-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="08f39-105">Se si ha familiarità con le app per dispositivi mobili di Azure, prima è necessario completare l' [Avvio rapido alle app per dispositivi mobili di Azure] per creare un back-end e una tabella.</span><span class="sxs-lookup"><span data-stu-id="08f39-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="08f39-106">In questa Guida, l'attenzione è posta sull'uso di un back-end mobile nelle applicazioni Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="08f39-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="08f39-107">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="08f39-107">Supported platforms</span></span>
<span data-ttu-id="08f39-108">Il supporto del browser è limitato alle versioni correnti e aggiornate dei browser principali: Google Chrome, Microsoft Edge, Microsoft Internet Explorer e Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="08f39-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="08f39-109">L'SDK dovrebbe funzionare con qualsiasi browser abbastanza aggiornato.</span><span class="sxs-lookup"><span data-stu-id="08f39-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="08f39-110">Il pacchetto viene distribuito come Universal JavaScript Module, in modo da supportare i formati globali, AMD e CommonJS.</span><span class="sxs-lookup"><span data-stu-id="08f39-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="08f39-111"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="08f39-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="08f39-112">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="08f39-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="08f39-113">In questa guida si presuppone che la tabella abbia lo stesso schema delle tabelle presenti in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="08f39-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="08f39-114">L'installazione di JavaScript SDK per le app per dispositivi mobili di Azure può essere eseguito tramite il comando `npm` :</span><span class="sxs-lookup"><span data-stu-id="08f39-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="08f39-115">La libreria può anche essere utilizzata come modulo ES2015, all'interno di ambienti CommonJS come ad esempio Browserify e Webpack, e come libreria AMD.</span><span class="sxs-lookup"><span data-stu-id="08f39-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="08f39-116">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="08f39-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="08f39-117">È anche possibile usare una versione predefinita dell'SDK scaricandolo direttamente dalla rete CDN:</span><span class="sxs-lookup"><span data-stu-id="08f39-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="08f39-118"><a name="auth"></a>Procedura: Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="08f39-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="08f39-119">Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f39-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="08f39-120">È possibile impostare le autorizzazioni per le tabelle per limitare l'accesso per operazioni specifiche solo agli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="08f39-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="08f39-121">È inoltre possibile utilizzare l'identità degli utenti autenticati per implementare regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="08f39-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="08f39-122">Per ulteriori informazioni, vedere l'esercitazione [Introduzione all'autenticazione] .</span><span class="sxs-lookup"><span data-stu-id="08f39-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="08f39-123">Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.</span><span class="sxs-lookup"><span data-stu-id="08f39-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="08f39-124">Il flusso server è il processo di autenticazione più semplice, poiché si basa sull'interfaccia di autenticazione Web del provider.</span><span class="sxs-lookup"><span data-stu-id="08f39-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="08f39-125">Il flusso client assicura una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio Single-Sign-On, poiché si basa su SDK specifici del provider.</span><span class="sxs-lookup"><span data-stu-id="08f39-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="08f39-126"><a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.</span><span class="sxs-lookup"><span data-stu-id="08f39-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="08f39-127">Molti tipi di applicazioni JavaScript usano una funzionalità di loopback per gestire i flussi dell'interfaccia utente di OAuth.</span><span class="sxs-lookup"><span data-stu-id="08f39-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="08f39-128">Queste funzionalità includono:</span><span class="sxs-lookup"><span data-stu-id="08f39-128">These capabilities include:</span></span>

* <span data-ttu-id="08f39-129">Esecuzione del servizio in locale</span><span class="sxs-lookup"><span data-stu-id="08f39-129">Running your service locally</span></span>
* <span data-ttu-id="08f39-130">Uso di Live Reload con Ionic Framework</span><span class="sxs-lookup"><span data-stu-id="08f39-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="08f39-131">Reindirizzamento al servizio app per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="08f39-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="08f39-132">L'esecuzione in locale può causare problemi perché, per impostazione predefinita, l'autenticazione del servizio app viene configurata solo per consentire l'accesso dal back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="08f39-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="08f39-133">Usare i passaggi seguenti per modificare le impostazioni del servizio app per abilitare l'autenticazione quando si esegue il server in locale:</span><span class="sxs-lookup"><span data-stu-id="08f39-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="08f39-134">Accedere al [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="08f39-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="08f39-135">Passare al back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="08f39-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="08f39-136">Selezionare **Esplora risorse** nel menu **STRUMENTI DI SVILUPPO**.</span><span class="sxs-lookup"><span data-stu-id="08f39-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="08f39-137">Fare clic su **Vai** per aprire Esplora risorse per il back-end dell'app per dispositivi mobili in una nuova scheda o finestra.</span><span class="sxs-lookup"><span data-stu-id="08f39-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="08f39-138">Espandere il nodo **config** > **authsettings** per l'app.</span><span class="sxs-lookup"><span data-stu-id="08f39-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="08f39-139">Fare clic sul pulsante **Modifica** per abilitare la modifica della risorsa.</span><span class="sxs-lookup"><span data-stu-id="08f39-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="08f39-140">Cercare l'elemento **allowedExternalRedirectUrls** che deve essere null.</span><span class="sxs-lookup"><span data-stu-id="08f39-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="08f39-141">Aggiungere gli URL in una matrice:</span><span class="sxs-lookup"><span data-stu-id="08f39-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="08f39-142">Sostituire gli URL nella matrice con gli URL del servizio, che in questo esempio è `http://localhost:3000` per il servizio di esempio Node.js locale.</span><span class="sxs-lookup"><span data-stu-id="08f39-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="08f39-143">È anche possibile usare `http://localhost:4400` per il servizio Ripple o un altro URL, a seconda della configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="08f39-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="08f39-144">Nella parte superiore della pagina fare clic su **Lettura/Scrittura**, quindi su **PUT** per salvare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="08f39-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="08f39-145">È necessario anche aggiungere gli stessi URL di loopback alle impostazioni dell'elenco elementi consentiti CORS:</span><span class="sxs-lookup"><span data-stu-id="08f39-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="08f39-146">Ritornare al [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="08f39-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="08f39-147">Passare al back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="08f39-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="08f39-148">Fare clic su **CORS** nel menu dell'**API**.</span><span class="sxs-lookup"><span data-stu-id="08f39-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="08f39-149">Immettere ogni URL nella casella di testo vuota **Origini consentite** .</span><span class="sxs-lookup"><span data-stu-id="08f39-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="08f39-150">Viene creata una nuova casella di testo.</span><span class="sxs-lookup"><span data-stu-id="08f39-150">A new text box is created.</span></span>
5. <span data-ttu-id="08f39-151">Fare clic su **SALVA**</span><span class="sxs-lookup"><span data-stu-id="08f39-151">Click **SAVE**</span></span>

<span data-ttu-id="08f39-152">Dopo l'aggiornamento del backend, sarà possibile usare i nuovi URL di loopback nell'app.</span><span class="sxs-lookup"><span data-stu-id="08f39-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="08f39-153">[Avvio rapido alle app per dispositivi mobili di Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="08f39-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="08f39-154">[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="08f39-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="08f39-155">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="08f39-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="08f39-156">[JavaScript SDK per le app per dispositivi mobili di Azure]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="08f39-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
