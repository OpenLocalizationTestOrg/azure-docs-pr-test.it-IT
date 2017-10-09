---
title: app xamarin. Forms di aaaAdd push notifiche tooyour | Documenti Microsoft
description: Informazioni su come toouse Azure servizi toosend multipiattaforma push notifiche tooyour xamarin. Forms app.
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Aggiungere app xamarin. Forms tooyour di notifiche push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, aggiungere i progetti push notifiche tooall hello derivante da hello [avvio rapido di xamarin. Forms](app-service-mobile-xamarin-forms-get-started.md). Ciò significa che push viene inviata una notifica client multipiattaforma tooall ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push. Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Prerequisiti
Per iOS sono necessari un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/). Hello [simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Aggiornare le notifiche push di hello server progetto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Configurare ed eseguire progetto Android hello (facoltativo)
Completare questa sezione tooenable le notifiche push per hello progetto Droid xamarin. Forms per Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Abilitare Firebase Cloud Messaging (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Configurare hello App per dispositivi mobili back-end toosend push richieste tramite FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Aggiungi progetto Android toohello di notifiche push
Con hello back-end configurato con FCM, è possibile aggiungere componenti e i codici tooregister client toohello con FCM. È anche possibile registrare le notifiche di push con hub di notifica di Azure tramite hello fine, indietro App per dispositivi mobili e ricevere le notifiche.

1. In hello **Droid** del progetto, fare doppio clic su hello **componenti** cartella e fare clic su **ottenere più componenti...** . Cercare quindi hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto. Questo componente supporta le notifiche push per un progetto Xamarin Android.
2. Aprire il file di progetto Mainactivity hello e aggiungere hello seguente istruzione all'inizio di hello del file hello:

        using Gcm.Client;
3. Aggiungere i seguenti toohello codice hello **OnCreate** chiamata del metodo dopo hello troppo**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Aggiungere un nuovo metodo helper **CreateAndShowDialog** , come indicato di seguito:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Aggiungere i seguenti toohello codice hello **MainActivity** classe:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    Espone hello corrente **MainActivity** istanza, pertanto è possibile eseguire sul thread dell'interfaccia utente principale di hello.
6. Inizializzare hello `instance` variabile all'inizio di hello di hello **OnCreate** (metodo), come indicato di seguito.

        // Set hello current instance of MainActivity.
        instance = this;
7. Aggiungere un nuovo toohello di file di classe **Droid** progetto denominato `GcmService.cs`e che hello seguenti **utilizzando** istruzioni presenti nella parte superiore di hello del file hello:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Aggiungere hello seguente all'inizio di hello del file hello, le richieste di autorizzazione dopo hello **utilizzando** istruzioni e prima di hello **dello spazio dei nomi** dichiarazione.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Aggiungere hello seguente spazio dei nomi toohello definizione di classe.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Sostituire **<PROJECT_NUMBER>** con il numero di progetto annotato in precedenza.    
   >
   >
10. Sostituire hello vuoto **GcmService** classe con hello seguente di codice che utilizza ricevitore broadcast nuovo hello:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Aggiungere i seguenti toohello codice hello **GcmService** classe. Esegue l'override hello **OnRegistered** gestore eventi e implementa un **registrare** metodo.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Si noti che questo codice Usa hello `messageParam` parametro nella registrazione del modello hello.
12. Aggiungere hello seguente di codice che implementa **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Questo gestisce le notifiche in arrivo e li invia toohello notification manager toobe visualizzato.
13. **GcmServiceBase** richiede anche hello tooimplement **OnUnRegistered** e **OnError** metodi del gestore, che è possibile procedere come segue:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

A questo punto, si test pronto le notifiche push hello app in esecuzione in un dispositivo Android o hello emulatore.

### <a name="test-push-notifications-in-your-android-app"></a>Testare le notifiche push nell'app Android
Hello primi due passaggi sono necessari solo quando si verifica in un emulatore.

1. Assicurarsi che si sta distribuendo tooor debug in un dispositivo virtuale con Google APIs impostato come destinazione di hello, come illustrato di seguito nella console di gestione dispositivo virtuale Android hello.
2. Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**. Seguire quindi hello richieste tooadd un dispositivo di toohello account Google esistente o toocreate uno nuovo.
3. In Visual Studio o Xamarin Studio, fare doppio clic su hello **Droid** sul progetto e scegliere **imposta come progetto di avvio**.
4. Fare clic su **eseguire** toobuild hello progetto e avviare l'applicazione hello in un emulatore o il dispositivo Android.
5. Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.
6. Assicurarsi di ricevere una notifica quando viene aggiunto un elemento.

## <a name="configure-and-run-hello-ios-project-optional"></a>Configurare ed eseguire un progetto iOS hello (facoltativo)
In questa sezione è per l'esecuzione di progetto di hello Xamarin iOS per i dispositivi iOS. Se non si usano dispositivi iOS, è possibile ignorare questa sezione.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Configurazione dell'hub di notifica hello per servizio APN
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Successivamente, configurare l'impostazione di progetto iOS hello in Xamarin Studio o Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Aggiungere app per iOS tooyour le notifiche push
1. In hello **iOS** del progetto, aprire appdelegate. cs e aggiungere hello top toohello istruzione hello del file di codice seguente.

        using Newtonsoft.Json.Linq;
2. In hello **AppDelegate** classe, aggiungere una sostituzione per hello **RegisteredForRemoteNotifications** tooregister eventi per le notifiche:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. In **AppDelegate**, aggiungere anche hello seguente override per hello **DidReceiveRemoteNotification** gestore eventi:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Questo metodo gestisce le notifiche in ingresso durante l'esecuzione di app hello.
4. In hello **AppDelegate** classe, aggiungere hello seguente codice toohello **FinishedLaunching** metodo:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    L'aggiunta di questo codice consente il supporto per le notifiche remote e richiede la registrazione push.

L'app è notifiche push toosupport aggiornato.

#### <a name="test-push-notifications-in-your-ios-app"></a>Testare le notifiche push nell'app iOS
1. Fare clic sul progetto iOS hello e fare clic su **imposta come progetto di avvio**.
2. Hello premere **eseguire** pulsante o **F5** in Visual Studio toobuild hello progetto e avviare l'applicazione hello in un dispositivo iOS. Quindi fare clic su **OK** tooaccept le notifiche push.

   > [!NOTE]
   > È necessario accettare le notifiche push in modo esplicito dall'app. Questa richiesta si verifica solo hello prima volta che l'esecuzione applicazione hello.
   >
   >
3. Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.
4. Verificare che viene ricevuta una notifica e quindi fare clic su **OK** toodismiss hello notifica.

## <a name="configure-and-run-windows-projects-optional"></a>Configurare ed eseguire progetti Windows (facoltativo)
In questa sezione è per l'esecuzione di xamarin. Forms WinApp e WinPhone81 progetti per dispositivi Windows hello. Questa procedura supporta anche progetti per la piattaforma UWP (Universal Windows Platform). Se non si usano dispositivi Windows, è possibile ignorare questa sezione.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Registrare l'app Windows per le notifiche push con il servizio di notifica Windows (WNS)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configurazione dell'hub di notifica hello per WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Aggiungere app di Windows tooyour le notifiche push
1. In Visual Studio, aprire **App.xaml.cs** in un progetto e aggiungere hello seguendo le istruzioni.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Sostituire `<your_TodoItemManager_portable_class_namespace>` con spazio dei nomi hello del progetto portabile contenente hello `TodoItemManager` classe.
2. In App.xaml.cs, aggiungere hello seguente **InitNotificationsAsync** metodo:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Questo metodo ottiene canale di notifica push di hello e registra le notifiche di modello tooreceive un modello da hub di notifica. Una notifica di modello che supporta *messageParam* verrà recapitato toothis client.
3. In App.xaml.cs, aggiornare hello **OnLaunched** definizione di metodo di gestore eventi aggiungendo hello `async` modificatore. Aggiungere quindi hello successiva riga di codice alla fine di hello del metodo hello:

        await InitNotificationsAsync();

    Ciò garantisce che registrazione della notifica push hello viene creata o aggiornata ogni volta che viene avviata l'applicazione hello. È importante toodo questo tooguarantee che hello WNS push channel è sempre attivo.  
4. In Esplora soluzioni per Visual Studio, aprire hello **package. appxmanifest** file e impostare **in grado di tipo avviso popup** troppo**Sì** in **notifiche**.
5. Compilare l'applicazione hello e verificare che non siano presenti errori. L'applicazione client deve ora registrarsi per hello modello notifiche inviate dal hello che terminare nuovamente App per dispositivi mobili. Ripetere questa sezione per ogni progetto Windows nella soluzione.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testare le notifiche push nell'app di Windows
1. In Visual Studio fare clic con il pulsante destro del mouse su un progetto Windows e quindi scegliere **Imposta come progetto di avvio**.
2. Hello premere **eseguire** pulsante progetto hello toobuild e avviare l'applicazione hello.
3. Nell'app hello, digitare un nome per un oggetto todoitem nuovo e quindi fare clic su hello segno più (**+**) tooadd icona è.
4. Verificare che viene ricevuta una notifica quando viene aggiunto l'elemento hello.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulle notifiche push:

* [Diagnose push notification issues](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  (Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi. Questo argomento viene illustrato come tooanalyze e individuare la radice hello causa dell'assenza di errori di notifica push.

È anche possibile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app tooyour authentication](app-service-mobile-xamarin-forms-get-started-users.md)  
  Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.
* [Abilitare la sincronizzazione offline per l'app](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Informazioni su come tooadd supporto offline per l'app usando un App per dispositivi mobili back-end. Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
