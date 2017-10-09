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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="7949f-103">Aggiungere app xamarin. Forms tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="7949f-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="7949f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7949f-104">Overview</span></span>
<span data-ttu-id="7949f-105">In questa esercitazione, aggiungere i progetti push notifiche tooall hello derivante da hello [avvio rapido di xamarin. Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7949f-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="7949f-106">Ciò significa che push viene inviata una notifica client multipiattaforma tooall ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="7949f-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="7949f-107">Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="7949f-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="7949f-108">Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7949f-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7949f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7949f-109">Prerequisites</span></span>
<span data-ttu-id="7949f-110">Per iOS sono necessari un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="7949f-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="7949f-111">Hello [simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="7949f-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="7949f-112"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="7949f-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="7949f-113">Aggiornare le notifiche push di hello server progetto toosend</span><span class="sxs-lookup"><span data-stu-id="7949f-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="7949f-114">Configurare ed eseguire progetto Android hello (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="7949f-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="7949f-115">Completare questa sezione tooenable le notifiche push per hello progetto Droid xamarin. Forms per Android.</span><span class="sxs-lookup"><span data-stu-id="7949f-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="7949f-116">Abilitare Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="7949f-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="7949f-117">Configurare hello App per dispositivi mobili back-end toosend push richieste tramite FCM</span><span class="sxs-lookup"><span data-stu-id="7949f-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="7949f-118">Aggiungi progetto Android toohello di notifiche push</span><span class="sxs-lookup"><span data-stu-id="7949f-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="7949f-119">Con hello back-end configurato con FCM, è possibile aggiungere componenti e i codici tooregister client toohello con FCM.</span><span class="sxs-lookup"><span data-stu-id="7949f-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="7949f-120">È anche possibile registrare le notifiche di push con hub di notifica di Azure tramite hello fine, indietro App per dispositivi mobili e ricevere le notifiche.</span><span class="sxs-lookup"><span data-stu-id="7949f-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="7949f-121">In hello **Droid** del progetto, fare doppio clic su hello **componenti** cartella e fare clic su **ottenere più componenti...** . Cercare quindi hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="7949f-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="7949f-122">Questo componente supporta le notifiche push per un progetto Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="7949f-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="7949f-123">Aprire il file di progetto Mainactivity hello e aggiungere hello seguente istruzione all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="7949f-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="7949f-124">Aggiungere i seguenti toohello codice hello **OnCreate** chiamata del metodo dopo hello troppo**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="7949f-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

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
4. <span data-ttu-id="7949f-125">Aggiungere un nuovo metodo helper **CreateAndShowDialog** , come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7949f-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="7949f-126">Aggiungere i seguenti toohello codice hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="7949f-126">Add hello following code toohello **MainActivity** class:</span></span>

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

    <span data-ttu-id="7949f-127">Espone hello corrente **MainActivity** istanza, pertanto è possibile eseguire sul thread dell'interfaccia utente principale di hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="7949f-128">Inizializzare hello `instance` variabile all'inizio di hello di hello **OnCreate** (metodo), come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7949f-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="7949f-129">Aggiungere un nuovo toohello di file di classe **Droid** progetto denominato `GcmService.cs`e che hello seguenti **utilizzando** istruzioni presenti nella parte superiore di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="7949f-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="7949f-130">Aggiungere hello seguente all'inizio di hello del file hello, le richieste di autorizzazione dopo hello **utilizzando** istruzioni e prima di hello **dello spazio dei nomi** dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="7949f-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="7949f-131">Aggiungere hello seguente spazio dei nomi toohello definizione di classe.</span><span class="sxs-lookup"><span data-stu-id="7949f-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="7949f-132">Sostituire **<PROJECT_NUMBER>** con il numero di progetto annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7949f-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="7949f-133">Sostituire hello vuoto **GcmService** classe con hello seguente di codice che utilizza ricevitore broadcast nuovo hello:</span><span class="sxs-lookup"><span data-stu-id="7949f-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="7949f-134">Aggiungere i seguenti toohello codice hello **GcmService** classe.</span><span class="sxs-lookup"><span data-stu-id="7949f-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="7949f-135">Esegue l'override hello **OnRegistered** gestore eventi e implementa un **registrare** metodo.</span><span class="sxs-lookup"><span data-stu-id="7949f-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="7949f-136">Si noti che questo codice Usa hello `messageParam` parametro nella registrazione del modello hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="7949f-137">Aggiungere hello seguente di codice che implementa **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="7949f-137">Add hello following code that implements **OnMessage**:</span></span>

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

    <span data-ttu-id="7949f-138">Questo gestisce le notifiche in arrivo e li invia toohello notification manager toobe visualizzato.</span><span class="sxs-lookup"><span data-stu-id="7949f-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="7949f-139">**GcmServiceBase** richiede anche hello tooimplement **OnUnRegistered** e **OnError** metodi del gestore, che è possibile procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="7949f-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="7949f-140">A questo punto, si test pronto le notifiche push hello app in esecuzione in un dispositivo Android o hello emulatore.</span><span class="sxs-lookup"><span data-stu-id="7949f-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="7949f-141">Testare le notifiche push nell'app Android</span><span class="sxs-lookup"><span data-stu-id="7949f-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="7949f-142">Hello primi due passaggi sono necessari solo quando si verifica in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="7949f-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="7949f-143">Assicurarsi che si sta distribuendo tooor debug in un dispositivo virtuale con Google APIs impostato come destinazione di hello, come illustrato di seguito nella console di gestione dispositivo virtuale Android hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="7949f-144">Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**.</span><span class="sxs-lookup"><span data-stu-id="7949f-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="7949f-145">Seguire quindi hello richieste tooadd un dispositivo di toohello account Google esistente o toocreate uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7949f-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="7949f-146">In Visual Studio o Xamarin Studio, fare doppio clic su hello **Droid** sul progetto e scegliere **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="7949f-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="7949f-147">Fare clic su **eseguire** toobuild hello progetto e avviare l'applicazione hello in un emulatore o il dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="7949f-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="7949f-148">Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.</span><span class="sxs-lookup"><span data-stu-id="7949f-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="7949f-149">Assicurarsi di ricevere una notifica quando viene aggiunto un elemento.</span><span class="sxs-lookup"><span data-stu-id="7949f-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="7949f-150">Configurare ed eseguire un progetto iOS hello (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="7949f-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="7949f-151">In questa sezione è per l'esecuzione di progetto di hello Xamarin iOS per i dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="7949f-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="7949f-152">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="7949f-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="7949f-153">Configurazione dell'hub di notifica hello per servizio APN</span><span class="sxs-lookup"><span data-stu-id="7949f-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="7949f-154">Successivamente, configurare l'impostazione di progetto iOS hello in Xamarin Studio o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7949f-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="7949f-155">Aggiungere app per iOS tooyour le notifiche push</span><span class="sxs-lookup"><span data-stu-id="7949f-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="7949f-156">In hello **iOS** del progetto, aprire appdelegate. cs e aggiungere hello top toohello istruzione hello del file di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="7949f-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="7949f-157">In hello **AppDelegate** classe, aggiungere una sostituzione per hello **RegisteredForRemoteNotifications** tooregister eventi per le notifiche:</span><span class="sxs-lookup"><span data-stu-id="7949f-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="7949f-158">In **AppDelegate**, aggiungere anche hello seguente override per hello **DidReceiveRemoteNotification** gestore eventi:</span><span class="sxs-lookup"><span data-stu-id="7949f-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="7949f-159">Questo metodo gestisce le notifiche in ingresso durante l'esecuzione di app hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="7949f-160">In hello **AppDelegate** classe, aggiungere hello seguente codice toohello **FinishedLaunching** metodo:</span><span class="sxs-lookup"><span data-stu-id="7949f-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="7949f-161">L'aggiunta di questo codice consente il supporto per le notifiche remote e richiede la registrazione push.</span><span class="sxs-lookup"><span data-stu-id="7949f-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="7949f-162">L'app è notifiche push toosupport aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7949f-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="7949f-163">Testare le notifiche push nell'app iOS</span><span class="sxs-lookup"><span data-stu-id="7949f-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="7949f-164">Fare clic sul progetto iOS hello e fare clic su **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="7949f-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7949f-165">Hello premere **eseguire** pulsante o **F5** in Visual Studio toobuild hello progetto e avviare l'applicazione hello in un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="7949f-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="7949f-166">Quindi fare clic su **OK** tooaccept le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="7949f-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7949f-167">È necessario accettare le notifiche push in modo esplicito dall'app.</span><span class="sxs-lookup"><span data-stu-id="7949f-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="7949f-168">Questa richiesta si verifica solo hello prima volta che l'esecuzione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="7949f-169">Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.</span><span class="sxs-lookup"><span data-stu-id="7949f-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="7949f-170">Verificare che viene ricevuta una notifica e quindi fare clic su **OK** toodismiss hello notifica.</span><span class="sxs-lookup"><span data-stu-id="7949f-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="7949f-171">Configurare ed eseguire progetti Windows (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="7949f-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="7949f-172">In questa sezione è per l'esecuzione di xamarin. Forms WinApp e WinPhone81 progetti per dispositivi Windows hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="7949f-173">Questa procedura supporta anche progetti per la piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="7949f-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="7949f-174">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="7949f-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="7949f-175">Registrare l'app Windows per le notifiche push con il servizio di notifica Windows (WNS)</span><span class="sxs-lookup"><span data-stu-id="7949f-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="7949f-176">Configurazione dell'hub di notifica hello per WNS</span><span class="sxs-lookup"><span data-stu-id="7949f-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="7949f-177">Aggiungere app di Windows tooyour le notifiche push</span><span class="sxs-lookup"><span data-stu-id="7949f-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="7949f-178">In Visual Studio, aprire **App.xaml.cs** in un progetto e aggiungere hello seguendo le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="7949f-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="7949f-179">Sostituire `<your_TodoItemManager_portable_class_namespace>` con spazio dei nomi hello del progetto portabile contenente hello `TodoItemManager` classe.</span><span class="sxs-lookup"><span data-stu-id="7949f-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="7949f-180">In App.xaml.cs, aggiungere hello seguente **InitNotificationsAsync** metodo:</span><span class="sxs-lookup"><span data-stu-id="7949f-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="7949f-181">Questo metodo ottiene canale di notifica push di hello e registra le notifiche di modello tooreceive un modello da hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="7949f-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="7949f-182">Una notifica di modello che supporta *messageParam* verrà recapitato toothis client.</span><span class="sxs-lookup"><span data-stu-id="7949f-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="7949f-183">In App.xaml.cs, aggiornare hello **OnLaunched** definizione di metodo di gestore eventi aggiungendo hello `async` modificatore.</span><span class="sxs-lookup"><span data-stu-id="7949f-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="7949f-184">Aggiungere quindi hello successiva riga di codice alla fine di hello del metodo hello:</span><span class="sxs-lookup"><span data-stu-id="7949f-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="7949f-185">Ciò garantisce che registrazione della notifica push hello viene creata o aggiornata ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="7949f-186">È importante toodo questo tooguarantee che hello WNS push channel è sempre attivo.</span><span class="sxs-lookup"><span data-stu-id="7949f-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="7949f-187">In Esplora soluzioni per Visual Studio, aprire hello **package. appxmanifest** file e impostare **in grado di tipo avviso popup** troppo**Sì** in **notifiche**.</span><span class="sxs-lookup"><span data-stu-id="7949f-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="7949f-188">Compilare l'applicazione hello e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="7949f-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="7949f-189">L'applicazione client deve ora registrarsi per hello modello notifiche inviate dal hello che terminare nuovamente App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7949f-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="7949f-190">Ripetere questa sezione per ogni progetto Windows nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="7949f-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="7949f-191">Testare le notifiche push nell'app di Windows</span><span class="sxs-lookup"><span data-stu-id="7949f-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="7949f-192">In Visual Studio fare clic con il pulsante destro del mouse su un progetto Windows e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="7949f-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="7949f-193">Hello premere **eseguire** pulsante progetto hello toobuild e avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="7949f-194">Nell'app hello, digitare un nome per un oggetto todoitem nuovo e quindi fare clic su hello segno più (**+**) tooadd icona è.</span><span class="sxs-lookup"><span data-stu-id="7949f-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="7949f-195">Verificare che viene ricevuta una notifica quando viene aggiunto l'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="7949f-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7949f-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7949f-196">Next steps</span></span>
<span data-ttu-id="7949f-197">Altre informazioni sulle notifiche push:</span><span class="sxs-lookup"><span data-stu-id="7949f-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="7949f-198">Diagnose push notification issues</span><span class="sxs-lookup"><span data-stu-id="7949f-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="7949f-199">(Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7949f-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="7949f-200">Questo argomento viene illustrato come tooanalyze e individuare la radice hello causa dell'assenza di errori di notifica push.</span><span class="sxs-lookup"><span data-stu-id="7949f-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="7949f-201">È anche possibile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="7949f-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="7949f-202">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="7949f-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="7949f-203">Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="7949f-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="7949f-204">Abilitare la sincronizzazione offline per l'app</span><span class="sxs-lookup"><span data-stu-id="7949f-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="7949f-205">Informazioni su come tooadd supporto offline per l'app usando un App per dispositivi mobili back-end.</span><span class="sxs-lookup"><span data-stu-id="7949f-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="7949f-206">Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="7949f-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
