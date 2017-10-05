---
title: Introduzione ad Hub di notifica di Azure per le app per Kindle | Documentazione Microsoft
description: In questa esercitazione, sono presenti informazioni su come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione per Kindle.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="9ea2d-103">Introduzione ad Hub di notifica per le app per Kindle</span><span class="sxs-lookup"><span data-stu-id="9ea2d-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9ea2d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9ea2d-104">Overview</span></span>
<span data-ttu-id="9ea2d-105">In questa esercitazione viene illustrato come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione Kindle.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="9ea2d-106">Verrà creata un'app Kindle vuota che riceve notifiche push tramite Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="9ea2d-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ea2d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9ea2d-107">Prerequisites</span></span>
<span data-ttu-id="9ea2d-108">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="9ea2d-109">Ottenere Android SDK (si presuppone che verrà utilizzato Eclipse) dal <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sito Android</a>.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="9ea2d-110">Seguire i passaggi in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Configurazione dell’ambiente di sviluppo</a> per impostare l'ambiente di sviluppo per Kindle.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="9ea2d-111">Aggiunta di una nuova app al portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="9ea2d-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="9ea2d-112">Innanzitutto, creare un'app nel [portale per gli sviluppatori di Amazon].</span><span class="sxs-lookup"><span data-stu-id="9ea2d-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="9ea2d-113">Copiare la **chiave applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="9ea2d-114">Nel portale, fare clic sul nome dell'app, quindi fare clic sulla scheda **Device Messaging** .</span><span class="sxs-lookup"><span data-stu-id="9ea2d-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="9ea2d-115">Fare clic su **Create a New Security Profile**, quindi creare un nuovo profilo di sicurezza, ad esempio il **profilo di sicurezza TestAdm**.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="9ea2d-116">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="9ea2d-117">Fare clic su **Security Profiles** per visualizzare il profilo di sicurezza creato.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="9ea2d-118">Copiare i valori **Client ID** e **Client Secret** per usarli in seguito.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="9ea2d-119">Creazione di una chiave API</span><span class="sxs-lookup"><span data-stu-id="9ea2d-119">Create an API key</span></span>
1. <span data-ttu-id="9ea2d-120">Aprire un prompt dei comandi con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="9ea2d-121">Passare alla cartella Android SDK.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="9ea2d-122">Immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="9ea2d-123">Per la password **keystore**, digitare **android**.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="9ea2d-124">Copiare l'ID digitale **MD5** .</span><span class="sxs-lookup"><span data-stu-id="9ea2d-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="9ea2d-125">Nel portale per sviluppatori, fare clic su **Android/Kindle** nella scheda **Messaging**, immettere il nome del pacchetto per l'app, ad esempio, **com.sample.notificationhubtest**, e il valore **MD5**, quindi fare clic su **Generate API Key** (Genera chiave API).</span><span class="sxs-lookup"><span data-stu-id="9ea2d-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="9ea2d-126">Aggiunta di credenziali all'hub</span><span class="sxs-lookup"><span data-stu-id="9ea2d-126">Add credentials to the hub</span></span>
<span data-ttu-id="9ea2d-127">Nel portale, aggiungere il segreto client e l'ID client alla scheda **Configure** dell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="9ea2d-128">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9ea2d-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="9ea2d-129">Quando si crea un'applicazione, usare come requisito minimo il livello API 17.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="9ea2d-130">Aggiungere le librerie ADM al progetto Eclipse:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="9ea2d-131">Per ottenere la libreria ADM, [scaricare l'SDK].</span><span class="sxs-lookup"><span data-stu-id="9ea2d-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="9ea2d-132">Estrarre il file zip SDK.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="9ea2d-133">In Eclipse fare clic con il pulsante destro del mouse sul progetto e scegliere **Properties**.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="9ea2d-134">Selezionare **Java Build Path** a sinistra, quindi selezionare il * * librerie * * nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="9ea2d-135">Fare clic su **Add External Jar** (Aggiungi JAR esterni), quindi selezionare il file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` dalla directory in cui è stato estratto Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="9ea2d-136">Scaricare NotificationHubs Android SDK (collegamento).</span><span class="sxs-lookup"><span data-stu-id="9ea2d-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="9ea2d-137">Decomprimere il pacchetto, quindi trascinare il file `notification-hubs-sdk.jar` nella cartella `libs` in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="9ea2d-138">Modificare il manifesto dell'app per supportare ADM:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="9ea2d-139">Aggiungere lo spazio dei nomi Amazon nell'elemento manifesto radice:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="9ea2d-140">Aggiungere le autorizzazioni come primo elemento sotto l'elemento manifesto.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="9ea2d-141">Sostituire **[YOUR PACKAGE NAME]** con il pacchetto usato per creare l'app.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="9ea2d-142">Inserire l'elemento seguente come primo figlio dell'elemento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="9ea2d-143">Ricordare di sostituire **[YOUR SERVICE NAME]** con il nome del gestore di messaggi ADM che verrà creato nella sezione successiva (incluso il pacchetto) e sostituire **[YOUR PACKAGE NAME]** con il nome del pacchetto utilizzato per creare l'app.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="9ea2d-144">Creazione del gestore di messaggi ADM</span><span class="sxs-lookup"><span data-stu-id="9ea2d-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="9ea2d-145">Creare una nuova classe che eredita da `com.amazon.device.messaging.ADMMessageHandlerBase` e denominarla `MyADMMessageHandler`, come mostrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="9ea2d-146">Aggiungere le istruzioni `import` seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="9ea2d-147">Aggiungere il codice seguente alla classe creata.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="9ea2d-148">Ricordare di sostituire il nome dell'hub e la stringa di connessione (ascolto):</span><span class="sxs-lookup"><span data-stu-id="9ea2d-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="9ea2d-149">Aggiungere il codice seguente al metodo `OnMessage()` :</span><span class="sxs-lookup"><span data-stu-id="9ea2d-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="9ea2d-150">Aggiungere il codice seguente al metodo `OnRegistered` :</span><span class="sxs-lookup"><span data-stu-id="9ea2d-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="9ea2d-151">Aggiungere il codice seguente al metodo `OnUnregistered` :</span><span class="sxs-lookup"><span data-stu-id="9ea2d-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="9ea2d-152">Quindi, nel metodo `MainActivity` , aggiungere l'istruzione import seguente:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="9ea2d-153">Alla fine del metodo `OnCreate` aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="9ea2d-154">Aggiunta della chiave API all'app</span><span class="sxs-lookup"><span data-stu-id="9ea2d-154">Add your API key to your app</span></span>
1. <span data-ttu-id="9ea2d-155">In Eclipse creare un nuovo file denominato **api_key.txt** negli asset della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="9ea2d-156">Aprire il file e copiare la chiave API generata nel portale per sviluppatori Amazon.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="9ea2d-157">Esecuzione dell'app</span><span class="sxs-lookup"><span data-stu-id="9ea2d-157">Run the app</span></span>
1. <span data-ttu-id="9ea2d-158">Avviare l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-158">Start the emulator.</span></span>
2. <span data-ttu-id="9ea2d-159">Nell'emulatore, scorrere dall'alto e fare clic su **Settings** (Impostazioni), quindi fare clic su **My account** ed effettuare la registrazione usando un account Amazon valido.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="9ea2d-160">In Eclipse eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="9ea2d-161">Se si verifica un problema, controllare l'ora dell'emulatore (o del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="9ea2d-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="9ea2d-162">Il valore dell'ora deve essere accurato.</span><span class="sxs-lookup"><span data-stu-id="9ea2d-162">The time value must be accurate.</span></span> <span data-ttu-id="9ea2d-163">Per modificare l'ora dell'emulatore Kindle è possibile eseguire il comando seguente dalla directory di strumenti della piattaforma Android SDK:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="9ea2d-164">Invio di un messaggio</span><span class="sxs-lookup"><span data-stu-id="9ea2d-164">Send a message</span></span>
<span data-ttu-id="9ea2d-165">Per inviare un messaggio usando .NET:</span><span class="sxs-lookup"><span data-stu-id="9ea2d-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="9ea2d-166">[portale per gli sviluppatori di Amazon]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="9ea2d-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="9ea2d-167">[scaricare l'SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="9ea2d-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
