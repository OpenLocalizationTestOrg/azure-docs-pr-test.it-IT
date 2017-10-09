---
title: le notifiche Push di aaaAdd tooApache Cordova App con App mobili di Azure | Documenti Microsoft
description: Informazioni su app di Apache Cordova tooyour le notifiche push toouse toosend di App mobili di Azure.
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
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="26514-103">Aggiungere app Apache Cordova tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="26514-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="26514-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="26514-104">Overview</span></span>
<span data-ttu-id="26514-105">In questa esercitazione, progetto toohello [avvio rapido di Apache Cordova] di notifiche push è aggiungere in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="26514-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="26514-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="26514-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="26514-107">Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="26514-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="26514-108"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="26514-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="26514-109">In questa esercitazione illustra un'applicazione di Apache Cordova sviluppata con Visual Studio 2015 che viene eseguito su hello emulatore Android di Google, un dispositivo Android, un dispositivo Windows e un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="26514-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="26514-110">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="26514-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="26514-111">Un computer in cui è installato [Visual Studio Community 2015][2] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="26514-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="26514-112">[Visual Studio Tools per Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="26514-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="26514-113">Un [account Azure attivo][3].</span><span class="sxs-lookup"><span data-stu-id="26514-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="26514-114">Un progetto di [avvio rapido di Apache Cordova][5] completato.</span><span class="sxs-lookup"><span data-stu-id="26514-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="26514-115">(Android) Un [account Google][6] con un indirizzo di posta elettronica verificato.</span><span class="sxs-lookup"><span data-stu-id="26514-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="26514-116">(iOS) [Iscrizione all'Apple Developer Program][7] e un dispositivo iOS. Il simulatore iOS non supporta le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="26514-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="26514-117">(Windows) Un [account per sviluppatore di Windows Store][8] e un dispositivo Windows 10.</span><span class="sxs-lookup"><span data-stu-id="26514-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="26514-118"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="26514-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="26514-119">[Guardare un video che illustra la procedura disponibile in questa sezione][9]</span><span class="sxs-lookup"><span data-stu-id="26514-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="26514-120">Aggiornare project server hello</span><span class="sxs-lookup"><span data-stu-id="26514-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="26514-121"><a name="add-push-to-app"></a>Modificare l'app Cordova</span><span class="sxs-lookup"><span data-stu-id="26514-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="26514-122">Verificare che il progetto di app Apache Cordova sia le notifiche push toohandle pronto per l'installazione del plug-in push di Cordova hello più tutti i servizi push specifico della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="26514-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="26514-123">Aggiornare la versione di Cordova hello nel progetto.</span><span class="sxs-lookup"><span data-stu-id="26514-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="26514-124">Se il progetto usa una versione precedente a v6.1.1 di Apache Cordova, è possibile aggiornare il progetto di client hello.</span><span class="sxs-lookup"><span data-stu-id="26514-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="26514-125">progetto hello tooupdate:</span><span class="sxs-lookup"><span data-stu-id="26514-125">tooupdate hello project:</span></span>

* <span data-ttu-id="26514-126">Fare doppio clic su `config.xml` tooopen finestra di progettazione configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="26514-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="26514-127">Selezionare una scheda piattaforme hello.</span><span class="sxs-lookup"><span data-stu-id="26514-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="26514-128">Scegliere 6.1.1 hello **Cordova CLI** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="26514-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="26514-129">Scegliere **compilare**, quindi **Compila soluzione** progetto hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="26514-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="26514-130">Installazione di plug-in di hello push</span><span class="sxs-lookup"><span data-stu-id="26514-130">Install hello push plugin</span></span>
<span data-ttu-id="26514-131">Le applicazioni Apache Cordova non gestiscono in modo nativo le funzionalità del dispositivo o della rete.</span><span class="sxs-lookup"><span data-stu-id="26514-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="26514-132">Queste funzionalità sono incluse nei plug-in che vengono pubblicati in [npm][10] o GitHub.</span><span class="sxs-lookup"><span data-stu-id="26514-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="26514-133">Hello `phonegap-plugin-push` plug-in è toohandle utilizzato le notifiche push di rete.</span><span class="sxs-lookup"><span data-stu-id="26514-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="26514-134">È possibile installare plug-in push hello in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26514-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="26514-135">**Dal prompt hello:**</span><span class="sxs-lookup"><span data-stu-id="26514-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="26514-136">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="26514-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="26514-137">**Da Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="26514-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="26514-138">In Esplora soluzioni, aprire hello `config.xml` fare clic su file **plug-in** > **personalizzato**selezionare **Git** come origine dell'installazione, quindi immettere `https://github.com/phonegap/phonegap-plugin-push`come origine di hello.</span><span class="sxs-lookup"><span data-stu-id="26514-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="26514-139">Fare clic su hello sulla freccia avanti toohello origine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="26514-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="26514-140">In **SENDER_ID**, se si dispone già di un ID progetto numerico per il progetto di Google Developer Console hello, è possibile aggiungere qui.</span><span class="sxs-lookup"><span data-stu-id="26514-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="26514-141">In caso contrario, immettere un valore segnaposto, ad esempio 777777.</span><span class="sxs-lookup"><span data-stu-id="26514-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="26514-142">Se la destinazione è Android, sarà possibile aggiornare questo valore nel file config.xml in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="26514-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="26514-143">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="26514-143">Click **Add**.</span></span>

<span data-ttu-id="26514-144">plug-in push Hello è ora installato.</span><span class="sxs-lookup"><span data-stu-id="26514-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="26514-145">Installazione di plug-in di hello dispositivo</span><span class="sxs-lookup"><span data-stu-id="26514-145">Install hello device plugin</span></span>
<span data-ttu-id="26514-146">Seguire hello stessa procedura utilizzata plug-in di tooinstall hello push.</span><span class="sxs-lookup"><span data-stu-id="26514-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="26514-147">Aggiungere plug-in di hello dispositivo dall'elenco di plug-in principali di hello (fare clic su **plug-in** > **Core** toofind è).</span><span class="sxs-lookup"><span data-stu-id="26514-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="26514-148">È necessario il nome della piattaforma hello tooobtain plug-in.</span><span class="sxs-lookup"><span data-stu-id="26514-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="26514-149">Registrare il dispositivo all'avvio dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="26514-149">Register your device on application start-up</span></span>
<span data-ttu-id="26514-150">Viene inizialmente incluso un codice minimo per Android.</span><span class="sxs-lookup"><span data-stu-id="26514-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="26514-151">Successivamente, si modificano hello app toorun su iOS o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="26514-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="26514-152">Aggiungere una chiamata troppo**registerForPushNotifications** durante il callback di hello per il processo di accesso di hello o nella parte inferiore di hello di hello **onDeviceReady** metodo:</span><span class="sxs-lookup"><span data-stu-id="26514-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="26514-153">Questo esempio illustra la chiamata a **registerForPushNotifications** al termine dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="26514-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="26514-154">È possibile chiamare `registerForPushNotifications()` ogni qualvolta è necessario.</span><span class="sxs-lookup"><span data-stu-id="26514-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="26514-155">Aggiungi nuova hello **registerForPushNotifications** metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="26514-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
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
3. <span data-ttu-id="26514-156">(Android) Nel codice precedente di hello, sostituire `Your_Project_ID` con numerica hello ID del progetto per l'app dal [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="26514-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="26514-157">(Facoltativo) Configurare ed eseguire l'applicazione hello in Android</span><span class="sxs-lookup"><span data-stu-id="26514-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="26514-158">Completare le notifiche push tooenable questa sezione per Android.</span><span class="sxs-lookup"><span data-stu-id="26514-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="26514-159"><a name="enable-gcm"></a>Abilitare Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="26514-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="26514-160">Poiché destinazione hello piattaforma Android di Google inizialmente, è necessario abilitare Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="26514-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="26514-161"><a name="configure-backend"></a>Configurare utilizzando FCM hello App Mobile back-end toosend push richieste</span><span class="sxs-lookup"><span data-stu-id="26514-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="26514-162">Configurare l'app Cordova per Android</span><span class="sxs-lookup"><span data-stu-id="26514-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="26514-163">Nell'app Cordova, aprire file config.xml e sostituire `Your_Project_ID` con numerica hello ID del progetto per l'app da hello [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="26514-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="26514-164">Aprire index.js e aggiornare toouse codice hello l'ID progetto numerico.</span><span class="sxs-lookup"><span data-stu-id="26514-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="26514-165"><a name="configure-device"></a>Configurare il dispositivo Android per il debug USB</span><span class="sxs-lookup"><span data-stu-id="26514-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="26514-166">Prima di poter distribuire il tooyour applicazione dispositivo Android, è necessario tooenable debug USB.</span><span class="sxs-lookup"><span data-stu-id="26514-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="26514-167">Sul telefono Android seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26514-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="26514-168">Andare troppo**impostazioni** > **informazioni sul telefono**, quindi toccare hello **numero Build** fino a quando la modalità sviluppatore è abilitata (circa sette volte).</span><span class="sxs-lookup"><span data-stu-id="26514-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="26514-169">In **impostazioni** > **opzioni per gli sviluppatori** abilitare **debug USB**, quindi connettere il computer di sviluppo tooyour telefono Android tramite un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="26514-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="26514-170">Per questo test è stato usato un dispositivo Google Nexus 5X con Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="26514-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="26514-171">Tuttavia, le tecniche di hello sono comuni a qualsiasi versione di Android moderne.</span><span class="sxs-lookup"><span data-stu-id="26514-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="26514-172">Installare servizi Google Play</span><span class="sxs-lookup"><span data-stu-id="26514-172">Install Google Play Services</span></span>
<span data-ttu-id="26514-173">plug-in di Hello push si basa su Android Google Play Services per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="26514-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="26514-174">In Visual Studio, fare clic su **strumenti** > **Android** > **Android SDK Manager**, espandere hello **extra** cartella e verificare hello casella toomake che ognuno di hello seguenti SDK sia installato.</span><span class="sxs-lookup"><span data-stu-id="26514-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="26514-175">Android 2.3 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="26514-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="26514-176">Google Repository 27 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="26514-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="26514-177">Google Play Services 9.0.2 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="26514-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="26514-178">Fare clic su **installare pacchetti** e attendere toocomplete installazione hello.</span><span class="sxs-lookup"><span data-stu-id="26514-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="26514-179">Hello corrente necessarie librerie sono elencate in hello [nella documentazione di installazione push di plug-in di phonegap][19].</span><span class="sxs-lookup"><span data-stu-id="26514-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="26514-180">Notifiche push di test in hello app in Android</span><span class="sxs-lookup"><span data-stu-id="26514-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="26514-181">È possibile ora le notifiche push di test eseguendo hello app e gli elementi di inserimento nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="26514-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="26514-182">È possibile eseguire test da hello stesso dispositivo o da un secondo dispositivo, purché si utilizza hello stesso back-end.</span><span class="sxs-lookup"><span data-stu-id="26514-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="26514-183">Testare l'app Cordova nella piattaforma Android hello in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="26514-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="26514-184">**In un dispositivo fisico:** collegare il computer di sviluppo tooyour dispositivo Android con un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="26514-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="26514-185">Invece di selezionare **Emulatore Android di Google**, selezionare **Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="26514-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="26514-186">Visual Studio distribuisce dispositivo toohello di applicazione hello e quindi esegue un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="26514-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="26514-187">È quindi possibile interagire con un'applicazione hello sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="26514-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="26514-188">Migliorare l'esperienza di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="26514-188">Improve your development experience.</span></span>  <span data-ttu-id="26514-189">Le applicazioni per la condivisione dello schermo come [Mobizen][20] possono facilitare lo sviluppo di un'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="26514-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="26514-190">Mobizen progetti Android schermata tooa web browser nel PC.</span><span class="sxs-lookup"><span data-stu-id="26514-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="26514-191">**In un emulatore Android:** sono necessari altri passaggi di configurazione per l'esecuzione in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="26514-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="26514-192">Verificare che si sta distribuendo periferica virtuale tooa con Google APIs impostato come destinazione di hello, come illustrato nella console di gestione hello dispositivo virtuale Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="26514-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="26514-193">Se si desidera toouse un x86 più veloce dell'emulatore, è [installare driver HAXM hello] [ 11] e configurare toouse emulatore hello è.</span><span class="sxs-lookup"><span data-stu-id="26514-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="26514-194">Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**, seguire i prompt hello.</span><span class="sxs-lookup"><span data-stu-id="26514-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="26514-195">Eseguire l'applicazione hello come prima e inserire un nuovo elemento di attività.</span><span class="sxs-lookup"><span data-stu-id="26514-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="26514-196">Questa volta, viene visualizzata un'icona di notifica nell'area di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="26514-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="26514-197">È possibile aprire hello notifica cassetto tooview hello full-text della notifica hello.</span><span class="sxs-lookup"><span data-stu-id="26514-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="26514-198">(Facoltativo) Configurare ed eseguire l'app in iOS</span><span class="sxs-lookup"><span data-stu-id="26514-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="26514-199">In questa sezione è per l'esecuzione di progetto Cordova hello nei dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="26514-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="26514-200">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="26514-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="26514-201">Installare e hello esecuzione iOS remoto agente di compilazione su un Mac o un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="26514-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="26514-202">Prima di eseguire un'app Cordova in iOS usando Visual Studio, eseguire passaggi di hello in hello [iOS Guida all'installazione] [ 12] tooinstall e hello esecuzione remota di agente di compilazione.</span><span class="sxs-lookup"><span data-stu-id="26514-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="26514-203">Verificare che sia possibile compilare hello app per iOS.</span><span class="sxs-lookup"><span data-stu-id="26514-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="26514-204">Hello passaggi nella Guida alla configurazione di hello sono necessari toobuild per iOS da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26514-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="26514-205">Se non si dispone di un computer Mac, è possibile compilare per iOS usando l'agente di compilazione remota hello in un servizio, ad esempio MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="26514-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="26514-206">Per altre informazioni, vedere [eseguire app iOS nel cloud hello][21].</span><span class="sxs-lookup"><span data-stu-id="26514-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="26514-207">XCode 7 o versione successiva è richiesto toouse hello push plugin in iOS.</span><span class="sxs-lookup"><span data-stu-id="26514-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="26514-208">Trovare hello ID toouse come ID App</span><span class="sxs-lookup"><span data-stu-id="26514-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="26514-209">Prima di registrare l'app per le notifiche push, aprire config.xml nell'app Cordova, trovare hello `id` valore nell'elemento widget hello dell'attributo e copiarlo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="26514-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="26514-210">In hello XML seguente, l'ID di hello è `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="26514-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="26514-211">Questo identificatore verrà usato in un secondo momento, durante la creazione di un ID app nel portale per sviluppatori di Apple.</span><span class="sxs-lookup"><span data-stu-id="26514-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="26514-212">Se si crea un ID diverso di App nel portale per sviluppatori di hello, è necessario eseguire alcuni passaggi aggiuntivi più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="26514-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="26514-213">ID di Hello nell'elemento widget deve corrispondere hello ID App nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="26514-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="26514-214">Registrare l'applicazione hello per le notifiche push nel portale per sviluppatori di Apple</span><span class="sxs-lookup"><span data-stu-id="26514-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="26514-215">Guardare un video che illustra una procedura simile</span><span class="sxs-lookup"><span data-stu-id="26514-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="26514-216">Configurare le notifiche push toosend Azure</span><span class="sxs-lookup"><span data-stu-id="26514-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="26514-217">Verificare che l'ID app corrisponda all'app Cordova</span><span class="sxs-lookup"><span data-stu-id="26514-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="26514-218">Se corrisponde a hello ID App creato nel tuo Account sviluppatore Apple già hello ID dell'elemento widget hello in config.xml, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="26514-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="26514-219">Tuttavia, se hello ID non corrispondono, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="26514-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="26514-220">Elimina cartella platforms hello dal progetto.</span><span class="sxs-lookup"><span data-stu-id="26514-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="26514-221">Elimina cartella plug-in di hello dal progetto.</span><span class="sxs-lookup"><span data-stu-id="26514-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="26514-222">Elimina cartella node_modules hello dal progetto.</span><span class="sxs-lookup"><span data-stu-id="26514-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="26514-223">Aggiornare hello id attributo dell'elemento widget hello in config.xml toouse hello ID App creata con l'Account per sviluppatori di Apple.</span><span class="sxs-lookup"><span data-stu-id="26514-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="26514-224">Ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="26514-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="26514-225">Testare le notifiche push nell'app iOS</span><span class="sxs-lookup"><span data-stu-id="26514-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="26514-226">In Visual Studio, assicurarsi che **iOS** selezionato come destinazione di distribuzione hello e quindi scegliere **dispositivo** toorun sul dispositivo iOS connesso.</span><span class="sxs-lookup"><span data-stu-id="26514-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="26514-227">È possibile eseguire su un tooyour dispositivo connesso iOS PC con iTunes.</span><span class="sxs-lookup"><span data-stu-id="26514-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="26514-228">Simulatore iOS Hello non supporta le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="26514-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="26514-229">Hello premere **eseguire** pulsante o **F5** in Visual Studio toobuild progetto hello inizio hello app in un dispositivo iOS, quindi fare clic su **OK** tooaccept le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="26514-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26514-230">app Hello viene richiesta una conferma per le notifiche push durante la prima esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="26514-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="26514-231">Nell'app hello, digitare un'attività e quindi fare clic su hello più (+) icona.</span><span class="sxs-lookup"><span data-stu-id="26514-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="26514-232">Verificare che viene ricevuta una notifica, quindi fare clic su OK toodismiss hello notifica.</span><span class="sxs-lookup"><span data-stu-id="26514-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="26514-233">(Facoltativo) Configurare ed eseguire l'app in Windows</span><span class="sxs-lookup"><span data-stu-id="26514-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="26514-234">In questa sezione è per l'esecuzione di progetto di app Apache Cordova hello nei dispositivi Windows 10 (plug-in di hello PhoneGap push è supportato in Windows 10).</span><span class="sxs-lookup"><span data-stu-id="26514-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="26514-235">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="26514-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="26514-236">Registrare l'app di Windows per le notifiche push con WNS</span><span class="sxs-lookup"><span data-stu-id="26514-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="26514-237">le opzioni di archivio hello toouse in Visual Studio, selezionare una destinazione di Windows dall'elenco piattaforme soluzione hello, ad esempio **Windows-x64** o **Windows-x86** (evitare **Windows AnyCPU** per le notifiche push).</span><span class="sxs-lookup"><span data-stu-id="26514-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="26514-238">[Guardare un video che illustra una procedura simile][13]</span><span class="sxs-lookup"><span data-stu-id="26514-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="26514-239">Configurazione dell'hub di notifica hello per WNS</span><span class="sxs-lookup"><span data-stu-id="26514-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="26514-240">Configurare le notifiche push di Windows toosupport di app di Cordova</span><span class="sxs-lookup"><span data-stu-id="26514-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="26514-241">Finestra di progettazione configurazione hello aprire (destro del mouse sul file config.xml e selezionare **Visualizza finestra di progettazione**), selezionare hello **Windows** scheda e scegliere **Windows 10** in **Windows versione**.</span><span class="sxs-lookup"><span data-stu-id="26514-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="26514-242">compilazioni di notifiche push toosupport nel predefinito (debug), build.json aprire file.</span><span class="sxs-lookup"><span data-stu-id="26514-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="26514-243">Copiare la configurazione di debug tooyour configurazione "versione".</span><span class="sxs-lookup"><span data-stu-id="26514-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="26514-244">Dopo l'aggiornamento di hello, hello build.json deve contenere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="26514-244">After hello update, hello build.json should contain hello following code:</span></span>

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

<span data-ttu-id="26514-245">Compilare app hello e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="26514-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="26514-246">L'app client deve ora registrarsi per le notifiche di hello dal back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="26514-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="26514-247">Ripetere questa sezione per ogni progetto Windows nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="26514-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="26514-248">Testare le notifiche push nell'app di Windows</span><span class="sxs-lookup"><span data-stu-id="26514-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="26514-249">In Visual Studio, assicurarsi che sia selezionata una piattaforma Windows come destinazione di distribuzione hello, ad esempio **Windows-x64** o **Windows-x86**.</span><span class="sxs-lookup"><span data-stu-id="26514-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="26514-250">toorun hello app nei PC Windows 10 che ospita Visual Studio, scegliere **computer locale**.</span><span class="sxs-lookup"><span data-stu-id="26514-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="26514-251">Hello premere eseguire pulsante toobuild hello progetto e avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="26514-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="26514-252">Nell'app hello, digitare un nome per un oggetto todoitem nuovo e quindi fare clic su hello più (+) tooadd icona è.</span><span class="sxs-lookup"><span data-stu-id="26514-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="26514-253">Verificare che viene ricevuta una notifica quando viene aggiunto l'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="26514-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="26514-254"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26514-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="26514-255">Conoscenza [gli hub di notifica] [ 17] toolearn sulle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="26514-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="26514-256">Se non è già stato fatto, continuare l'esercitazione di hello da [aggiunta Authentication] [ 14] tooyour app di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="26514-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="26514-257">Informazioni su come toouse hello SDK.</span><span class="sxs-lookup"><span data-stu-id="26514-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="26514-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="26514-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="26514-259">[ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="26514-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="26514-260">[Node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="26514-260">[Node.js Server SDK][16]</span></span>

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
