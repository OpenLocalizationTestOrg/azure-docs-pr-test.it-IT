---
title: aaaHow tooUse hello SDK JavaScript per App mobili di Azure
description: Come v tooUse per App mobili di Azure
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
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="b3065-103">Come tooUse hello libreria client JavaScript per App mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="b3065-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="b3065-104">Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [SDK JavaScript per App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="b3065-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="b3065-105">Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end e creare una tabella.</span><span class="sxs-lookup"><span data-stu-id="b3065-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="b3065-106">In questa Guida, l'attenzione sull'utilizzo di back-end mobile hello in applicazioni Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b3065-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b3065-107">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="b3065-107">Supported platforms</span></span>
<span data-ttu-id="b3065-108">È limitare browser supporto toohello corrente e l'ultimo versioni di hello i browser principali: Google Chrome, Microsoft Edge, Microsoft Internet Explorer e Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="b3065-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="b3065-109">Prevediamo hello SDK toofunction con qualsiasi browser moderno relativamente.</span><span class="sxs-lookup"><span data-stu-id="b3065-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="b3065-110">pacchetto di Hello viene distribuito come modulo JavaScript universale, in modo che supporta funzioni globali, AMD, CommonJS i formati e.</span><span class="sxs-lookup"><span data-stu-id="b3065-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="b3065-111"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b3065-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="b3065-112">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="b3065-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="b3065-113">Questa guida si presuppone che la tabella hello è hello stesso schema come tabelle hello in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="b3065-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="b3065-114">L'installazione di hello Azure Mobile App JavaScript SDK possono essere eseguita tramite hello `npm` comando:</span><span class="sxs-lookup"><span data-stu-id="b3065-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="b3065-115">libreria di Hello può essere utilizzata anche come un modulo ES2015, all'interno di ambienti CommonJS come Browserify e Webpack e come una libreria AMD.</span><span class="sxs-lookup"><span data-stu-id="b3065-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="b3065-116">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b3065-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="b3065-117">È anche possibile utilizzare una versione preesistente di hello SDK scaricando direttamente dal nostro CDN:</span><span class="sxs-lookup"><span data-stu-id="b3065-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="b3065-118"><a name="auth"></a>Procedura: Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="b3065-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="b3065-119">Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="b3065-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="b3065-120">È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users.</span><span class="sxs-lookup"><span data-stu-id="b3065-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="b3065-121">È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="b3065-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="b3065-122">Per ulteriori informazioni, vedere hello [Introduzione all'autenticazione] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b3065-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="b3065-123">Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.</span><span class="sxs-lookup"><span data-stu-id="b3065-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="b3065-124">flusso server Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="b3065-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="b3065-125">Hello flusso client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio single sign-on quanto si basa sulla SDK specifici del provider.</span><span class="sxs-lookup"><span data-stu-id="b3065-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="b3065-126"><a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.</span><span class="sxs-lookup"><span data-stu-id="b3065-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="b3065-127">Diversi tipi di applicazioni JavaScript di utilizzare un toohandle funzionalità loopback che OAuth UI flussi.</span><span class="sxs-lookup"><span data-stu-id="b3065-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="b3065-128">Queste funzionalità includono:</span><span class="sxs-lookup"><span data-stu-id="b3065-128">These capabilities include:</span></span>

* <span data-ttu-id="b3065-129">Esecuzione del servizio in locale</span><span class="sxs-lookup"><span data-stu-id="b3065-129">Running your service locally</span></span>
* <span data-ttu-id="b3065-130">Utilizzo di ricaricamento in tempo reale con hello Framework Ionic</span><span class="sxs-lookup"><span data-stu-id="b3065-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="b3065-131">Reindirizzamento tooApp servizio per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b3065-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="b3065-132">In esecuzione in locale può causare problemi in quanto, per impostazione predefinita, il servizio App è solo l'autenticazione configurato l'accesso tooallow dal back-end App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b3065-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="b3065-133">Utilizzare i seguenti passaggi toochange hello autenticazione tooenable le impostazioni di servizio App in esecuzione in locale server hello hello:</span><span class="sxs-lookup"><span data-stu-id="b3065-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="b3065-134">Accedi toohello [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="b3065-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="b3065-135">Passare back-end di tooyour App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b3065-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="b3065-136">Selezionare **Esplora inventario risorse** in hello **gli strumenti di sviluppo** menu.</span><span class="sxs-lookup"><span data-stu-id="b3065-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="b3065-137">Fare clic su **passare** Esplora inventario risorse di hello tooopen per il back-end di App per dispositivi mobili in una nuova scheda o finestra.</span><span class="sxs-lookup"><span data-stu-id="b3065-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="b3065-138">Espandere hello **config** > **authsettings** nodo per l'app.</span><span class="sxs-lookup"><span data-stu-id="b3065-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="b3065-139">Fare clic su hello **modifica** pulsante tooenable la modifica della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="b3065-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="b3065-140">Trovare hello **allowedExternalRedirectUrls** elemento che deve essere null.</span><span class="sxs-lookup"><span data-stu-id="b3065-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="b3065-141">Aggiungere gli URL in una matrice:</span><span class="sxs-lookup"><span data-stu-id="b3065-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="b3065-142">Sostituire gli URL di hello nella matrice hello con hello URL del servizio, che in questo esempio è `http://localhost:3000` per il servizio di esempio hello locale Node.js.</span><span class="sxs-lookup"><span data-stu-id="b3065-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="b3065-143">È anche possibile usare `http://localhost:4400` per il servizio di Ripple hello o altri URL, a seconda della configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b3065-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="b3065-144">Nella parte superiore di hello della pagina hello, fare clic su **lettura/scrittura**, quindi fare clic su **inserire** toosave gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="b3065-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="b3065-145">È inoltre necessario tooadd hello stesso loopback URL toohello whitelist delle impostazioni CORS:</span><span class="sxs-lookup"><span data-stu-id="b3065-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="b3065-146">Spostarsi indietro toohello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="b3065-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="b3065-147">Passare back-end di tooyour App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b3065-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="b3065-148">Fare clic su **CORS** in hello **API** menu.</span><span class="sxs-lookup"><span data-stu-id="b3065-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="b3065-149">Immettere ogni URL in hello vuoto **le origini consentite** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b3065-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="b3065-150">Viene creata una nuova casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b3065-150">A new text box is created.</span></span>
5. <span data-ttu-id="b3065-151">Fare clic su **SALVA**</span><span class="sxs-lookup"><span data-stu-id="b3065-151">Click **SAVE**</span></span>

<span data-ttu-id="b3065-152">Dopo l'aggiornamento di back-end hello, sarà in grado di toouse hello nuovi loopback URL nell'app.</span><span class="sxs-lookup"><span data-stu-id="b3065-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[avvio rapido di Azure Mobile app]: app-service-mobile-cordova-get-started.md
[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portale di Azure]: https://portal.azure.com/
[SDK JavaScript per App mobili di Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
