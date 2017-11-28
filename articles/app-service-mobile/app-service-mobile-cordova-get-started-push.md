---
title: Aggiungere notifiche push all'app Apache Cordova con App per dispositivi mobili di Azure | Documentazione Microsoft
description: Informazioni su come usare App per dispositivi mobili di Azure per inviare notifiche push all'app Apache Cordova.
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="9672e-103">Aggiungere notifiche push all'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="9672e-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="9672e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9672e-104">Overview</span></span>
<span data-ttu-id="9672e-105">In questa esercitazione vengono aggiunte notifiche push al progetto di [avvio rapido di Apache Cordova], in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="9672e-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="9672e-106">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="9672e-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="9672e-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="9672e-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="9672e-108"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9672e-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="9672e-109">Questa esercitazione illustra un'applicazione Apache Cordova sviluppata in Visual Studio 2015 e in esecuzione nell'emulatore Android di Google, in un dispositivo Android, un dispositivo Windows e un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="9672e-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="9672e-110">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="9672e-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="9672e-111">Un computer in cui è installato [Visual Studio Community 2015][2] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9672e-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="9672e-112">[Visual Studio Tools per Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="9672e-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="9672e-113">Un [account Azure attivo][3].</span><span class="sxs-lookup"><span data-stu-id="9672e-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="9672e-114">Un progetto di [avvio rapido di Apache Cordova][5] completato.</span><span class="sxs-lookup"><span data-stu-id="9672e-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="9672e-115">(Android) Un [account Google][6] con un indirizzo di posta elettronica verificato.</span><span class="sxs-lookup"><span data-stu-id="9672e-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="9672e-116">(iOS) [Iscrizione all'Apple Developer Program][7] e un dispositivo iOS. Il simulatore iOS non supporta le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="9672e-117">(Windows) Un [account per sviluppatore di Windows Store][8] e un dispositivo Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9672e-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="9672e-118"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="9672e-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="9672e-119">[Guardare un video che illustra la procedura disponibile in questa sezione][9]</span><span class="sxs-lookup"><span data-stu-id="9672e-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="9672e-120">Aggiornare il progetto server</span><span class="sxs-lookup"><span data-stu-id="9672e-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="9672e-121"><a name="add-push-to-app"></a>Modificare l'app Cordova</span><span class="sxs-lookup"><span data-stu-id="9672e-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="9672e-122">Assicurarsi che il progetto app Apache Cordova sia pronto per la gestione delle notifiche push installando il plug-in di push di Cordova ed eventuali servizi push specifici della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="9672e-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="9672e-123">Aggiornare la versione di Cordova nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="9672e-124">Se il progetto utilizza una versione di Apache Cordova precedente alla v6.1.1, aggiornare il progetto client.</span><span class="sxs-lookup"><span data-stu-id="9672e-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="9672e-125">Per aggiornare il progetto:</span><span class="sxs-lookup"><span data-stu-id="9672e-125">To update the project:</span></span>

* <span data-ttu-id="9672e-126">Fare clic con il pulsante destro su `config.xml` per aprire la finestra di progettazione configurazione.</span><span class="sxs-lookup"><span data-stu-id="9672e-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="9672e-127">Selezionare la scheda Piattaforme.</span><span class="sxs-lookup"><span data-stu-id="9672e-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="9672e-128">Scegliere 6.1.1 nella casella di testo **Cordova CLI**.</span><span class="sxs-lookup"><span data-stu-id="9672e-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="9672e-129">Scegliere **Compila**, quindi **Compila soluzione** per aggiornare il progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="9672e-130">Installare il plug-in di push</span><span class="sxs-lookup"><span data-stu-id="9672e-130">Install the push plugin</span></span>
<span data-ttu-id="9672e-131">Le applicazioni Apache Cordova non gestiscono in modo nativo le funzionalità del dispositivo o della rete.</span><span class="sxs-lookup"><span data-stu-id="9672e-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="9672e-132">Queste funzionalità sono incluse nei plug-in che vengono pubblicati in [npm][10] o GitHub.</span><span class="sxs-lookup"><span data-stu-id="9672e-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="9672e-133">Il plug-in `phonegap-plugin-push` viene usato per gestire le notifiche push di rete.</span><span class="sxs-lookup"><span data-stu-id="9672e-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="9672e-134">È possibile installare il plug-in di push in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9672e-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="9672e-135">**Dal prompt dei comandi:**</span><span class="sxs-lookup"><span data-stu-id="9672e-135">**From the command-prompt:**</span></span>

<span data-ttu-id="9672e-136">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9672e-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="9672e-137">**Da Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="9672e-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="9672e-138">In Esplora soluzioni aprire il file `config.xml`, fare clic su **Plug-in**>**Personalizza**, selezionare **Git** come origine dell'installazione e quindi immettere `https://github.com/phonegap/phonegap-plugin-push` come origine.</span><span class="sxs-lookup"><span data-stu-id="9672e-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="9672e-139">Fare clic sulla freccia accanto all'origine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="9672e-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="9672e-140">In **SENDER_ID** è possibile aggiungere l'ID numerico del progetto della Console per gli sviluppatori di Google, se l'ID è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="9672e-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="9672e-141">In caso contrario, immettere un valore segnaposto, ad esempio 777777.</span><span class="sxs-lookup"><span data-stu-id="9672e-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="9672e-142">Se la destinazione è Android, sarà possibile aggiornare questo valore nel file config.xml in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9672e-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="9672e-143">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9672e-143">Click **Add**.</span></span>

<span data-ttu-id="9672e-144">Il plug-in di push è stato installato.</span><span class="sxs-lookup"><span data-stu-id="9672e-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="9672e-145">Installare il plug-in del dispositivo</span><span class="sxs-lookup"><span data-stu-id="9672e-145">Install the device plugin</span></span>
<span data-ttu-id="9672e-146">Seguire la stessa procedura utilizzata per installare il plug-in di push.</span><span class="sxs-lookup"><span data-stu-id="9672e-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="9672e-147">Aggiungere il plug-in del dispositivo dall'elenco di plug-in di base (fare clic su **Plug-in** > **Base** per trovarlo).</span><span class="sxs-lookup"><span data-stu-id="9672e-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="9672e-148">Questo plug-in è necessario per ottenere il nome della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="9672e-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="9672e-149">Registrare il dispositivo all'avvio dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9672e-149">Register your device on application start-up</span></span>
<span data-ttu-id="9672e-150">Viene inizialmente incluso un codice minimo per Android.</span><span class="sxs-lookup"><span data-stu-id="9672e-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="9672e-151">Modificare quindi l'applicazione per eseguirla su iOS o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9672e-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="9672e-152">Aggiungere una chiamata a **registerForPushNotifications** durante il callback per il processo di accesso o nella parte inferiore del metodo **onDeviceReady**:</span><span class="sxs-lookup"><span data-stu-id="9672e-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="9672e-153">Questo esempio illustra la chiamata a **registerForPushNotifications** al termine dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9672e-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="9672e-154">È possibile chiamare `registerForPushNotifications()` ogni qualvolta è necessario.</span><span class="sxs-lookup"><span data-stu-id="9672e-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="9672e-155">Aggiungere il nuovo metodo **registerForPushNotifications** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9672e-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="9672e-156">(Android) Nel codice precedente sostituire `Your_Project_ID` con l'ID progetto numerico dell'app indicato nella [Console per gli sviluppatori di Google][18].</span><span class="sxs-lookup"><span data-stu-id="9672e-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="9672e-157">(Facoltativo) Configurare ed eseguire l'app in Android</span><span class="sxs-lookup"><span data-stu-id="9672e-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="9672e-158">Completare questa sezione per abilitare le notifiche push per Android.</span><span class="sxs-lookup"><span data-stu-id="9672e-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="9672e-159"><a name="enable-gcm"></a>Abilitare Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="9672e-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="9672e-160">Poiché la destinazione iniziale è la piattaforma di Google Android, è necessario abilitare Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="9672e-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="9672e-161"><a name="configure-backend"></a>Configurare il back-end dell'app per dispositivi mobili per inviare richieste push usando FCM</span><span class="sxs-lookup"><span data-stu-id="9672e-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="9672e-162">Configurare l'app Cordova per Android</span><span class="sxs-lookup"><span data-stu-id="9672e-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="9672e-163">Nell'app Cordova aprire il file config.xml e sostituire `Your_Project_ID` con l'ID progetto numerico dell'app indicato nella [Console per gli sviluppatori di Google][18].</span><span class="sxs-lookup"><span data-stu-id="9672e-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="9672e-164">Aprire index.js e aggiornare il codice per usare l'ID progetto numerico.</span><span class="sxs-lookup"><span data-stu-id="9672e-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="9672e-165"><a name="configure-device"></a>Configurare il dispositivo Android per il debug USB</span><span class="sxs-lookup"><span data-stu-id="9672e-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="9672e-166">Prima di poter distribuire l'applicazione al dispositivo Android, è necessario abilitare il debug USB.</span><span class="sxs-lookup"><span data-stu-id="9672e-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="9672e-167">Sul telefono Android seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9672e-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="9672e-168">Passare a **Settings** (Impostazioni)>**About phone** (Info sul dispositivo) e toccare **Build number** (Numero build) circa sette volte finché non sarà abilitata la modalità sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="9672e-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="9672e-169">Tornare in **Settings** (Impostazioni)>**Developer Options** (Opzioni per gli sviluppatori), abilitare **USB debugging** (Debug USB), quindi connettere lo smartphone Android al PC di sviluppo con un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="9672e-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="9672e-170">Per questo test è stato usato un dispositivo Google Nexus 5X con Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="9672e-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="9672e-171">Tuttavia, le tecniche sono comuni a qualsiasi versione moderna di Android.</span><span class="sxs-lookup"><span data-stu-id="9672e-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="9672e-172">Installare servizi Google Play</span><span class="sxs-lookup"><span data-stu-id="9672e-172">Install Google Play Services</span></span>
<span data-ttu-id="9672e-173">Il plug-in di push si basa su servizi Google Play Android per notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="9672e-174">In Visual Studio fare clic su **Strumenti**>**Android**>**Android SDK Manager**, espandere la cartella **Funzionalità aggiuntive** e selezionare la casella per assicurarsi che tutti gli SDK seguenti siano installati.</span><span class="sxs-lookup"><span data-stu-id="9672e-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="9672e-175">Android 2.3 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9672e-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="9672e-176">Google Repository 27 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9672e-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="9672e-177">Google Play Services 9.0.2 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9672e-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="9672e-178">Fare clic su **Install Packages** (Installa pacchetti) e attendere il completamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="9672e-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="9672e-179">Le librerie attualmente necessarie sono elencate nella [documentazione relativa all'installazione di phonegap-plugin-push][19].</span><span class="sxs-lookup"><span data-stu-id="9672e-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="9672e-180">Testare le notifiche push nell'app in Android</span><span class="sxs-lookup"><span data-stu-id="9672e-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="9672e-181">A questo punto è possibile testare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="9672e-182">Eseguire l'applicazione e inserire elementi nella tabella TodoItem usando lo stesso dispositivo oppure un altro dispositivo, purché il back-end sia lo stesso.</span><span class="sxs-lookup"><span data-stu-id="9672e-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="9672e-183">Testare l'app Cordova sulla piattaforma Android in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9672e-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="9672e-184">**In un dispositivo fisico:** collegare il dispositivo Android al computer di sviluppo con un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="9672e-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="9672e-185">Invece di selezionare **Emulatore Android di Google**, selezionare **Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="9672e-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="9672e-186">Visual Studio distribuisce l'applicazione nel dispositivo e quindi la esegue.</span><span class="sxs-lookup"><span data-stu-id="9672e-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="9672e-187">Sarà quindi possibile interagire con l'applicazione dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9672e-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="9672e-188">Migliorare l'esperienza di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9672e-188">Improve your development experience.</span></span>  <span data-ttu-id="9672e-189">Le applicazioni per la condivisione dello schermo come [Mobizen][20] possono facilitare lo sviluppo di un'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="9672e-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="9672e-190">Mobizen proietta lo schermo Android su un Web browser sul PC.</span><span class="sxs-lookup"><span data-stu-id="9672e-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="9672e-191">**In un emulatore Android:** sono necessari altri passaggi di configurazione per l'esecuzione in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="9672e-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="9672e-192">Assicurarsi di distribuire su un dispositivo virtuale che abbia le API Google impostate come destinazione, come illustrato di seguito nel gestore del dispositivo virtuale Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="9672e-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="9672e-193">Se si vuole usare un emulatore x86 più veloce, [installare il driver HAXM][11] e configurare l'emulatore per usarlo.</span><span class="sxs-lookup"><span data-stu-id="9672e-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="9672e-194">Aggiungere un account Google al dispositivo Android facendo clic su **Apps** (App) > **Settings** (Impostazioni) > **Add account** (Aggiungi account), quindi seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9672e-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="9672e-195">Eseguire l'app todolist come fatto in precedenza e inserire un nuovo elemento todo.</span><span class="sxs-lookup"><span data-stu-id="9672e-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="9672e-196">Questa volta, viene visualizzata un'icona di notifica nell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="9672e-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="9672e-197">È possibile aprire la cassetta della notifica per visualizzare il testo completo della notifica.</span><span class="sxs-lookup"><span data-stu-id="9672e-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="9672e-198">(Facoltativo) Configurare ed eseguire l'app in iOS</span><span class="sxs-lookup"><span data-stu-id="9672e-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="9672e-199">Questa sezione illustra l'esecuzione del progetto Cordova in dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="9672e-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="9672e-200">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9672e-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="9672e-201">Installare ed eseguire l'agente remotebuild per iOS in un computer Mac o un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="9672e-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="9672e-202">Prima di eseguire un'app Cordova in iOS usando Visual Studio, seguire i passaggi nella [guida alla configurazione per iOS][12] per installare ed eseguire l'agente remotebuild.</span><span class="sxs-lookup"><span data-stu-id="9672e-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="9672e-203">Verificare che sia possibile compilare l'app per iOS.</span><span class="sxs-lookup"><span data-stu-id="9672e-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="9672e-204">I passaggi indicati nella guida alla configurazione sono necessari per la compilazione per iOS da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9672e-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="9672e-205">Se non è disponibile un computer Mac, è possibile eseguire la compilazione per iOS usando l'agente remotebuild in un servizio come MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="9672e-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="9672e-206">Per altre informazioni, vedere [Eseguire l'app iOS nel cloud][21].</span><span class="sxs-lookup"><span data-stu-id="9672e-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="9672e-207">XCode 7 o versione successiva è necessario per usare il plug-in di push in iOS.</span><span class="sxs-lookup"><span data-stu-id="9672e-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="9672e-208">Trovare l'ID da usare come ID app</span><span class="sxs-lookup"><span data-stu-id="9672e-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="9672e-209">Prima di registrare l'app per le notifiche push, aprire il file config.xml nell'app Cordova, trovare il valore dell'attributo `id` nell'elemento widget e copiarlo per usarlo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9672e-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="9672e-210">Nel codice XML seguente, l'ID è `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="9672e-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="9672e-211">Questo identificatore verrà usato in un secondo momento, durante la creazione di un ID app nel portale per sviluppatori di Apple.</span><span class="sxs-lookup"><span data-stu-id="9672e-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="9672e-212">Se si crea un ID app diverso nel portale per sviluppatori, è necessario eseguire alcuni passaggi aggiuntivi più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9672e-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="9672e-213">L'ID nell'elemento widget deve corrispondere all'ID app indicato nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9672e-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="9672e-214">Registrare l'app per le notifiche push nel portale per sviluppatori Apple</span><span class="sxs-lookup"><span data-stu-id="9672e-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="9672e-215">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="9672e-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="9672e-216">Configurare Azure per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="9672e-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="9672e-217">Verificare che l'ID app corrisponda all'app Cordova</span><span class="sxs-lookup"><span data-stu-id="9672e-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="9672e-218">Se l'ID app creato nell'account per sviluppatori Apple corrisponde già all'ID dell'elemento widget nel file config.xml, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="9672e-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="9672e-219">Se tuttavia gli ID non corrispondono, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="9672e-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="9672e-220">Eliminare la cartella platforms dal progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="9672e-221">Eliminare la cartella plugins dal progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="9672e-222">Eliminare la cartella node_modules dal progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="9672e-223">Aggiornare l'attributo id dell'elemento widget nel file config.xml per usare l'ID app creato nell'account per sviluppatori Apple.</span><span class="sxs-lookup"><span data-stu-id="9672e-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="9672e-224">Ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="9672e-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="9672e-225">Testare le notifiche push nell'app iOS</span><span class="sxs-lookup"><span data-stu-id="9672e-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="9672e-226">In Visual Studio verificare che sia selezionato **iOS** come destinazione di distribuzione e quindi scegliere **Dispositivo** per l'esecuzione nel dispositivo iOS connesso.</span><span class="sxs-lookup"><span data-stu-id="9672e-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="9672e-227">È possibile eseguire il progetto in un dispositivo iOS connesso al PC usando iTunes.</span><span class="sxs-lookup"><span data-stu-id="9672e-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="9672e-228">Il simulatore iOS non supporta le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="9672e-229">Scegliere **Esegui** o premere **F5** per compilare il progetto e avviare l'app in un dispositivo iOS, quindi fare clic su **OK** per accettare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9672e-230">L'app richiede una conferma per le notifiche push durante la prima esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9672e-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="9672e-231">Nell'app digitare un'attività e fare clic sull'icona con il segno PIÙ (+).</span><span class="sxs-lookup"><span data-stu-id="9672e-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="9672e-232">Verificare che venga ricevuta una notifica, quindi fare clic su OK per ignorarla.</span><span class="sxs-lookup"><span data-stu-id="9672e-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="9672e-233">(Facoltativo) Configurare ed eseguire l'app in Windows</span><span class="sxs-lookup"><span data-stu-id="9672e-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="9672e-234">Questa sezione descrive l'esecuzione del progetto di un'app Apache Cordova nei dispositivi Windows 10. Il plug-in di push PhoneGap è supportato in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9672e-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="9672e-235">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9672e-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="9672e-236">Registrare l'app di Windows per le notifiche push con WNS</span><span class="sxs-lookup"><span data-stu-id="9672e-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="9672e-237">Per usare le opzioni di Store in Visual Studio, selezionare una destinazione Windows dall'elenco Piattaforme soluzione, ad esempio **Windows-x64** o **Windows-x86**. Evitare **Windows-AnyCPU** per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="9672e-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="9672e-238">[Guardare un video che illustra una procedura simile][13]</span><span class="sxs-lookup"><span data-stu-id="9672e-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="9672e-239">Configurare l'hub di notifica per WNS</span><span class="sxs-lookup"><span data-stu-id="9672e-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="9672e-240">Configurare l'app Cordova per il supporto delle notifiche push di Windows</span><span class="sxs-lookup"><span data-stu-id="9672e-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="9672e-241">Aprire Progettazione configurazione facendo clic con il pulsante destro del mouse sul file config.xml e scegliendo **Visualizza finestra di progettazione**. Selezionare quindi la scheda **Windows** e scegliere **Windows 10** in **Versione Windows di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="9672e-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="9672e-242">Per supportare le notifiche push nelle compilazioni predefinite (debug), aprire il file build.json.</span><span class="sxs-lookup"><span data-stu-id="9672e-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="9672e-243">Copiare la configurazione "release" nella configurazione di debug.</span><span class="sxs-lookup"><span data-stu-id="9672e-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="9672e-244">Dopo l'aggiornamento, il file build.json deve contenere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9672e-244">After the update, the build.json should contain the following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="9672e-245">Compilare l'app e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="9672e-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="9672e-246">A questo punto l'app client dovrebbe eseguire la registrazione per le notifiche dal back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="9672e-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="9672e-247">Ripetere questa sezione per ogni progetto Windows nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="9672e-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="9672e-248">Testare le notifiche push nell'app di Windows</span><span class="sxs-lookup"><span data-stu-id="9672e-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="9672e-249">In Visual Studio verificare che sia selezionata una piattaforma Windows come destinazione di distribuzione, ad esempio **Windows-x64** o **Windows-x86**.</span><span class="sxs-lookup"><span data-stu-id="9672e-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="9672e-250">Per eseguire l'app in un PC con Windows 10 che ospita Visual Studio, scegliere **Computer locale**.</span><span class="sxs-lookup"><span data-stu-id="9672e-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="9672e-251">Premere il pulsante Esegui per compilare il progetto e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="9672e-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="9672e-252">Nell'app digitare un nome per un nuovo elemento todoitem, quindi fare clic sull'icona del segno più (+) per aggiungerlo.</span><span class="sxs-lookup"><span data-stu-id="9672e-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="9672e-253">Assicurarsi di ricevere una notifica quando viene aggiunto l'elemento.</span><span class="sxs-lookup"><span data-stu-id="9672e-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="9672e-254"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9672e-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="9672e-255">Per informazioni sulle notifiche push, vedere [Hub di notifica di Azure][17].</span><span class="sxs-lookup"><span data-stu-id="9672e-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="9672e-256">Se non è già stato fatto, proseguire con l'esercitazione [aggiungendo l'autenticazione][14] all'app Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="9672e-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="9672e-257">Informazioni su come usare gli SDK.</span><span class="sxs-lookup"><span data-stu-id="9672e-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="9672e-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="9672e-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="9672e-259">[ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="9672e-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="9672e-260">[Node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="9672e-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
