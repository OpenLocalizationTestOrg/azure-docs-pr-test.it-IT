---
title: aaaGet avviato con Azure Mobile Engagement per Cordova/Phonegap
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app Cordova/Phonegap.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="de6b4-103">Introduzione ad Azure Mobile Engagement per Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="de6b4-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="de6b4-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand app informazioni sull'utilizzo e trasmissione push notifiche toosegmented utenti per un'applicazione per dispositivi mobili sviluppati con Cordova.</span><span class="sxs-lookup"><span data-stu-id="de6b4-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="de6b4-105">In questa esercitazione verrà creata un'app Cordova vuota mediante Mac e quindi verrà eseguita l'integrazione di Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="de6b4-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="de6b4-106">L'app raccoglierà dati analitici di base e riceverà notifiche push tramite Apple Push Notification System (APNS) per iOS e Google Cloud Messaging (GCM) per Android.</span><span class="sxs-lookup"><span data-stu-id="de6b4-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="de6b4-107">Si distribuirà questo tooan dispositivo iOS o Android per il test.</span><span class="sxs-lookup"><span data-stu-id="de6b4-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="de6b4-108">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="de6b4-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="de6b4-109">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="de6b4-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="de6b4-110">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="de6b4-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="de6b4-111">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="de6b4-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="de6b4-112">XCode, che è possibile installare Mac App Store (per la distribuzione tooiOS)</span><span class="sxs-lookup"><span data-stu-id="de6b4-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="de6b4-113">[Android SDK & emulatore](http://developer.android.com/sdk/installing/index.html) (per la distribuzione tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="de6b4-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="de6b4-114">Certificato per notifiche push (con estensione p12) che è possibile ottenere nell'Apple Dev Center per APNS</span><span class="sxs-lookup"><span data-stu-id="de6b4-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="de6b4-115">Numero di progetto GCM, che è possibile ottenere da Google Developer Console per GCM</span><span class="sxs-lookup"><span data-stu-id="de6b4-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="de6b4-116">Plug-in di Cordova per Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="de6b4-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="de6b4-117">È possibile trovare il codice sorgente hello e hello file Leggimi per plug-in Cordova hello in [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="de6b4-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="de6b4-118"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app Cordova</span><span class="sxs-lookup"><span data-stu-id="de6b4-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="de6b4-119"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="de6b4-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="de6b4-120">Questa esercitazione viene illustrato un "integrazione di base" hello minimo imposta dati toocollect necessarie e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="de6b4-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="de6b4-121">Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Cordova:</span><span class="sxs-lookup"><span data-stu-id="de6b4-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="de6b4-122">Creare un nuovo progetto Cordova</span><span class="sxs-lookup"><span data-stu-id="de6b4-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="de6b4-123">Avviare *Terminal* finestra il hello macchina e tipo Mac successivo che verrà creato un nuovo progetto Cordova dal modello predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="de6b4-124">Assicurarsi che la pubblicazione di hello profilo è alla fine toodeploy di usare l'app iOS Usa 'com.mycompany.myapp' come hello ID App.</span><span class="sxs-lookup"><span data-stu-id="de6b4-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="de6b4-125">Eseguire hello seguente tooconfigure il progetto per **iOS** ed eseguirlo nel simulatore iOS hello:</span><span class="sxs-lookup"><span data-stu-id="de6b4-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="de6b4-126">Eseguire hello seguente tooconfigure il progetto per **Android** ed eseguirlo nell'emulatore Android hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="de6b4-127">Assicurarsi che le impostazioni dell'emulatore di Android SDK dispongano la destinazione come Google APIs (Google Inc.) con hello CPU / ABI come Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="de6b4-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="de6b4-128">Aggiungi plug-in Cordova Console hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="de6b4-129">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="de6b4-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="de6b4-130">Installazione di plug-in Cordova di Azure Mobile Engagement hello fornendo hello i valori delle variabili tooconfigure hello plug-in:</span><span class="sxs-lookup"><span data-stu-id="de6b4-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="de6b4-131">*Icona di raggiungere Android* : deve essere hello nome della risorsa hello senza qualsiasi estensione né drawable prefisso (ad esempio: mynotificationicon), e i file di icona hello devono essere copiati nel progetto android (piattaforme/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="de6b4-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="de6b4-132">*Icona raggiungere iOS* : deve essere hello nome della risorsa hello con l'estensione (ad esempio: mynotificationicon.png), e file di icona hello devono essere aggiunti al progetto iOS con XCode (tramite hello Aggiungi file Menu)</span><span class="sxs-lookup"><span data-stu-id="de6b4-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="de6b4-133"><a id="monitor"></a>Abilitazione del monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="de6b4-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="de6b4-134">Nel progetto Cordova hello - modifica **www/js/index.js** chiamata hello tooadd tooMobile Engagement toodeclare una nuova attività una volta hello *deviceReady* viene ricevuto l'evento.</span><span class="sxs-lookup"><span data-stu-id="de6b4-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="de6b4-135">Eseguire un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="de6b4-135">Run hello application:</span></span>
   
   * <span data-ttu-id="de6b4-136">**Per iOS**</span><span class="sxs-lookup"><span data-stu-id="de6b4-136">**For iOS**</span></span>
     
       <span data-ttu-id="de6b4-137">In `Terminal` finestra Avvia l'app in una nuova istanza di simulatore eseguendo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="de6b4-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="de6b4-138">**Per Android**</span><span class="sxs-lookup"><span data-stu-id="de6b4-138">**For Android**</span></span>
     
       <span data-ttu-id="de6b4-139">In `Terminal` finestra Avvia l'app in una nuova istanza dell'emulatore eseguendo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="de6b4-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="de6b4-140">È possibile visualizzare i seguenti hello in hello registri della console:</span><span class="sxs-lookup"><span data-stu-id="de6b4-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="de6b4-141"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="de6b4-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="de6b4-142"><a id="integrate-push"></a>Abilitazione delle notifiche push e della messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="de6b4-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="de6b4-143">Engagement mobile permette di toointeract con gli utenti utilizzando le notifiche Push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="de6b4-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="de6b4-144">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="de6b4-145">Hello nelle sezioni seguenti installerà il tooreceive app li.</span><span class="sxs-lookup"><span data-stu-id="de6b4-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="de6b4-146">Configurare le credenziali push per Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="de6b4-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="de6b4-147">tooallow Mobile Engagement toosend le notifiche Push per conto dell'utente, è necessario accedere a tooyour del certificato per Apple iOS o la chiave API Server GCM toogrant.</span><span class="sxs-lookup"><span data-stu-id="de6b4-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="de6b4-148">Passare portale Mobile Engagement tooyour.</span><span class="sxs-lookup"><span data-stu-id="de6b4-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="de6b4-149">Verificare le app hello è in uso per questo progetto e quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:</span><span class="sxs-lookup"><span data-stu-id="de6b4-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="de6b4-150">Viene visualizzata nella pagina Impostazioni hello nel portale del progetto.</span><span class="sxs-lookup"><span data-stu-id="de6b4-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="de6b4-151">Da scegliere è hello **Push nativo** sezione:</span><span class="sxs-lookup"><span data-stu-id="de6b4-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="de6b4-152">Configurare il certificato iOS o la chiave dell'API del server GCM</span><span class="sxs-lookup"><span data-stu-id="de6b4-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="de6b4-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-153">**[iOS]**</span></span>
   
    <span data-ttu-id="de6b4-154">a.</span><span class="sxs-lookup"><span data-stu-id="de6b4-154">a.</span></span> <span data-ttu-id="de6b4-155">Selezionare il certificato con estensione p12, caricarlo e digitare la password:</span><span class="sxs-lookup"><span data-stu-id="de6b4-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="de6b4-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-156">**[Android]**</span></span>
   
    <span data-ttu-id="de6b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="de6b4-157">a.</span></span> <span data-ttu-id="de6b4-158">Fare clic sull'icona di modifica hello in primo piano **chiave API** nella sezione Impostazioni GCM hello e nella finestra popup di hello che viene visualizzato, incollare hello chiave Server GCM, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="de6b4-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="de6b4-159">Abilitare le notifiche push in app di Cordova hello</span><span class="sxs-lookup"><span data-stu-id="de6b4-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="de6b4-160">Modifica **www/js/index.js** tooadd hello chiamata tooMobile Engagement toorequest notifiche push e dichiarare un gestore:</span><span class="sxs-lookup"><span data-stu-id="de6b4-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="de6b4-161">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="de6b4-161">Run hello app</span></span>
<span data-ttu-id="de6b4-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-162">**[iOS]**</span></span>

1. <span data-ttu-id="de6b4-163">Verrà utilizzare toobuild XCode e distribuire app hello in notifiche di push tootest dispositivo hello poiché iOS consente solo dispositivo effettivo tooan di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="de6b4-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="de6b4-164">Passare toohello percorso in cui è stato creato il progetto Cordova e passare troppo**...\platforms\ios** percorso.</span><span class="sxs-lookup"><span data-stu-id="de6b4-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="de6b4-165">Aprire il file con estensione xcodeproj nativo hello in XCode.</span><span class="sxs-lookup"><span data-stu-id="de6b4-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="de6b4-166">Compilare e distribuire i dispositivi iOS hello Cordova app toohello utilizzando account hello è hello contenente il certificato di hello che appena caricato portale Mobile Engagement toohello e hello App Id che trova la corrispondenza hello uno fornita durante la creazione di profilo di provisioning app Cordova Hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="de6b4-167">È possibile estrarre hello *identificatore Bundle* nel **risorse\*-Info. plist** file in XCode toomatch il backup.</span><span class="sxs-lookup"><span data-stu-id="de6b4-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="de6b4-168">Si noterà popup iOS standard hello sul dispositivo che informa che app hello richiede notifiche toosend di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="de6b4-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="de6b4-169">Concedere l'autorizzazione di hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-169">Grant hello permission.</span></span> 

<span data-ttu-id="de6b4-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-170">**[Android]**</span></span>

<span data-ttu-id="de6b4-171">È possibile utilizzare l'applicazione Android hello hello emulatore toorun semplicemente come le notifiche GCM sono supportate nell'emulatore Android hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="de6b4-172"><a id="send"></a>Invia un'app tooyour notifica</span><span class="sxs-lookup"><span data-stu-id="de6b4-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="de6b4-173">Verrà ora creata una semplice campagna di notifica Push che invierà un'app tooyour push in esecuzione sul dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="de6b4-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="de6b4-174">Passare toohello **raggiungere** scheda nel portale Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="de6b4-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="de6b4-175">Fare clic su **nuovo annuncio** toocreate la campagna push</span><span class="sxs-lookup"><span data-stu-id="de6b4-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="de6b4-176">Fornire input toocreate campagna **[Android]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="de6b4-177">Fornire un **Nome** per la campagna.</span><span class="sxs-lookup"><span data-stu-id="de6b4-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="de6b4-178">Seleziona hello **tipo di recapito** come *notifica di sistema* *semplice*</span><span class="sxs-lookup"><span data-stu-id="de6b4-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="de6b4-179">Seleziona hello **l'ora di recapito** come *"Any ora"*</span><span class="sxs-lookup"><span data-stu-id="de6b4-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="de6b4-180">Fornire un **titolo** per la notifica che sarà hello nella prima riga push hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="de6b4-181">Fornire un **messaggio** per la notifica che verrà utilizzata come corpo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="de6b4-182">Fornire input toocreate campagna **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="de6b4-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="de6b4-183">Fornire un **Nome** per la campagna.</span><span class="sxs-lookup"><span data-stu-id="de6b4-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="de6b4-184">Seleziona hello **l'ora di recapito** come *"da solo app"*</span><span class="sxs-lookup"><span data-stu-id="de6b4-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="de6b4-185">Fornire un **titolo** per la notifica che sarà hello nella prima riga push hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="de6b4-186">Fornire un **messaggio** per la notifica che verrà utilizzata come corpo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="de6b4-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="de6b4-187">Scorrere verso il basso e in hello sezione di contenuto selezionare **sola notifica**</span><span class="sxs-lookup"><span data-stu-id="de6b4-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="de6b4-188">[Facoltativo] È anche possibile specificare un URL di azione.</span><span class="sxs-lookup"><span data-stu-id="de6b4-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="de6b4-189">Assicurarsi che utilizza uno schema URL fornito durante la configurazione del plug-in di hello **AZME\_REINDIRIZZARE\_URL** variabile, ad esempio *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="de6b4-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="de6b4-190">Possibili campagna più elementare di impostazione hello completato.</span><span class="sxs-lookup"><span data-stu-id="de6b4-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="de6b4-191">Ora nuovamente a scorrere verso il basso e fare clic su hello **crea** pulsante toosave la campagna.</span><span class="sxs-lookup"><span data-stu-id="de6b4-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="de6b4-192">Fare infine clic su **Attiva** per la campagna.</span><span class="sxs-lookup"><span data-stu-id="de6b4-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="de6b4-193">Una notifica push dovrebbe essere visualizzata nel dispositivo o nell'emulatore come parte di questa campagna.</span><span class="sxs-lookup"><span data-stu-id="de6b4-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="de6b4-194"><a id="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de6b4-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="de6b4-195">Panoramica di tutti i metodi disponibili con Cordova Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="de6b4-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

