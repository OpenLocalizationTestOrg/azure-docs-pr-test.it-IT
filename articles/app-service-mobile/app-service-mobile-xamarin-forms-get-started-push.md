---
title: Aggiungere notifiche push all'app Xamarin.Forms | Microsoft Docs
description: Informazioni su come usare i servizi di Azure per inviare notifiche push multipiattaforma alle app Xamarin.Forms.
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="b3b3f-103">Aggiungere notifiche push all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="b3b3f-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="b3b3f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b3b3f-104">Overview</span></span>
<span data-ttu-id="b3b3f-105">In questa esercitazione vengono aggiunte notifiche push a tutti i progetti creati nella [guida introduttiva per Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md),</span><span class="sxs-lookup"><span data-stu-id="b3b3f-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="b3b3f-106">in modo che a ogni inserimento di record venga inviata una notifica push a tutti i client multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="b3b3f-107">Se non si usa il progetto server di avvio rapido scaricato, sarà necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="b3b3f-108">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3b3f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b3b3f-109">Prerequisites</span></span>
<span data-ttu-id="b3b3f-110">Per iOS sono necessari un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="b3b3f-111">[Il simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="b3b3f-112"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="b3b3f-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="b3b3f-113">Aggiornare il progetto server per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="b3b3f-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="b3b3f-114">Configurare ed eseguire il progetto Android (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b3b3f-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="b3b3f-115">Completare questa sezione per abilitare le notifiche push per il progetto Xamarin.Forms Droid per Android.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="b3b3f-116">Abilitare Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="b3b3f-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="b3b3f-117">Configurare il back-end dell'app per dispositivi mobili per inviare richieste push usando FCM</span><span class="sxs-lookup"><span data-stu-id="b3b3f-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="b3b3f-118">Aggiungere notifiche push al progetto Android</span><span class="sxs-lookup"><span data-stu-id="b3b3f-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="b3b3f-119">Dopo aver configurato il back-end con FCM, è possibile aggiungere componenti e codici al client per la registrazione in FCM,</span><span class="sxs-lookup"><span data-stu-id="b3b3f-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="b3b3f-120">iscriversi alle notifiche push con l'Hub di notifica di Azure tramite il back-end dell'app per dispositivi mobili e ricevere notifiche.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="b3b3f-121">Nel progetto **Droid** fare doppio clic sulla cartella **Components** (Componenti) e scegliere **Get More Components...** (Recupera altri componenti...).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="b3b3f-122">Cercare quindi il componente **Google Cloud Messaging Client** (Client Google Cloud Messaging) e aggiungerlo al progetto.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="b3b3f-123">Questo componente supporta le notifiche push per un progetto Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="b3b3f-124">Aprire il file di progetto MainActivity.cs e aggiungere l'istruzione seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="b3b3f-125">Aggiungere il codice seguente al metodo **OnCreate** dopo la chiamata a **LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="b3b3f-126">Aggiungere un nuovo metodo helper **CreateAndShowDialog** , come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="b3b3f-127">Aggiungere il codice seguente alla classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="b3b3f-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="b3b3f-128">Verrà esposta l'istanza corrente di **MainActivity**, in modo che sia possibile l'esecuzione nel thread principale dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="b3b3f-129">Inizializzare la variabile `instance` all'inizio del metodo **OnCreate**, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="b3b3f-130">Aggiungere un nuovo file di classe al progetto **Droid** denominato `GcmService.cs`, quindi assicurarsi che le istruzioni **using** seguenti siano presenti nella parte iniziale del file:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="b3b3f-131">Aggiungere le richieste di autorizzazione seguenti alla parte iniziale del file, dopo le istruzioni **using** e prima della dichiarazione **namespace**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="b3b3f-132">Aggiungere la definizione di classe seguente allo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="b3b3f-133">Sostituire **<PROJECT_NUMBER>** con il numero di progetto annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="b3b3f-134">Sostituire la classe **GcmService** vuota con il codice seguente, che usa il nuovo ricevitore di trasmissione:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="b3b3f-135">Aggiungere il codice seguente alla classe **GcmService**</span><span class="sxs-lookup"><span data-stu-id="b3b3f-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="b3b3f-136">in modo da sostituire il gestore eventi **OnRegistered** e implementare un metodo **Register**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="b3b3f-137">Si noti che questo codice usa il parametro `messageParam` nella registrazione del modello.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="b3b3f-138">Aggiungere il codice seguente che implementa **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="b3b3f-139">Questa operazione consente di gestire le notifiche in ingresso e di inviarle alla gestione notifiche per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="b3b3f-140">**GcmServiceBase** richiede anche l'implementazione dei metodi gestore **OnUnRegistered** e **OnError**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="b3b3f-141">È ora possibile testare le notifiche push nell'app in esecuzione su un dispositivo Android o nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="b3b3f-142">Testare le notifiche push nell'app Android</span><span class="sxs-lookup"><span data-stu-id="b3b3f-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="b3b3f-143">I primi due passaggi sono necessari solo per i test eseguiti in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="b3b3f-144">Assicurarsi di distribuire o eseguire il debug su un dispositivo virtuale che ha le API Google impostate come destinazione, come illustrato di seguito nel gestore del dispositivo virtuale Android.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="b3b3f-145">Aggiungere un account Google al dispositivo Android facendo clic su **App** > **Impostazioni** > **Aggiunti account**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="b3b3f-146">Seguire quindi le istruzioni per aggiungere un account Google esistente al dispositivo o per crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="b3b3f-147">In Visual Studio o Xamarin Studio fare clic con il pulsante destro del mouse sul progetto **Droid** e scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="b3b3f-148">Fare clic su **Esegui** per creare il progetto e avviare l'app sul dispositivo Android o sull'emulatore.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="b3b3f-149">Nell'app digitare un'attività e fare clic sull'icona con il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="b3b3f-150">Assicurarsi di ricevere una notifica quando viene aggiunto un elemento.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="b3b3f-151">Configurare ed eseguire il progetto iOS (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b3b3f-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="b3b3f-152">Questa sezione illustra l'esecuzione del progetto Xamarin iOS per dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="b3b3f-153">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="b3b3f-154">Configurare l'hub di notifica per APNS</span><span class="sxs-lookup"><span data-stu-id="b3b3f-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="b3b3f-155">In seguito verrà configurata l'impostazione di progetto iOS in Xamarin Studio o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="b3b3f-156">Aggiungere notifiche push all'app iOS</span><span class="sxs-lookup"><span data-stu-id="b3b3f-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="b3b3f-157">Nel progetto **iOS** aprire il file AppDelegate.cs e aggiungere l'istruzione seguente all'inizio del file di codice.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="b3b3f-158">Nella classe **AppDelegate** aggiungere un override per l'evento **RegisteredForRemoteNotifications** per eseguire la registrazione per le notifiche:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="b3b3f-159">In **AppDelegate** aggiungere anche l'override seguente per il gestore eventi **DidReceiveRemoteNotification**:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="b3b3f-160">Questo metodo gestisce le notifiche in ingresso mentre l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="b3b3f-161">Nella classe **AppDelegate** aggiungere il codice seguente al metodo **FinishedLaunching**:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="b3b3f-162">L'aggiunta di questo codice consente il supporto per le notifiche remote e richiede la registrazione push.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="b3b3f-163">L'app è ora aggiornata per il supporto delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="b3b3f-164">Testare le notifiche push nell'app iOS</span><span class="sxs-lookup"><span data-stu-id="b3b3f-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="b3b3f-165">Fare clic con il pulsante destro del mouse sul progetto iOS e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="b3b3f-166">Scegliere **Esegui** o premere **F5** per compilare il progetto e avviare l'app in un dispositivo iOS</span><span class="sxs-lookup"><span data-stu-id="b3b3f-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="b3b3f-167">e quindi fare clic su **OK** per accettare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b3b3f-168">È necessario accettare le notifiche push in modo esplicito dall'app.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="b3b3f-169">Questa richiesta viene visualizzata solo la prima volta che si esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="b3b3f-170">Nell'app digitare un'attività e fare clic sull'icona con il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="b3b3f-171">Verificare che venga ricevuta una notifica e quindi fare clic su **OK** per ignorarla.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="b3b3f-172">Configurare ed eseguire progetti Windows (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b3b3f-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="b3b3f-173">Questa sezione illustra l'esecuzione dei progetti Xamarin.Forms WinApp e WinPhone81 per dispositivi Windows.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="b3b3f-174">Questa procedura supporta anche progetti per la piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="b3b3f-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="b3b3f-175">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="b3b3f-176">Registrare l'app Windows per le notifiche push con il servizio di notifica Windows (WNS)</span><span class="sxs-lookup"><span data-stu-id="b3b3f-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="b3b3f-177">Configurare l'hub di notifica per WNS</span><span class="sxs-lookup"><span data-stu-id="b3b3f-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="b3b3f-178">Aggiungere notifiche push all'app di Windows</span><span class="sxs-lookup"><span data-stu-id="b3b3f-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="b3b3f-179">In Visual Studio aprire il file **App.xaml.cs** in un progetto Windows e aggiungere le istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="b3b3f-180">Sostituire `<your_TodoItemManager_portable_class_namespace>` con lo spazio dei nomi del progetto portabile che contiene la classe `TodoItemManager`.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="b3b3f-181">Nel file App.xaml.cs aggiungere il metodo **InitNotificationsAsync** seguente:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="b3b3f-182">Questo metodo ottiene il canale per la notifica push e registra un modello per la ricezione di notifiche di modello dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="b3b3f-183">A questo client verrà recapitata una notifica di modello che supporta *messageParam* .</span><span class="sxs-lookup"><span data-stu-id="b3b3f-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="b3b3f-184">Nel file App.xaml.cs aggiornare la definizione del metodo **OnLaunched** del gestore eventi aggiungendo il modificatore `async`</span><span class="sxs-lookup"><span data-stu-id="b3b3f-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="b3b3f-185">e quindi aggiungere la riga di codice seguente alla fine del metodo:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="b3b3f-186">In questo modo è possibile garantire che la registrazione della notifica push venga creata o aggiornata a ogni avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="b3b3f-187">È importante eseguire questa operazione per assicurare che il canale di notifica push WNS sia sempre attivo.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="b3b3f-188">In Esplora soluzioni di Visual Studio aprire il file **Package.appxmanifest** e in **Notifiche** impostare **Avvisi popup supportati** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="b3b3f-189">Compilare l'app e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="b3b3f-190">A questo punto l'app client dovrebbe eseguire la registrazione per le notifiche di modello dal back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="b3b3f-191">Ripetere questa sezione per ogni progetto Windows nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="b3b3f-192">Testare le notifiche push nell'app di Windows</span><span class="sxs-lookup"><span data-stu-id="b3b3f-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="b3b3f-193">In Visual Studio fare clic con il pulsante destro del mouse su un progetto Windows e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="b3b3f-194">Premere il pulsante **Esegui** per compilare il progetto e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="b3b3f-195">Nell'app digitare un nome per un nuovo elemento todoitem, quindi fare clic sull'icona del segno più (**+**) per aggiungerlo.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="b3b3f-196">Assicurarsi di ricevere una notifica quando viene aggiunto l'elemento.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3b3f-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3b3f-197">Next steps</span></span>
<span data-ttu-id="b3b3f-198">Altre informazioni sulle notifiche push:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="b3b3f-199">Diagnose push notification issues</span><span class="sxs-lookup"><span data-stu-id="b3b3f-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="b3b3f-200">(Diagnosticare i problemi relativi alle notifiche push) Esistono varie ragioni per cui le notifiche possono essere eliminate o non giungere ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="b3b3f-201">Questo argomento illustra come analizzare e capire la causa radice degli errori relativi alle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="b3b3f-202">È possibile anche proseguire con una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3b3f-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="b3b3f-203">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="b3b3f-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="b3b3f-204">(Aggiungere l'autenticazione all'app) Informazioni sull'autenticazione degli utenti dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="b3b3f-205">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="b3b3f-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="b3b3f-206">Informazioni su come aggiungere il supporto offline all'app usando il back-end di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="b3b3f-207">Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="b3b3f-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
