---
title: aaaHow tooUse plug-in Cordova Apache per App mobili di Azure
description: Come tooUse plug-in Cordova Apache per App mobili di Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="4b379-103">La libreria client di Apache Cordova toouse per App mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="4b379-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="4b379-104">Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [plug-in Cordova Apache per App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="4b379-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="4b379-105">Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end, creare una tabella e scaricare un progetto di Apache Cordova preesistente.</span><span class="sxs-lookup"><span data-stu-id="4b379-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="4b379-106">In questa Guida, focalizzata sul lato client hello plug-in Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="4b379-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4b379-107">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="4b379-107">Supported platforms</span></span>
<span data-ttu-id="4b379-108">Questo SDK supporta Apache Cordova v6.0.0 e versioni successive sui dispositivi iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="4b379-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="4b379-109">supporto della piattaforma Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4b379-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="4b379-110">API Android 19-24 (KitKat tramite Nougat).</span><span class="sxs-lookup"><span data-stu-id="4b379-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="4b379-111">iOS versioni 8.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="4b379-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="4b379-112">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4b379-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="4b379-113">Piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="4b379-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="4b379-114"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4b379-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="4b379-115">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="4b379-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="4b379-116">Questa guida si presuppone che la tabella hello è hello stesso schema come tabelle hello in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="4b379-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="4b379-117">Questa guida si presuppone inoltre che hello plug-in Apache Cordova tooyour codice sia stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="4b379-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="4b379-118">Se non si è connessi, è possibile aggiungere progetto tooyour plug-in Apache Cordova di hello nella riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="4b379-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4b379-119">Per altre informazioni sulla creazione della [prima app Apache Cordova], vedere la relativa documentazione.</span><span class="sxs-lookup"><span data-stu-id="4b379-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="4b379-120"><a name="ionic"></a>Configurazione di un'app Ionic v2</span><span class="sxs-lookup"><span data-stu-id="4b379-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="4b379-121">tooproperly configurare un progetto Ionic v2, prima di tutto creare un'app di base e aggiungere plug-in Cordova hello:</span><span class="sxs-lookup"><span data-stu-id="4b379-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4b379-122">Aggiungere hello seguenti righe troppo`app.component.ts` oggetto client di hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="4b379-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="4b379-123">È possibile compilare ed eseguire il progetto hello nel browser hello:</span><span class="sxs-lookup"><span data-stu-id="4b379-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="4b379-124">plug-in Cordova le app mobili di Azure Hello supporta entrambe le app di Ionic v1 e v2.</span><span class="sxs-lookup"><span data-stu-id="4b379-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="4b379-125">Solo app hello v2 Ionic richiedere che la dichiarazione aggiuntiva hello `WindowsAzure` oggetto.</span><span class="sxs-lookup"><span data-stu-id="4b379-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="4b379-126"><a name="auth"></a>Procedura: Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="4b379-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="4b379-127">Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="4b379-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="4b379-128">È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users.</span><span class="sxs-lookup"><span data-stu-id="4b379-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4b379-129">È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="4b379-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="4b379-130">Per ulteriori informazioni, vedere hello [Introduzione all'autenticazione] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4b379-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="4b379-131">Quando si utilizza l'autenticazione in un'app di Apache Cordova, hello seguenti plug-in Cordova devono essere disponibile:</span><span class="sxs-lookup"><span data-stu-id="4b379-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="4b379-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="4b379-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="4b379-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="4b379-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="4b379-134">Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.</span><span class="sxs-lookup"><span data-stu-id="4b379-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="4b379-135">flusso server Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="4b379-136">Hello flusso client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio single sign-on quanto si basa sulla SDK specifici del dispositivo specifico del provider.</span><span class="sxs-lookup"><span data-stu-id="4b379-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="4b379-137"><a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.</span><span class="sxs-lookup"><span data-stu-id="4b379-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="4b379-138">Diversi tipi di applicazioni Apache Cordova usano un toohandle funzionalità loopback che OAuth UI flussi.</span><span class="sxs-lookup"><span data-stu-id="4b379-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="4b379-139">Poiché il servizio di autenticazione hello riconosce solo problemi OAuth UI flussi su localhost come tooutilize il servizio per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4b379-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="4b379-140">Alcuni esempi di flussi dell'interfaccia utente di OAuth problematici sono:</span><span class="sxs-lookup"><span data-stu-id="4b379-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="4b379-141">emulatore Ripple Hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="4b379-142">Live Reload con Ionic.</span><span class="sxs-lookup"><span data-stu-id="4b379-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="4b379-143">Esecuzione di back-end mobile hello in locale</span><span class="sxs-lookup"><span data-stu-id="4b379-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="4b379-144">Back-end mobile hello è in esecuzione in Azure App Service diverso rispetto all'autenticazione che fornisce uno hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="4b379-145">Seguire queste istruzioni tooadd configurazione toohello impostazioni locali:</span><span class="sxs-lookup"><span data-stu-id="4b379-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="4b379-146">Accedi toohello [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="4b379-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="4b379-147">Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="4b379-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="4b379-148">Fare clic su **Strumenti**</span><span class="sxs-lookup"><span data-stu-id="4b379-148">Click **Tools**</span></span>
4. <span data-ttu-id="4b379-149">Fare clic su **Esplora inventario risorse** nel menu NOTERÀ hello, quindi fare clic su **passare**.</span><span class="sxs-lookup"><span data-stu-id="4b379-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="4b379-150">Si apre una nuova finestra o una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="4b379-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="4b379-151">Espandere hello **config**, **authsettings** nodi per il sito di navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="4b379-152">Fare clic su **Modifica**</span><span class="sxs-lookup"><span data-stu-id="4b379-152">Click **Edit**</span></span>
7. <span data-ttu-id="4b379-153">Cercare l'elemento "allowedExternalRedirectUrls" hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="4b379-154">Può essere impostata toonull o una matrice di valori.</span><span class="sxs-lookup"><span data-stu-id="4b379-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="4b379-155">Modificare hello valore toohello il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="4b379-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="4b379-156">Sostituire gli URL di hello con hello URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="4b379-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="4b379-157">Ad esempio "http://localhost:3000" (per hello servizio esempio Node. js), o "http://localhost:4400" (per il servizio Ripple hello).</span><span class="sxs-lookup"><span data-stu-id="4b379-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="4b379-158">Tuttavia, questi URL sono esempi - situazione attuale, tra cui servizi di hello indicati negli esempi di hello, potrebbero essere diversi.</span><span class="sxs-lookup"><span data-stu-id="4b379-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="4b379-159">Fare clic su hello **lettura/scrittura** pulsante nell'angolo superiore destro di hello della schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="4b379-160">Fare clic su hello verde **inserire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4b379-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="4b379-161">impostazioni di Hello vengono salvate in questa fase.</span><span class="sxs-lookup"><span data-stu-id="4b379-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="4b379-162">Non chiudere finestra del browser hello fino a quando non vengono completate le impostazioni di hello salvataggio.</span><span class="sxs-lookup"><span data-stu-id="4b379-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="4b379-163">Aggiungere anche queste impostazioni di CORS loopback toohello gli URL per il servizio App:</span><span class="sxs-lookup"><span data-stu-id="4b379-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="4b379-164">Accedi toohello [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="4b379-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="4b379-165">Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="4b379-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="4b379-166">pannello impostazioni Hello viene aperta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4b379-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="4b379-167">In caso contrario fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b379-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="4b379-168">Fare clic su **CORS** nel menu hello API.</span><span class="sxs-lookup"><span data-stu-id="4b379-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="4b379-169">Immettere l'URL di hello che si desidera tooadd nell'apposita casella hello e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="4b379-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="4b379-170">Immettere gli altri URL in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="4b379-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="4b379-171">Fare clic su **salvare** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4b379-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="4b379-172">Impiegato circa 10-15 secondi per effetto di tootake hello nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="4b379-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="4b379-173"><a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="4b379-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="4b379-174">Installare hello [phonegap-plug-in-push] toohandle le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="4b379-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="4b379-175">Questo plug-in possono essere aggiunti facilmente mediante la `cordova plugin add` comando nella riga di comando hello o tramite installazione guidata di plug-in Git hello all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b379-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="4b379-176">Il codice seguente nell'app Apache Cordova registra il dispositivo per le notifiche push:</span><span class="sxs-lookup"><span data-stu-id="4b379-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="4b379-177">Usare le notifiche push di hello SDK hub di notifica toosend dal server hello.</span><span class="sxs-lookup"><span data-stu-id="4b379-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="4b379-178">Non inviare mai le notifiche push direttamente dai client.</span><span class="sxs-lookup"><span data-stu-id="4b379-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="4b379-179">Procedere quindi potrebbe essere tootrigger usato un attacco denial of service contro gli hub di notifica o hello PNS.</span><span class="sxs-lookup"><span data-stu-id="4b379-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="4b379-180">Hello PNS Impossibile escludere il traffico in seguito a tali attacchi.</span><span class="sxs-lookup"><span data-stu-id="4b379-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="4b379-181">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="4b379-181">More information</span></span>

<span data-ttu-id="4b379-182">È possibile trovare informazioni dettagliate sulle API nella [documentazione sulle API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="4b379-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[portale di Azure]: https://portal.azure.com
[avvio rapido di Azure Mobile app]: app-service-mobile-cordova-get-started.md
[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in Cordova Apache per App mobili di Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[prima app Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plug-in-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
