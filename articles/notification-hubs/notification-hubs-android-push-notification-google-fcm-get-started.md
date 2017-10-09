---
title: tooAndroid di notifiche push aaaSending con gli hub di notifica di Azure e la messaggistica Cloud Firebase | Documenti Microsoft
description: "In questa esercitazione, è illustrato come toouse gli hub di notifica di Azure e Cloud Firebase Messaging toopush notifiche tooAndroid dispositivi."
services: notification-hubs
documentationcenter: android
keywords: notifiche push, notifica push, notifiche push per android, fcm, firebase cloud messaging
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="06f99-104">TooAndroid l'invio di notifiche push con hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="06f99-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="06f99-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="06f99-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06f99-106">Questo argomento illustra le notifiche push con Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="06f99-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="06f99-107">Se si sta ancora utilizzando Google Cloud Messaging (GCM), vedere [tooAndroid le notifiche push di invio con gli hub di notifica di Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="06f99-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="06f99-108">Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure e Cloud Firebase Messaging toosend push applicazione Android tooan di notifiche.</span><span class="sxs-lookup"><span data-stu-id="06f99-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="06f99-109">In questa esercitazione verrà creata un'app per Android vuota che riceve notifiche push tramite Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="06f99-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="06f99-110">codice Hello completata per questa esercitazione può essere scaricato da GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="06f99-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06f99-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="06f99-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06f99-112">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="06f99-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="06f99-113">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="06f99-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="06f99-114">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="06f99-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="06f99-115">Inoltre account Azure active tooan indicati sopra, in questa esercitazione richiede la versione più recente di hello di [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="06f99-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="06f99-116">Android 2.3 o versione successiva per Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="06f99-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="06f99-117">Google Repository revision 27 o versione successiva è richiesta per Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="06f99-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="06f99-118">Google Play Services 9.0.2 o versione successiva per Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="06f99-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="06f99-119">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Android.</span><span class="sxs-lookup"><span data-stu-id="06f99-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="06f99-120">Creare un nuovo progetto di Android Studio</span><span class="sxs-lookup"><span data-stu-id="06f99-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="06f99-121">In Android Studio avviare un nuovo progetto Android Studio.</span><span class="sxs-lookup"><span data-stu-id="06f99-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="06f99-122">Scegliere hello **Tablet e telefoni** form factor e hello **minimo SDK** che si desidera toosupport.</span><span class="sxs-lookup"><span data-stu-id="06f99-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="06f99-123">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="06f99-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="06f99-124">Scegliere **attività vuota** per l'attività principale hello, fare clic su **Avanti**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="06f99-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="06f99-125">Creare un progetto che supporta Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="06f99-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="06f99-126">Configurare un nuovo hub di notifica</span><span class="sxs-lookup"><span data-stu-id="06f99-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="06f99-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="06f99-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="06f99-128">In hello **impostazioni** blade di hub di notifica, selezionare **Notification Services** e quindi **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="06f99-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="06f99-129">Immetterne hello FCM server precedentemente copiati da hello [console Firebase](https://firebase.google.com/console/) e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="06f99-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="06f99-131">Hub di notifica è ora configurato toowork con Firebase Cloud Messagin, e si dispone di tooboth stringhe di connessione hello registrare tooreceive l'app e inviare notifiche push.</span><span class="sxs-lookup"><span data-stu-id="06f99-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="06f99-132"><a id="connecting-app"></a>Connettere l'hub di notifica toohello app</span><span class="sxs-lookup"><span data-stu-id="06f99-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="06f99-133">Aggiungi progetto toohello di Google Play services</span><span class="sxs-lookup"><span data-stu-id="06f99-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="06f99-134">Aggiunta di librerie dell'Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="06f99-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="06f99-135">In hello `Build.Gradle` file per hello **app**, aggiungere hello seguenti righe hello **dipendenze** sezione.</span><span class="sxs-lookup"><span data-stu-id="06f99-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="06f99-136">Aggiungere hello seguenti repository dopo hello **dipendenze** sezione.</span><span class="sxs-lookup"><span data-stu-id="06f99-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="06f99-137">Aggiornamento hello androidmanifest. Xml.</span><span class="sxs-lookup"><span data-stu-id="06f99-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="06f99-138">toosupport FCM, è necessario implementare un servizio di listener di ID istanza nel codice viene utilizzato troppo[ottenere i token di registrazione](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) utilizzando [Google FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="06f99-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="06f99-139">In questa esercitazione verrà assegnato un nome classe hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="06f99-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="06f99-140">Aggiungere hello seguente toohello AndroidManifest.xml file di definizione servizio all'interno di hello `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="06f99-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="06f99-141">Una volta che è stato ricevuto il token di registrazione FCM da hello FirebaseInstanceId API, verrà usato troppo[registrare con l'Hub di notifica di Azure hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="06f99-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="06f99-142">Saranno supportati la registrazione in background hello utilizzando un `IntentService` denominato `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="06f99-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="06f99-143">Il servizio sarà anche responsabile dell'aggiornamento del token di registrazione di FCM.</span><span class="sxs-lookup"><span data-stu-id="06f99-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="06f99-144">Aggiungere hello seguente toohello AndroidManifest.xml file di definizione servizio all'interno di hello `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="06f99-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="06f99-145">Verrà inoltre definito un notifiche tooreceive ricevitore.</span><span class="sxs-lookup"><span data-stu-id="06f99-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="06f99-146">Aggiungere hello seguente ricevitore toohello AndroidManifest.xml file di definizione, all'interno di hello `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="06f99-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="06f99-147">Sostituire hello `<your package>` hello di segnaposto con il nome del pacchetto effettivo visualizzato nella parte superiore di hello di hello `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="06f99-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="06f99-148">Aggiungere hello seguente FCM necessarie relative autorizzazioni seguito hello `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="06f99-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="06f99-149">Verificare che tooreplace `<your package>` con il nome di pacchetto hello visualizzato nella parte superiore di hello di hello `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="06f99-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="06f99-150">Per ulteriori informazioni su queste autorizzazioni, vedere [configurazione di un'app Client GCM per Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [eseguire la migrazione di un'App Client GCM per Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="06f99-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="06f99-151">Aggiunta di codice</span><span class="sxs-lookup"><span data-stu-id="06f99-151">Adding code</span></span>
1. <span data-ttu-id="06f99-152">Nella visualizzazione progetto hello, espandere **app** > **src** > **principale** > **java**.</span><span class="sxs-lookup"><span data-stu-id="06f99-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="06f99-153">Fare clic con il pulsante destro del mouse sulla cartella del pacchetto in **java**, scegliere **Nuovo**, quindi selezionare **Java Class** (Classe Java).</span><span class="sxs-lookup"><span data-stu-id="06f99-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="06f99-154">Aggiungere una nuova classe denominata `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="06f99-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio: nuova classe Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="06f99-156">Assicurarsi che questi tre segnaposto nel seguente codice per hello hello di hello tooupdate `NotificationSettings` classe:</span><span class="sxs-lookup"><span data-stu-id="06f99-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="06f99-157">**ID mittente**: hello Id mittente è ottenuto in precedenza hello **Cloud Messaging** scheda delle impostazioni di progetto in hello [console Firebase](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="06f99-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="06f99-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** stringa di connessione per l'hub.</span><span class="sxs-lookup"><span data-stu-id="06f99-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="06f99-159">È possibile copiare la stringa di connessione, fare clic su **criteri di accesso** su hello **impostazioni** blade di hub di su hello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="06f99-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="06f99-160">**HubName**: utilizza il nome dell'hub di notifica che viene visualizzato nel Pannello di hub hello in hello hello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="06f99-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="06f99-161">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="06f99-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="06f99-162">classe pubblica NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="06f99-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="06f99-163">}</span><span class="sxs-lookup"><span data-stu-id="06f99-163">}</span></span>
2. <span data-ttu-id="06f99-164">Seguendo i passaggi di hello sopra riportati, aggiungere un'altra nuova classe denominata `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="06f99-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="06f99-165">Questa sarà l'implementazione del servizio listener Instance ID.</span><span class="sxs-lookup"><span data-stu-id="06f99-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="06f99-166">codice Hello per questa classe chiamerà il nostro `IntentService` troppo[token di aggiornamento hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in background hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="06f99-167">Aggiungere un altro nuovo progetto tooyour di classe denominato, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="06f99-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="06f99-168">Questo sarà l'implementazione di hello per il nostro `IntentService` che gestirà [aggiornati i token FCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registrazione con hub di notifica hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="06f99-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="06f99-169">Utilizzare hello seguente codice per questa classe.</span><span class="sxs-lookup"><span data-stu-id="06f99-169">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {
   
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="06f99-170">Nel `MainActivity` classe, aggiungere il seguente hello `import` istruzioni sopra hello dichiarazione di classe.</span><span class="sxs-lookup"><span data-stu-id="06f99-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="06f99-171">Aggiungere i seguenti membri privati della classe hello lato superiore hello hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="06f99-172">Si utilizzerà questi [verificare la disponibilità di hello di Google Play Services come consigliato da Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="06f99-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="06f99-173">Nel `MainActivity` classe, aggiungere hello successivi la disponibilità di toohello metodo di Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="06f99-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="06f99-174">Nel `MainActivity` classe, aggiungere hello seguente di codice che verrà archiviata per Google Play Services prima di chiamare il `IntentService` tooget il token di registrazione FCM e la registrazione con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="06f99-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="06f99-175">In hello `OnCreate` metodo hello `MainActivity` classe, aggiungere hello successivo processo di registrazione hello toostart codice quando viene creato l'attività.</span><span class="sxs-lookup"><span data-stu-id="06f99-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="06f99-176">Aggiungere questi altri metodi toohello `MainActivity` tooverify app lo stato e segnalare lo stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="06f99-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="06f99-177">Hello `ToastNotify` metodo utilizza hello *"Hello World"* `TextView` controllare lo stato di tooreport e notifiche in modo permanente in app hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="06f99-178">Nel layout activity_main.xml, aggiungere hello seguente id per tale controllo.</span><span class="sxs-lookup"><span data-stu-id="06f99-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="06f99-179">Successivamente sarà necessario aggiungere una sottoclasse per il ricevitore che è stato definito in hello androidmanifest. Xml.</span><span class="sxs-lookup"><span data-stu-id="06f99-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="06f99-180">Aggiungere un altro nuovo progetto tooyour di classe denominato `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="06f99-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="06f99-181">Aggiungere hello seguendo le istruzioni import in cima hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="06f99-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="06f99-182">Aggiungere hello seguente codice per hello `MyHandler` rendendola una sottoclasse della classe `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="06f99-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="06f99-183">Questo codice esegue l'override di hello `OnReceive` metodo, pertanto il gestore di hello indicheranno le notifiche ricevute.</span><span class="sxs-lookup"><span data-stu-id="06f99-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="06f99-184">gestore Hello invia anche di gestione delle notifiche Android hello push notifica toohello utilizzando hello `sendNotification()` metodo.</span><span class="sxs-lookup"><span data-stu-id="06f99-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="06f99-185">Hello `sendNotification()` (metodo) deve essere eseguito quando l'applicazione hello non è in esecuzione e viene ricevuta una notifica.</span><span class="sxs-lookup"><span data-stu-id="06f99-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="06f99-186">In Android Studio hello barra dei menu, fare clic su **compilare** > **ricompilare progetto** toomake assicurarsi che non sono presenti errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="06f99-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="06f99-187">Eseguire l'applicazione hello sul dispositivo e verificare che con hub di notifica hello registra correttamente.</span><span class="sxs-lookup"><span data-stu-id="06f99-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="06f99-188">Registrazione potrebbe non riuscire all'avvio iniziale hello finché hello `onTokenRefresh()` viene chiamato metodo del servizio di Id di istanza.</span><span class="sxs-lookup"><span data-stu-id="06f99-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="06f99-189">aggiornamento di Hello deve avviare una registrazione ha esito positivo con hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="06f99-190">Invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="06f99-190">Sending push notifications</span></span>
<span data-ttu-id="06f99-191">È possibile verificare la ricezione di notifiche push nell'app inviando tramite hello [portale Azure] -cercare hello **Troubleshooting** sezione nel Pannello di hub hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="06f99-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Hub di notifica di Azure: test dell'invio](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="06f99-193">(Facoltativo) Inviare notifiche push direttamente dall'app hello</span><span class="sxs-lookup"><span data-stu-id="06f99-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06f99-194">Questo esempio l'invio di notifiche da app client hello viene fornito solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="06f99-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="06f99-195">Poiché questo richiederà hello `DefaultFullSharedAccessSignature` toobe presente sull'app client hello, che espone il rischio di toohello hub di notifica che un utente può ottenere le notifiche di accesso non autorizzato toosend tooyour client.</span><span class="sxs-lookup"><span data-stu-id="06f99-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="06f99-196">In genere, le notifiche vengono inviate tramite un server back-end.</span><span class="sxs-lookup"><span data-stu-id="06f99-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="06f99-197">In alcuni casi, potrebbe essere toobe in grado di toosend le notifiche push direttamente da un'applicazione hello client.</span><span class="sxs-lookup"><span data-stu-id="06f99-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="06f99-198">Questa sezione viene illustrato come le notifiche di toosend da client hello utilizzando hello [API REST di Hub di notifica di Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="06f99-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="06f99-199">Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="06f99-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="06f99-200">Aprire hello `activity_main.xml` layout di file e fare clic su hello **testo** scheda contenuto di testo hello tooupdate del file hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="06f99-201">Aggiornarlo con codice hello seguente, che aggiunge nuove `Button` e `EditText` controlli per l'invio di push hub di notifica toohello i messaggi di notifica.</span><span class="sxs-lookup"><span data-stu-id="06f99-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="06f99-202">Aggiungere questo codice nella parte inferiore di hello, subito prima `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="06f99-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="06f99-203">Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="06f99-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="06f99-204">Aprire hello `strings.xml` file e aggiungere i valori stringa hello che fanno riferimento hello nuovo `Button` e `EditText` controlli.</span><span class="sxs-lookup"><span data-stu-id="06f99-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="06f99-205">Aggiungi queste nella parte inferiore di hello del file hello, appena prima `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="06f99-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="06f99-206">Nel `NotificationSetting.java` file, aggiungere hello seguente impostazione toohello `NotificationSettings` classe.</span><span class="sxs-lookup"><span data-stu-id="06f99-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="06f99-207">Aggiornamento `HubFullAccess` con hello **DefaultFullSharedAccessSignature** stringa di connessione per l'hub.</span><span class="sxs-lookup"><span data-stu-id="06f99-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="06f99-208">La stringa di connessione può essere copiata da hello [portale Azure] facendo **criteri di accesso** su hello **impostazioni** pannello per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="06f99-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="06f99-209">Nel `MainActivity.java` file, aggiungere il seguente hello `import` istruzioni sopra hello `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="06f99-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="06f99-210">Nel `MainActivity.java` file, aggiungere i seguenti membri nella parte superiore di hello di hello hello `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="06f99-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="06f99-211">Creare un hub di notifica POST richiesta toosend messaggi tooyour un tooauthenticate token di firma di accesso di Software (SaS).</span><span class="sxs-lookup"><span data-stu-id="06f99-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="06f99-212">Questa operazione viene eseguita mediante l'analisi di dati della chiave hello dalla stringa di connessione hello e quindi creare hello token SaS, come indicato in hello [concetti comuni](http://msdn.microsoft.com/library/azure/dn495627.aspx) riferimento all'API REST.</span><span class="sxs-lookup"><span data-stu-id="06f99-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="06f99-213">Hello seguente di codice è un'implementazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="06f99-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="06f99-214">In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` classe tooparse la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="06f99-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="06f99-215">In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` toocreate classe un token di autenticazione della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="06f99-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="06f99-216">In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` hello toohandle classe **invia una notifica** fare clic su pulsante e inviare la notifica push hello hub toohello messaggio utilizzando hello incorporato API REST.</span><span class="sxs-lookup"><span data-stu-id="06f99-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="06f99-217">Testare l'app</span><span class="sxs-lookup"><span data-stu-id="06f99-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="06f99-218">Le notifiche push nell'emulatore hello</span><span class="sxs-lookup"><span data-stu-id="06f99-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="06f99-219">Se si desidera tootest le notifiche push all'interno di un emulatore, assicurarsi che l'immagine dell'emulatore supporta livello API Google hello scelto per l'app.</span><span class="sxs-lookup"><span data-stu-id="06f99-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="06f99-220">Se l'immagine non supporta native Google APIs, si finirà con hello **servizio\_non\_disponibile** eccezione.</span><span class="sxs-lookup"><span data-stu-id="06f99-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="06f99-221">Inoltre toohello precedente, assicurarsi di aver aggiunto il tooyour account Google emulatore in esecuzione **impostazioni** > **account**.</span><span class="sxs-lookup"><span data-stu-id="06f99-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="06f99-222">In caso contrario, i tentativi tooregister con GCM può comportare hello **autenticazione\_FAILED** eccezione.</span><span class="sxs-lookup"><span data-stu-id="06f99-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="06f99-223">Esecuzione di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="06f99-223">Running hello application</span></span>
1. <span data-ttu-id="06f99-224">Eseguire app hello e notare che l'ID registrazione hello viene segnalato per la registrazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="06f99-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="06f99-225">Immettere un toobe messaggio di notifica inviati tooall i dispositivi Android registrati con hub hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="06f99-226">Premere **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="06f99-226">Press **Send Notification**.</span></span> <span data-ttu-id="06f99-227">Verranno visualizzati tutti i dispositivi che sono in esecuzione app hello un `AlertDialog` istanza con un messaggio di notifica push di hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="06f99-228">I dispositivi che non sono in esecuzione app hello ma sono stati registrati in precedenza per le notifiche push riceverà una notifica in hello Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="06f99-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="06f99-229">Quelli visualizzabili scorrendo verso il basso nell'angolo superiore sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="06f99-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06f99-230">Next steps</span></span>
<span data-ttu-id="06f99-231">Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione come passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="06f99-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="06f99-232">Verrà descritto come toosend notifiche da un back-end ASP.NET usando tag tootarget specifici utenti.</span><span class="sxs-lookup"><span data-stu-id="06f99-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="06f99-233">Se si desidera che gli utenti dai gruppi di interesse toosegment, estrarre hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="06f99-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="06f99-234">toolearn informazioni generali sull'hub di notifica, vedere il nostro [materiale sussidiario per gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="06f99-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[materiale sussidiario per gli hub di notifica]: notification-hubs-push-notification-overview.md
[toousers le notifiche di utilizzare gli hub di notifica toopush]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[portale Azure]: https://portal.azure.com
