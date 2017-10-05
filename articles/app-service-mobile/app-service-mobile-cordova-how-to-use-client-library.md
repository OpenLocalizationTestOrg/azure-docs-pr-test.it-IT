---
title: Come usare il plug-in Apache Cordova per le app per dispositivi mobili di Azure
description: Come usare il plug-in Apache Cordova per le app per dispositivi mobili di Azure
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="53331-103">Come usare la libreria client Apache Cordova per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="53331-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="53331-104">Questa guida descrive come eseguire scenari comuni usando il più recente [plug-in Apache Cordova per le app per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="53331-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="53331-105">Se non si ha familiarità con le app per dispositivi mobili di Azure, completare prima di tutto l' [esercitazione introduttiva sulle app per dispositivi mobili di Azure] per creare un back-end e una tabella e per scaricare un progetto Apache Cordova predefinito.</span><span class="sxs-lookup"><span data-stu-id="53331-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="53331-106">In questa guida si esaminerà il plug-in Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="53331-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="53331-107">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="53331-107">Supported platforms</span></span>
<span data-ttu-id="53331-108">Questo SDK supporta Apache Cordova v6.0.0 e versioni successive sui dispositivi iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="53331-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="53331-109">Il supporto della piattaforma è il seguente:</span><span class="sxs-lookup"><span data-stu-id="53331-109">The platform support is as follows:</span></span>

* <span data-ttu-id="53331-110">API Android 19-24 (KitKat tramite Nougat).</span><span class="sxs-lookup"><span data-stu-id="53331-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="53331-111">iOS versioni 8.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="53331-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="53331-112">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="53331-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="53331-113">Piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="53331-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="53331-114"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="53331-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="53331-115">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="53331-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="53331-116">In questa guida si presuppone che la tabella abbia lo stesso schema delle tabelle presenti in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="53331-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="53331-117">Si presuppone anche che il plug-in Apache Cordova sia stato aggiunto al codice.</span><span class="sxs-lookup"><span data-stu-id="53331-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="53331-118">In caso contrario, è possibile aggiungere il plug-in Apache Cordova al progetto nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="53331-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="53331-119">Per altre informazioni sulla creazione della [prima app Apache Cordova], vedere la relativa documentazione.</span><span class="sxs-lookup"><span data-stu-id="53331-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="53331-120"><a name="ionic"></a>Configurazione di un'app Ionic v2</span><span class="sxs-lookup"><span data-stu-id="53331-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="53331-121">Per configurare correttamente un progetto Ionic v2, innanzitutto creare un'applicazione di base e aggiungere il plug-in Cordova:</span><span class="sxs-lookup"><span data-stu-id="53331-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="53331-122">Aggiungere le seguenti righe a `app.component.ts` per creare l'oggetto client:</span><span class="sxs-lookup"><span data-stu-id="53331-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="53331-123">È ora possibile compilare ed eseguire il progetto nel browser:</span><span class="sxs-lookup"><span data-stu-id="53331-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="53331-124">Il plug-in Cordova di App per dispositivi mobili di Azure supporta le app Ionic sia v1 che v2.</span><span class="sxs-lookup"><span data-stu-id="53331-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="53331-125">Solo le app Ionic v2 richiedono la dichiarazione aggiuntiva per l'oggetto `WindowsAzure`.</span><span class="sxs-lookup"><span data-stu-id="53331-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="53331-126"><a name="auth"></a>Procedura: Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="53331-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="53331-127">Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="53331-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="53331-128">È possibile impostare le autorizzazioni per le tabelle per limitare l'accesso per operazioni specifiche solo agli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="53331-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="53331-129">È inoltre possibile utilizzare l'identità degli utenti autenticati per implementare regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="53331-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="53331-130">Per ulteriori informazioni, vedere l'esercitazione [Introduzione all'autenticazione] .</span><span class="sxs-lookup"><span data-stu-id="53331-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="53331-131">Quando si usa l'autenticazione in un'app Apache Cordova, devono essere disponibili i plug-in Cordova seguenti:</span><span class="sxs-lookup"><span data-stu-id="53331-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="53331-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="53331-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="53331-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="53331-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="53331-134">Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.</span><span class="sxs-lookup"><span data-stu-id="53331-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="53331-135">Il flusso server è il processo di autenticazione più semplice, poiché si basa sull'interfaccia di autenticazione Web del provider.</span><span class="sxs-lookup"><span data-stu-id="53331-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="53331-136">Il flusso client assicura una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio Single-Sign-On, poiché si basa su SDK specifici del provider e del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53331-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="53331-137"><a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.</span><span class="sxs-lookup"><span data-stu-id="53331-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="53331-138">Molti tipi di applicazioni Apache Cordova usano una funzionalità di loopback per gestire i flussi dell’interfaccia utente di OAuth.</span><span class="sxs-lookup"><span data-stu-id="53331-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="53331-139">I flussi dell'interfaccia utente di OAuth sull'host locale causa problemi in quanto il servizio di autenticazione sa usare il servizio solo con le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="53331-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="53331-140">Alcuni esempi di flussi dell'interfaccia utente di OAuth problematici sono:</span><span class="sxs-lookup"><span data-stu-id="53331-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="53331-141">L'emulatore Ripple.</span><span class="sxs-lookup"><span data-stu-id="53331-141">The Ripple emulator.</span></span>
* <span data-ttu-id="53331-142">Live Reload con Ionic.</span><span class="sxs-lookup"><span data-stu-id="53331-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="53331-143">L'esecuzione del back-end per dispositivi mobili in locale</span><span class="sxs-lookup"><span data-stu-id="53331-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="53331-144">L'esecuzione del back-end per dispositivi mobili in un Servizio app di Azure diverso rispetto a quello che fornisce l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="53331-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="53331-145">Per aggiungere le proprie impostazioni locali alla configurazione seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="53331-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="53331-146">Accedere al [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="53331-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="53331-147">Selezionare **Tutte le risorse** o **Servizi app** e quindi fare clic sul nome dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="53331-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="53331-148">Fare clic su **Strumenti**</span><span class="sxs-lookup"><span data-stu-id="53331-148">Click **Tools**</span></span>
4. <span data-ttu-id="53331-149">Fare clic su **Esplora risorse** nel menu OSSERVAZIONE, quindi fare clic su **Vai**.</span><span class="sxs-lookup"><span data-stu-id="53331-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="53331-150">Si apre una nuova finestra o una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="53331-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="53331-151">Espandere i nodi **config**, **authsettings** del sito nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="53331-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="53331-152">Fare clic su **Modifica**</span><span class="sxs-lookup"><span data-stu-id="53331-152">Click **Edit**</span></span>
7. <span data-ttu-id="53331-153">Cercare l’elemento "allowedExternalRedirectUrls".</span><span class="sxs-lookup"><span data-stu-id="53331-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="53331-154">Può essere impostato su null o su una matrice di valori.</span><span class="sxs-lookup"><span data-stu-id="53331-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="53331-155">Modificare il valore nel valore seguente:</span><span class="sxs-lookup"><span data-stu-id="53331-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="53331-156">Sostituire gli URL con quelli del servizio.</span><span class="sxs-lookup"><span data-stu-id="53331-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="53331-157">Ad esempio includere "http://localhost:3000" (per il servizio di esempio Node.js) o "http://localhost:4400" (per il servizio Ripple).</span><span class="sxs-lookup"><span data-stu-id="53331-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="53331-158">Questi URL sono solo esempi e la situazione reale per i servizi dell'esempio potrebbe essere diversa.</span><span class="sxs-lookup"><span data-stu-id="53331-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="53331-159">Fare clic sul pulsante **Lettura/scrittura** nell'angolo in alto a destra della schermata.</span><span class="sxs-lookup"><span data-stu-id="53331-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="53331-160">Fare clic sul pulsante verde **PUT** .</span><span class="sxs-lookup"><span data-stu-id="53331-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="53331-161">A questo punto le impostazioni vengono salvate.</span><span class="sxs-lookup"><span data-stu-id="53331-161">The settings are saved at this point.</span></span>  <span data-ttu-id="53331-162">Non chiudere la finestra del browser finché non è terminato il salvataggio delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="53331-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="53331-163">Aggiungere gli URL di loopback anche alle impostazioni CORS del servizio app:</span><span class="sxs-lookup"><span data-stu-id="53331-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="53331-164">Accedere al [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="53331-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="53331-165">Selezionare **Tutte le risorse** o **Servizi app** e quindi fare clic sul nome dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="53331-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="53331-166">Il pannello Impostazioni si apre automaticamente.</span><span class="sxs-lookup"><span data-stu-id="53331-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="53331-167">In caso contrario fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="53331-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="53331-168">Fare clic su **CORS** nel menu API.</span><span class="sxs-lookup"><span data-stu-id="53331-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="53331-169">Immettere l'URL che si desidera aggiungere nella casella apposita e prema INVIO.</span><span class="sxs-lookup"><span data-stu-id="53331-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="53331-170">Immettere gli altri URL in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="53331-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="53331-171">Fare clic su **Salva** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="53331-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="53331-172">Le nuove impostazioni saranno operative in 10-15 secondi.</span><span class="sxs-lookup"><span data-stu-id="53331-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="53331-173"><a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="53331-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="53331-174">Installare [phonegap-plugin-push] per gestire le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="53331-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="53331-175">Questo plug-in può essere facilmente aggiunto usando il comando `cordova plugin add` nella riga di comando o tramite il programma di installazione del plug-in Git in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53331-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="53331-176">Il codice seguente nell'app Apache Cordova registra il dispositivo per le notifiche push:</span><span class="sxs-lookup"><span data-stu-id="53331-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="53331-177">Usare Notification Hubs SDK per inviare notifiche push dal server.</span><span class="sxs-lookup"><span data-stu-id="53331-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="53331-178">Non inviare mai le notifiche push direttamente dai client.</span><span class="sxs-lookup"><span data-stu-id="53331-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="53331-179">Questa operazione può essere usata per attivare un attacco denial-of-service agli Hub di notifica o al servizio PNS.</span><span class="sxs-lookup"><span data-stu-id="53331-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="53331-180">Il servizio PNS potrebbe escludere il traffico come conseguenza di questi attacchi.</span><span class="sxs-lookup"><span data-stu-id="53331-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="53331-181">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="53331-181">More information</span></span>

<span data-ttu-id="53331-182">È possibile trovare informazioni dettagliate sulle API nella [documentazione sulle API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="53331-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="53331-183">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="53331-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="53331-184">[esercitazione introduttiva sulle app per dispositivi mobili di Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="53331-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="53331-185">[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="53331-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="53331-186">[plug-in Apache Cordova per le app per dispositivi mobili di Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="53331-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="53331-187">[prima app Apache Cordova]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="53331-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="53331-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="53331-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="53331-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="53331-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="53331-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="53331-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
