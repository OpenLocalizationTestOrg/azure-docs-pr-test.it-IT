---
title: aaaGet iniziali con gli hub di notifica di Azure per App Kindle | Documenti Microsoft
description: In questa esercitazione viene illustrato applicazione Kindle tooa di notifiche push toouse toosend di hub di notifica di Azure.
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
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="0c734-103">Introduzione ad Hub di notifica per le app per Kindle</span><span class="sxs-lookup"><span data-stu-id="0c734-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0c734-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0c734-104">Overview</span></span>
<span data-ttu-id="0c734-105">Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push applicazione Kindle tooa di notifiche.</span><span class="sxs-lookup"><span data-stu-id="0c734-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="0c734-106">Verrà creata un'app Kindle vuota che riceve notifiche push tramite Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="0c734-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c734-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c734-107">Prerequisites</span></span>
<span data-ttu-id="0c734-108">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0c734-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0c734-109">Ottenere hello Android SDK (si presuppone che si utilizzerà Eclipse) da hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sito Android</a>.</span><span class="sxs-lookup"><span data-stu-id="0c734-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="0c734-110">Seguire i passaggi di hello in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">impostazione delle variabili di sviluppo ambiente</a> tooset l'ambiente di sviluppo per Kindle.</span><span class="sxs-lookup"><span data-stu-id="0c734-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="0c734-111">Aggiungere un nuovo portale per sviluppatori di app toohello</span><span class="sxs-lookup"><span data-stu-id="0c734-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="0c734-112">Innanzitutto, creare un'app in hello [portale per gli sviluppatori Amazon].</span><span class="sxs-lookup"><span data-stu-id="0c734-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="0c734-113">Hello copia **chiave applicazione**.</span><span class="sxs-lookup"><span data-stu-id="0c734-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="0c734-114">Nel portale di hello, fare clic sul nome dell'applicazione hello e quindi fare clic su hello **Device Messaging** scheda.</span><span class="sxs-lookup"><span data-stu-id="0c734-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="0c734-115">Fare clic su **Create a New Security Profile**, quindi creare un nuovo profilo di sicurezza, ad esempio il **profilo di sicurezza TestAdm**.</span><span class="sxs-lookup"><span data-stu-id="0c734-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="0c734-116">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0c734-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="0c734-117">Fare clic su **profili sicurezza** profilo di sicurezza hello tooview appena creato.</span><span class="sxs-lookup"><span data-stu-id="0c734-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="0c734-118">Hello copia **ID Client** e **segreto Client** valori per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="0c734-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="0c734-119">Creazione di una chiave API</span><span class="sxs-lookup"><span data-stu-id="0c734-119">Create an API key</span></span>
1. <span data-ttu-id="0c734-120">Aprire un prompt dei comandi con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="0c734-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="0c734-121">Esplorazione delle cartelle di Android SDK toohello.</span><span class="sxs-lookup"><span data-stu-id="0c734-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="0c734-122">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0c734-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="0c734-123">Per hello **keystore** password, digitare **android**.</span><span class="sxs-lookup"><span data-stu-id="0c734-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="0c734-124">Hello copia **MD5** impronta digitale.</span><span class="sxs-lookup"><span data-stu-id="0c734-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="0c734-125">Nel portale per sviluppatori di hello in hello **messaggistica** scheda, fare clic su **Android/Kindle** e immettere il nome di hello del pacchetto di hello per l'applicazione (ad esempio, **com.sample.notificationhubtest**) hello e **MD5** valore e quindi fare clic su **generare la chiave API**.</span><span class="sxs-lookup"><span data-stu-id="0c734-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="0c734-126">Aggiungere le credenziali toohello hub</span><span class="sxs-lookup"><span data-stu-id="0c734-126">Add credentials toohello hub</span></span>
<span data-ttu-id="0c734-127">Nel portale hello aggiungere toohello ID client e il segreto hello client **configura** scheda di hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0c734-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="0c734-128">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="0c734-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="0c734-129">Quando si crea un'applicazione, usare come requisito minimo il livello API 17.</span><span class="sxs-lookup"><span data-stu-id="0c734-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="0c734-130">Aggiungere il progetto Eclipse tooyour di hello ADM librerie:</span><span class="sxs-lookup"><span data-stu-id="0c734-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="0c734-131">libreria ADM hello tooobtain [scaricare hello SDK].</span><span class="sxs-lookup"><span data-stu-id="0c734-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="0c734-132">Estrarre il file zip SDK hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="0c734-133">In Eclipse fare clic con il pulsante destro del mouse sul progetto e scegliere **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0c734-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="0c734-134">Selezionare **Java Build Path** hello a sinistra e quindi seleziona hello * * librerie * * scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="0c734-135">Fare clic su **aggiungere Jar esterna**e file hello selezionare `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` dalla directory hello in cui è stato estratto hello Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="0c734-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="0c734-136">Scaricare hello degli hub di notifica Android SDK (collegamento).</span><span class="sxs-lookup"><span data-stu-id="0c734-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="0c734-137">Decomprimere il pacchetto di hello e quindi trascinare file hello `notification-hubs-sdk.jar` in hello `libs` cartella in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0c734-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="0c734-138">Modificare il toosupport manifesto app ADM:</span><span class="sxs-lookup"><span data-stu-id="0c734-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="0c734-139">Aggiungere lo spazio dei nomi di Amazon hello nell'elemento di manifesto radice hello:</span><span class="sxs-lookup"><span data-stu-id="0c734-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="0c734-140">Aggiungere le autorizzazioni al primo elemento hello nell'elemento manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="0c734-141">Substitute **[nome pacchetto]** con pacchetto hello utilizzato toocreate l'app.</span><span class="sxs-lookup"><span data-stu-id="0c734-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="0c734-142">Inserire hello successivo elemento come figlio di primo hello dell'elemento applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="0c734-143">Ricordare toosubstitute **[nome servizio]** con nome hello del gestore di messaggi in formato ADM creati nella sezione successiva hello (pacchetto hello inclusi), e sostituire **[nome pacchetto]** con hello nome del pacchetto con cui è stato creato l'app.</span><span class="sxs-lookup"><span data-stu-id="0c734-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="0c734-144">Creazione del gestore di messaggi ADM</span><span class="sxs-lookup"><span data-stu-id="0c734-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="0c734-145">Creare una nuova classe che eredita da `com.amazon.device.messaging.ADMMessageHandlerBase` e denominarlo `MyADMMessageHandler`, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="0c734-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="0c734-146">Aggiungere il seguente hello `import` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="0c734-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="0c734-147">Aggiungere hello seguente codice nella classe hello creato.</span><span class="sxs-lookup"><span data-stu-id="0c734-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="0c734-148">Ricorda toosubstitute hello hub nome stringa di connessione e (ascolto):</span><span class="sxs-lookup"><span data-stu-id="0c734-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="0c734-149">Aggiungere i seguenti toohello codice hello `OnMessage()` metodo:</span><span class="sxs-lookup"><span data-stu-id="0c734-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="0c734-150">Aggiungere i seguenti toohello codice hello `OnRegistered` metodo:</span><span class="sxs-lookup"><span data-stu-id="0c734-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="0c734-151">Aggiungere i seguenti toohello codice hello `OnUnregistered` metodo:</span><span class="sxs-lookup"><span data-stu-id="0c734-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="0c734-152">In hello `MainActivity` metodo, aggiungere hello successiva istruzione di importazione:</span><span class="sxs-lookup"><span data-stu-id="0c734-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="0c734-153">Aggiungere hello seguente codice alla fine hello hello `OnCreate` metodo:</span><span class="sxs-lookup"><span data-stu-id="0c734-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="0c734-154">Aggiungere app tooyour chiave API</span><span class="sxs-lookup"><span data-stu-id="0c734-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="0c734-155">In Eclipse, creare un nuovo file denominato **api_key.txt** nell'asset di hello directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="0c734-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="0c734-156">Aprire hello file e copia hello chiave API che è stato generato nel portale per sviluppatori Amazon hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="0c734-157">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="0c734-157">Run hello app</span></span>
1. <span data-ttu-id="0c734-158">Avviare l'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-158">Start hello emulator.</span></span>
2. <span data-ttu-id="0c734-159">Nell'emulatore hello, scorrere verso il dalla parte superiore di hello e fare clic su **impostazioni**, quindi fare clic su **il mio account** e registrare con un account di Amazon valido.</span><span class="sxs-lookup"><span data-stu-id="0c734-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="0c734-160">In Eclipse, eseguire l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c734-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="0c734-161">Se si verifica un problema, controllare il momento di hello dell'emulatore hello (o dispositivo).</span><span class="sxs-lookup"><span data-stu-id="0c734-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="0c734-162">il valore di ora Hello deve essere accurato.</span><span class="sxs-lookup"><span data-stu-id="0c734-162">hello time value must be accurate.</span></span> <span data-ttu-id="0c734-163">tempo di hello toochange dell'emulatore Kindle hello, è possibile eseguire hello il seguente comando dalla directory di strumenti della piattaforma Android SDK:</span><span class="sxs-lookup"><span data-stu-id="0c734-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="0c734-164">Inviare un messaggio</span><span class="sxs-lookup"><span data-stu-id="0c734-164">Send a message</span></span>
<span data-ttu-id="0c734-165">toosend un messaggio tramite .NET:</span><span class="sxs-lookup"><span data-stu-id="0c734-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portale per gli sviluppatori Amazon]: https://developer.amazon.com/home.html
[scaricare hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
