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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Aggiungere app Apache Cordova tooyour di notifiche push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, progetto toohello [avvio rapido di Apache Cordova] di notifiche push è aggiungere in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario hello pacchetto estensione di notifica push. Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][1].

## <a name="prerequisites"></a>Prerequisiti
In questa esercitazione illustra un'applicazione di Apache Cordova sviluppata con Visual Studio 2015 che viene eseguito su hello emulatore Android di Google, un dispositivo Android, un dispositivo Windows e un dispositivo iOS.

toocomplete questa esercitazione, è necessario:

* Un computer in cui è installato [Visual Studio Community 2015][2] o versione successiva.
* [Visual Studio Tools per Apache Cordova][4].
* Un [account Azure attivo][3].
* Un progetto di [avvio rapido di Apache Cordova][5] completato.
* (Android) Un [account Google][6] con un indirizzo di posta elettronica verificato.
* (iOS) [Iscrizione all'Apple Developer Program][7] e un dispositivo iOS. Il simulatore iOS non supporta le notifiche push.
* (Windows) Un [account per sviluppatore di Windows Store][8] e un dispositivo Windows 10.

## <a name="configure-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Guardare un video che illustra la procedura disponibile in questa sezione][9]

## <a name="update-hello-server-project"></a>Aggiornare project server hello
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modificare l'app Cordova
Verificare che il progetto di app Apache Cordova sia le notifiche push toohandle pronto per l'installazione del plug-in push di Cordova hello più tutti i servizi push specifico della piattaforma.

#### <a name="update-hello-cordova-version-in-your-project"></a>Aggiornare la versione di Cordova hello nel progetto.
Se il progetto usa una versione precedente a v6.1.1 di Apache Cordova, è possibile aggiornare il progetto di client hello. progetto hello tooupdate:

* Fare doppio clic su `config.xml` tooopen finestra di progettazione configurazione hello.
* Selezionare una scheda piattaforme hello.
* Scegliere 6.1.1 hello **Cordova CLI** casella di testo.
* Scegliere **compilare**, quindi **Compila soluzione** progetto hello tooupdate.

#### <a name="install-hello-push-plugin"></a>Installazione di plug-in di hello push
Le applicazioni Apache Cordova non gestiscono in modo nativo le funzionalità del dispositivo o della rete.  Queste funzionalità sono incluse nei plug-in che vengono pubblicati in [npm][10] o GitHub.  Hello `phonegap-plugin-push` plug-in è toohandle utilizzato le notifiche push di rete.

È possibile installare plug-in push hello in uno dei modi seguenti:

**Dal prompt hello:**

Eseguire hello comando seguente:

    cordova plugin add phonegap-plugin-push

**Da Visual Studio:**

1. In Esplora soluzioni, aprire hello `config.xml` fare clic su file **plug-in** > **personalizzato**selezionare **Git** come origine dell'installazione, quindi immettere `https://github.com/phonegap/phonegap-plugin-push`come origine di hello.

   ![][img1]

2. Fare clic su hello sulla freccia avanti toohello origine dell'installazione.
3. In **SENDER_ID**, se si dispone già di un ID progetto numerico per il progetto di Google Developer Console hello, è possibile aggiungere qui. In caso contrario, immettere un valore segnaposto, ad esempio 777777.  Se la destinazione è Android, sarà possibile aggiornare questo valore nel file config.xml in un secondo momento.
4. Fare clic su **Aggiungi**.

plug-in push Hello è ora installato.

#### <a name="install-hello-device-plugin"></a>Installazione di plug-in di hello dispositivo
Seguire hello stessa procedura utilizzata plug-in di tooinstall hello push.  Aggiungere plug-in di hello dispositivo dall'elenco di plug-in principali di hello (fare clic su **plug-in** > **Core** toofind è). È necessario il nome della piattaforma hello tooobtain plug-in.

#### <a name="register-your-device-on-application-start-up"></a>Registrare il dispositivo all'avvio dell'applicazione
Viene inizialmente incluso un codice minimo per Android. Successivamente, si modificano hello app toorun su iOS o Windows 10.

1. Aggiungere una chiamata troppo**registerForPushNotifications** durante il callback di hello per il processo di accesso di hello o nella parte inferiore di hello di hello **onDeviceReady** metodo:

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

    Questo esempio illustra la chiamata a **registerForPushNotifications** al termine dell'autenticazione.  È possibile chiamare `registerForPushNotifications()` ogni qualvolta è necessario.

2. Aggiungi nuova hello **registerForPushNotifications** metodo come indicato di seguito:

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
3. (Android) Nel codice precedente di hello, sostituire `Your_Project_ID` con numerica hello ID del progetto per l'app dal [Google Developer Console][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Facoltativo) Configurare ed eseguire l'applicazione hello in Android
Completare le notifiche push tooenable questa sezione per Android.

#### <a name="enable-gcm"></a>Abilitare Firebase Cloud Messaging
Poiché destinazione hello piattaforma Android di Google inizialmente, è necessario abilitare Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Configurare utilizzando FCM hello App Mobile back-end toosend push richieste
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configurare l'app Cordova per Android
Nell'app Cordova, aprire file config.xml e sostituire `Your_Project_ID` con numerica hello ID del progetto per l'app da hello [Google Developer Console][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Aprire index.js e aggiornare toouse codice hello l'ID progetto numerico.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Configurare il dispositivo Android per il debug USB
Prima di poter distribuire il tooyour applicazione dispositivo Android, è necessario tooenable debug USB.  Sul telefono Android seguire questa procedura:

1. Andare troppo**impostazioni** > **informazioni sul telefono**, quindi toccare hello **numero Build** fino a quando la modalità sviluppatore è abilitata (circa sette volte).
2. In **impostazioni** > **opzioni per gli sviluppatori** abilitare **debug USB**, quindi connettere il computer di sviluppo tooyour telefono Android tramite un cavo USB.

Per questo test è stato usato un dispositivo Google Nexus 5X con Android 6.0 (Marshmallow).  Tuttavia, le tecniche di hello sono comuni a qualsiasi versione di Android moderne.

#### <a name="install-google-play-services"></a>Installare servizi Google Play
plug-in di Hello push si basa su Android Google Play Services per le notifiche push.

1. In Visual Studio, fare clic su **strumenti** > **Android** > **Android SDK Manager**, espandere hello **extra** cartella e verificare hello casella toomake che ognuno di hello seguenti SDK sia installato.

   * Android 2.3 o versione successiva
   * Google Repository 27 o versione successiva
   * Google Play Services 9.0.2 o versione successiva

2. Fare clic su **installare pacchetti** e attendere toocomplete installazione hello.

Hello corrente necessarie librerie sono elencate in hello [nella documentazione di installazione push di plug-in di phonegap][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Notifiche push di test in hello app in Android
È possibile ora le notifiche push di test eseguendo hello app e gli elementi di inserimento nella tabella TodoItem hello. È possibile eseguire test da hello stesso dispositivo o da un secondo dispositivo, purché si utilizza hello stesso back-end. Testare l'app Cordova nella piattaforma Android hello in uno dei seguenti modi hello:

* **In un dispositivo fisico:** collegare il computer di sviluppo tooyour dispositivo Android con un cavo USB.  Invece di selezionare **Emulatore Android di Google**, selezionare **Dispositivo**. Visual Studio distribuisce dispositivo toohello di applicazione hello e quindi esegue un'applicazione hello.  È quindi possibile interagire con un'applicazione hello sul dispositivo hello.

  Migliorare l'esperienza di sviluppo.  Le applicazioni per la condivisione dello schermo come [Mobizen][20] possono facilitare lo sviluppo di un'applicazione Android.  Mobizen progetti Android schermata tooa web browser nel PC.

* **In un emulatore Android:** sono necessari altri passaggi di configurazione per l'esecuzione in un emulatore.

    Verificare che si sta distribuendo periferica virtuale tooa con Google APIs impostato come destinazione di hello, come illustrato nella console di gestione hello dispositivo virtuale Android (AVD).

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Se si desidera toouse un x86 più veloce dell'emulatore, è [installare driver HAXM hello] [ 11] e configurare toouse emulatore hello è.

    Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**, seguire i prompt hello.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Eseguire l'applicazione hello come prima e inserire un nuovo elemento di attività. Questa volta, viene visualizzata un'icona di notifica nell'area di notifica hello. È possibile aprire hello notifica cassetto tooview hello full-text della notifica hello.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Facoltativo) Configurare ed eseguire l'app in iOS
In questa sezione è per l'esecuzione di progetto Cordova hello nei dispositivi iOS. Se non si usano dispositivi iOS, è possibile ignorare questa sezione.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Installare e hello esecuzione iOS remoto agente di compilazione su un Mac o un servizio cloud
Prima di eseguire un'app Cordova in iOS usando Visual Studio, eseguire passaggi di hello in hello [iOS Guida all'installazione] [ 12] tooinstall e hello esecuzione remota di agente di compilazione.

Verificare che sia possibile compilare hello app per iOS. Hello passaggi nella Guida alla configurazione di hello sono necessari toobuild per iOS da Visual Studio. Se non si dispone di un computer Mac, è possibile compilare per iOS usando l'agente di compilazione remota hello in un servizio, ad esempio MacInCloud. Per altre informazioni, vedere [eseguire app iOS nel cloud hello][21].

> [!NOTE]
> XCode 7 o versione successiva è richiesto toouse hello push plugin in iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Trovare hello ID toouse come ID App
Prima di registrare l'app per le notifiche push, aprire config.xml nell'app Cordova, trovare hello `id` valore nell'elemento widget hello dell'attributo e copiarlo per un uso successivo. In hello XML seguente, l'ID di hello è `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Questo identificatore verrà usato in un secondo momento, durante la creazione di un ID app nel portale per sviluppatori di Apple. Se si crea un ID diverso di App nel portale per sviluppatori di hello, è necessario eseguire alcuni passaggi aggiuntivi più avanti in questa esercitazione. ID di Hello nell'elemento widget deve corrispondere hello ID App nel portale per sviluppatori hello.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrare l'applicazione hello per le notifiche push nel portale per sviluppatori di Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Guardare un video che illustra una procedura simile](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Configurare le notifiche push toosend Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Verificare che l'ID app corrisponda all'app Cordova
Se corrisponde a hello ID App creato nel tuo Account sviluppatore Apple già hello ID dell'elemento widget hello in config.xml, è possibile ignorare questo passaggio. Tuttavia, se hello ID non corrispondono, eseguire hello alla procedura seguente:

1. Elimina cartella platforms hello dal progetto.
2. Elimina cartella plug-in di hello dal progetto.
3. Elimina cartella node_modules hello dal progetto.
4. Aggiornare hello id attributo dell'elemento widget hello in config.xml toouse hello ID App creata con l'Account per sviluppatori di Apple.
5. Ricompilare il progetto.

##### <a name="test-push-notifications-in-your-ios-app"></a>Testare le notifiche push nell'app iOS
1. In Visual Studio, assicurarsi che **iOS** selezionato come destinazione di distribuzione hello e quindi scegliere **dispositivo** toorun sul dispositivo iOS connesso.

    È possibile eseguire su un tooyour dispositivo connesso iOS PC con iTunes. Simulatore iOS Hello non supporta le notifiche push.

2. Hello premere **eseguire** pulsante o **F5** in Visual Studio toobuild progetto hello inizio hello app in un dispositivo iOS, quindi fare clic su **OK** tooaccept le notifiche push.

   > [!NOTE]
   > app Hello viene richiesta una conferma per le notifiche push durante la prima esecuzione hello.

3. Nell'app hello, digitare un'attività e quindi fare clic su hello più (+) icona.
4. Verificare che viene ricevuta una notifica, quindi fare clic su OK toodismiss hello notifica.

## <a name="optional-configure-and-run-on-windows"></a>(Facoltativo) Configurare ed eseguire l'app in Windows
In questa sezione è per l'esecuzione di progetto di app Apache Cordova hello nei dispositivi Windows 10 (plug-in di hello PhoneGap push è supportato in Windows 10). Se non si usano dispositivi Windows, è possibile ignorare questa sezione.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Registrare l'app di Windows per le notifiche push con WNS
le opzioni di archivio hello toouse in Visual Studio, selezionare una destinazione di Windows dall'elenco piattaforme soluzione hello, ad esempio **Windows-x64** o **Windows-x86** (evitare **Windows AnyCPU** per le notifiche push).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Guardare un video che illustra una procedura simile][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configurazione dell'hub di notifica hello per WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Configurare le notifiche push di Windows toosupport di app di Cordova
Finestra di progettazione configurazione hello aprire (destro del mouse sul file config.xml e selezionare **Visualizza finestra di progettazione**), selezionare hello **Windows** scheda e scegliere **Windows 10** in **Windows versione**.

compilazioni di notifiche push toosupport nel predefinito (debug), build.json aprire file. Copiare la configurazione di debug tooyour configurazione "versione".

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Dopo l'aggiornamento di hello, hello build.json deve contenere hello seguente codice:

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

Compilare app hello e verificare che non siano presenti errori. L'app client deve ora registrarsi per le notifiche di hello dal back-end di hello App per dispositivi mobili. Ripetere questa sezione per ogni progetto Windows nella soluzione.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testare le notifiche push nell'app di Windows
In Visual Studio, assicurarsi che sia selezionata una piattaforma Windows come destinazione di distribuzione hello, ad esempio **Windows-x64** o **Windows-x86**. toorun hello app nei PC Windows 10 che ospita Visual Studio, scegliere **computer locale**.

Hello premere eseguire pulsante toobuild hello progetto e avviare l'applicazione hello.

Nell'app hello, digitare un nome per un oggetto todoitem nuovo e quindi fare clic su hello più (+) tooadd icona è.

Verificare che viene ricevuta una notifica quando viene aggiunto l'elemento hello.

## <a name="next-steps"></a>Passaggi successivi
* Conoscenza [gli hub di notifica] [ 17] toolearn sulle notifiche push.
* Se non è già stato fatto, continuare l'esercitazione di hello da [aggiunta Authentication] [ 14] tooyour app di Apache Cordova.

Informazioni su come toouse hello SDK.

* [Apache Cordova SDK][15]
* [ASP.NET Server SDK][1]
* [Node.js Server SDK][16]

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
