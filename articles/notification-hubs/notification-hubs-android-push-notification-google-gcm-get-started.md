---
title: Invio di notifiche push ad Android con Hub di notifica di Azure | Documentazione di Microsoft
description: "In questa esercitazione, si apprenderà come usare Hub di notifica di Azure per inviare notifiche push a dispositivi Android."
services: notification-hubs
documentationcenter: android
keywords: notifiche push, notifica push, notifiche push per android
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="1b61a-104">Invio di notifiche push ad Android con Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="1b61a-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1b61a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="1b61a-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b61a-106">Questo argomento illustra le notifiche push con Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="1b61a-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="1b61a-107">Se si sta ancora usando Google Firebase Messaging (FCM), vedere [Invio di notifiche push ad Android con Hub di notifica di Azure e Firebase Cloud Messaging](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b61a-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="1b61a-108">Questa esercitazione illustra come usare Hub di notifica di Azure per inviare notifiche push a un'applicazione per Android.</span><span class="sxs-lookup"><span data-stu-id="1b61a-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="1b61a-109">In questa esercitazione verrà creata un'app Android vuota che riceve notifiche push usando il servizio Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="1b61a-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="1b61a-110">Il codice completo per questa esercitazione può essere scaricato da GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="1b61a-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b61a-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1b61a-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b61a-112">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="1b61a-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1b61a-113">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1b61a-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1b61a-114">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="1b61a-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="1b61a-115">Oltre a un account Azure attivo come indicato sopra, questa esercitazione richiede solo la versione più recente di [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="1b61a-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="1b61a-116">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app Android.</span><span class="sxs-lookup"><span data-stu-id="1b61a-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="1b61a-117">Creazione di un progetto che supporta Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="1b61a-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="1b61a-118">Configurare un nuovo hub di notifica</span><span class="sxs-lookup"><span data-stu-id="1b61a-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="1b61a-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="1b61a-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="1b61a-120">Nel pannello **Impostazioni** selezionare **Servizi di notifica**, quindi **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="1b61a-121">Immettere la chiave API e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="1b61a-123">A questo punto, l'hub di notifica è configurato per l'uso con GCM e sono disponibili le stringhe di connessione per registrare l'app per l'invio e la ricezione di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="1b61a-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="1b61a-124"><a id="connecting-app"></a>Connettere l'app all'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="1b61a-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="1b61a-125">Creare un nuovo progetto Android</span><span class="sxs-lookup"><span data-stu-id="1b61a-125">Create a new Android project</span></span>
1. <span data-ttu-id="1b61a-126">In Android Studio avviare un nuovo progetto Android Studio.</span><span class="sxs-lookup"><span data-stu-id="1b61a-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio: nuovo progetto][13]
2. <span data-ttu-id="1b61a-128">Scegliere il fattore di forma **Phone and Tablet** (Telefono e tablet) e la versione **Minimum SDK** (SDK minimo) che si vuole supportare.</span><span class="sxs-lookup"><span data-stu-id="1b61a-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="1b61a-129">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-129">Then click **Next**.</span></span>
   
   ![Android Studio: flusso di lavoro di creazione del progetto][14]
3. <span data-ttu-id="1b61a-131">Scegliere **Empty Activity** (Attività vuota) per l'attività principale, fare clic su **Avanti**, quindi su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="1b61a-132">Aggiungere Google Play Services al progetto</span><span class="sxs-lookup"><span data-stu-id="1b61a-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="1b61a-133">Aggiunta di librerie dell'Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="1b61a-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="1b61a-134">Nel file `Build.Gradle` relativo all'**app** aggiungere le righe seguenti alla sezione delle **dipendenze**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="1b61a-135">Aggiungere l'archivio seguente dopo la sezione **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="1b61a-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="1b61a-136">Aggiornamento del file AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1b61a-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="1b61a-137">Per supportare GCM è necessario implementare un servizio listener Instance ID nel codice, che consente di [ottenere token di registrazione](https://developers.google.com/cloud-messaging/android/client#sample-register) usando l'[API Instance ID di Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="1b61a-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="1b61a-138">In questa esercitazione verrà assegnato il nome `MyInstanceIDService`alla classe.</span><span class="sxs-lookup"><span data-stu-id="1b61a-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="1b61a-139">Aggiungere la definizione del servizio seguente al file AndroidManifest.xml, all'interno del tag `<application>` .</span><span class="sxs-lookup"><span data-stu-id="1b61a-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="1b61a-140">Sostituire il segnaposto `<your package>` con il nome effettivo del pacchetto visualizzato all'inizio del file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="1b61a-141">Dopo la ricezione del token di registrazione di GCM dall'API Instance ID, lo si userà per la [registrazione con Hub di notifica di Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="1b61a-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="1b61a-142">La registrazione verrà supportata in background mediante un `IntentService` denominato `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="1b61a-143">Il servizio sarà anche responsabile dell' [aggiornamento del token di registrazione di GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="1b61a-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="1b61a-144">Aggiungere la definizione del servizio seguente al file AndroidManifest.xml, all'interno del tag `<application>` .</span><span class="sxs-lookup"><span data-stu-id="1b61a-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="1b61a-145">Sostituire il segnaposto `<your package>` con il nome effettivo del pacchetto visualizzato all'inizio del file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="1b61a-146">Verrà definito anche un ricevitore per la ricezione di notifiche.</span><span class="sxs-lookup"><span data-stu-id="1b61a-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="1b61a-147">Aggiungere la definizione del ricevitore seguente al file AndroidManifest.xml, nel tag `<application>` .</span><span class="sxs-lookup"><span data-stu-id="1b61a-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="1b61a-148">Sostituire il segnaposto `<your package>` con il nome effettivo del pacchetto visualizzato all'inizio del file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="1b61a-149">Aggiungere le necessarie autorizzazioni correlate a GCM riportate di seguito sotto il tag `</application>`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="1b61a-150">Sostituire `<your package>` con il nome del pacchetto visualizzato all'inizio del file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="1b61a-151">Per altre informazioni su queste autorizzazioni, vedere [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest)(Configurare un'app client di GCM per Android).</span><span class="sxs-lookup"><span data-stu-id="1b61a-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="1b61a-152">Aggiunta di codice</span><span class="sxs-lookup"><span data-stu-id="1b61a-152">Adding code</span></span>
1. <span data-ttu-id="1b61a-153">Nella visualizzazione del progetto espandere **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="1b61a-154">Fare clic con il pulsante destro del mouse sulla cartella del pacchetto in **java**, scegliere **Nuovo**, quindi selezionare **Java Class** (Classe Java).</span><span class="sxs-lookup"><span data-stu-id="1b61a-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="1b61a-155">Aggiungere una nuova classe denominata `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio: nuova classe Java][6]
   
    <span data-ttu-id="1b61a-157">Aggiornare questi tre segnaposto nel codice seguente per la classe `NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="1b61a-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="1b61a-158">**SenderId**: numero di progetto ottenuto in precedenza in [Google Cloud Console](http://cloud.google.com/console)(Console Cloud di Google).</span><span class="sxs-lookup"><span data-stu-id="1b61a-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="1b61a-159">**HubListenConnectionString**: stringa di connessione **DefaultListenAccessSignature** per l'hub.</span><span class="sxs-lookup"><span data-stu-id="1b61a-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="1b61a-160">È possibile copiare la stringa di connessione facendo clic su **Criteri di accesso** nel pannello **Impostazioni** dell'hub nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="1b61a-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="1b61a-161">**HubName**: usare il nome dell'Hub di notifica visualizzato nel pannello dell'hub nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="1b61a-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="1b61a-162">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="1b61a-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="1b61a-163">classe pubblica NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="1b61a-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="1b61a-164">}</span><span class="sxs-lookup"><span data-stu-id="1b61a-164">}</span></span>
2. <span data-ttu-id="1b61a-165">Usando la procedura precedente, aggiungere un'altra nuova classe denominata `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="1b61a-166">Questa sarà l'implementazione del servizio listener Instance ID.</span><span class="sxs-lookup"><span data-stu-id="1b61a-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="1b61a-167">Il codice per questa classe chiamerà `IntentService` per [aggiornare il token di GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in background.</span><span class="sxs-lookup"><span data-stu-id="1b61a-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="1b61a-168">Aggiungere al progetto un'altra nuova classe denominata `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="1b61a-169">Questa sarà l'implementazione di `IntentService` che gestirà l'[aggiornamento del token di GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e la [registrazione nell'hub di notifica](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="1b61a-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="1b61a-170">Usare il codice seguente per la classe.</span><span class="sxs-lookup"><span data-stu-id="1b61a-170">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
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
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="1b61a-171">Nella classe `MainActivity` aggiungere le istruzioni `import` seguenti sopra la dichiarazione della classe.</span><span class="sxs-lookup"><span data-stu-id="1b61a-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="1b61a-172">Aggiungere i seguenti membri privati nella parte superiore della classe.</span><span class="sxs-lookup"><span data-stu-id="1b61a-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="1b61a-173">Verranno usati per [verificare la disponibilità di Google Play Services come consigliato da Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="1b61a-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="1b61a-174">Nella classe `MainActivity` aggiungere il metodo seguente alla disponibilità di Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="1b61a-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. <span data-ttu-id="1b61a-175">Nella classe `MainActivity` aggiungere il codice seguente che cercherà Google Play Services prima di chiamare `IntentService` per ottenere il token di registrazione di GCM e registrarlo nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="1b61a-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="1b61a-176">Nel metodo `OnCreate` della classe `MainActivity` aggiungere il codice seguente per avviare il processo di registrazione quando viene creata l'attività.</span><span class="sxs-lookup"><span data-stu-id="1b61a-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="1b61a-177">Aggiungere questi altri metodi a `MainActivity` per verificare lo stato dell'app e segnalare lo stato nell'app.</span><span class="sxs-lookup"><span data-stu-id="1b61a-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="1b61a-178">Il metodo `ToastNotify` usa il controllo *"Hello World"* `TextView` per segnalare lo stato e le notifiche in modo permanente nell'app.</span><span class="sxs-lookup"><span data-stu-id="1b61a-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="1b61a-179">Nel layout di activity_main.xml aggiungere l'ID seguente per il controllo.</span><span class="sxs-lookup"><span data-stu-id="1b61a-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="1b61a-180">Verrà quindi aggiunta una sottoclasse per il ricevitore definita nel file AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="1b61a-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="1b61a-181">Aggiungere al progetto un'altra nuova classe denominata `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="1b61a-182">Aggiungere le istruzioni import seguenti all'inizio di `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="1b61a-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="1b61a-183">Aggiungere il codice seguente per la classe `MyHandler` impostandola come sottoclasse di `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="1b61a-184">Questo codice ignora il metodo `OnReceive` , in modo che il gestore segnali le notifiche ricevute.</span><span class="sxs-lookup"><span data-stu-id="1b61a-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="1b61a-185">Il gestore invia anche la notifica push al gestore delle notifiche di Android usando il metodo `sendNotification()` .</span><span class="sxs-lookup"><span data-stu-id="1b61a-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="1b61a-186">Il metodo `sendNotification()` deve essere eseguito quando l'app non è in esecuzione e si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="1b61a-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="1b61a-187">Sulla barra dei menu in Android Studio fare clic su **Compila** > **Ricompila il progetto** per assicurarsi che non ci siano errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="1b61a-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="1b61a-188">Invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="1b61a-188">Sending push notifications</span></span>
<span data-ttu-id="1b61a-189">È possibile testare la ricezione delle notifiche push nell'app inviandole tramite il [portale di Azure]; cercare la sezione **Risoluzione dei problemi** nel pannello dell'hub, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b61a-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Hub di notifica di Azure: test dell'invio](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="1b61a-191">(Facoltativo) Inviare notifiche push direttamente dall'app</span><span class="sxs-lookup"><span data-stu-id="1b61a-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="1b61a-192">In genere, le notifiche vengono inviate tramite un server back-end.</span><span class="sxs-lookup"><span data-stu-id="1b61a-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="1b61a-193">In alcuni casi può essere necessario inviare notifiche push direttamente dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="1b61a-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="1b61a-194">Questa sezione illustra come inviare notifiche dal client usando l' [API REST dell'Hub di notifica di Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b61a-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="1b61a-195">Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="1b61a-196">Aprire il file di layout `activity_main.xml` e fare clic sulla scheda **Text** (Testo) per aggiornare il contenuto di testo del file.</span><span class="sxs-lookup"><span data-stu-id="1b61a-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="1b61a-197">Aggiornarlo con il codice seguente che aggiunge i nuovi controlli `Button` e `EditText` per l'invio di messaggi di notifica push all'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="1b61a-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="1b61a-198">Aggiungere questo codice alla fine, subito prima di `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="1b61a-199">Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="1b61a-200">Aprire il file `strings.xml` e aggiungere i valori di stringa a cui fanno riferimento i nuovi controlli `Button` e `EditText`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="1b61a-201">Aggiungerli alla fine del file, subito prima di `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="1b61a-202">Nel file `NotificationSetting.java` aggiungere l'impostazione seguente alla classe `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="1b61a-203">Aggiornare `HubFullAccess` con la stringa di connessione **DefaultFullSharedAccessSignature** per l'hub.</span><span class="sxs-lookup"><span data-stu-id="1b61a-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="1b61a-204">Questa stringa di connessione può essere copiata dal [portale di Azure] facendo clic su **Criteri di accesso** nel pannello **Impostazioni** dell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="1b61a-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="1b61a-205">Nel file `MainActivity.java` aggiungere le istruzioni `import` seguenti sopra la classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="1b61a-206">Nel file `MainActivity.java` aggiungere i membri seguenti all'inizio della classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="1b61a-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="1b61a-207">È necessario creare un token SaS (Software Access Signature) per autenticare una richiesta POST per l'invio di messaggi all'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="1b61a-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="1b61a-208">Per eseguire questa operazione, analizzare i dati della chiave dalla stringa di connessione e quindi creare il token di firma di accesso condiviso come indicato in [Concetti comuni](http://msdn.microsoft.com/library/azure/dn495627.aspx) nelle informazioni di riferimento sull'API REST.</span><span class="sxs-lookup"><span data-stu-id="1b61a-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="1b61a-209">Il codice seguente è un esempio di implementazione.</span><span class="sxs-lookup"><span data-stu-id="1b61a-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="1b61a-210">In `MainActivity.java` aggiungere il metodo seguente alla classe `MainActivity` per analizzare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="1b61a-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="1b61a-211">In `MainActivity.java` aggiungere il metodo seguente alla classe `MainActivity` per creare un token di autenticazione di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1b61a-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="1b61a-212">In `MainActivity.java` aggiungere il metodo seguente alla classe `MainActivity` per gestire il clic del pulsante **Invia notifica** e inviare il messaggio di notifica push all'hub usando l'API REST predefinita.</span><span class="sxs-lookup"><span data-stu-id="1b61a-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="1b61a-213">Testare l'app</span><span class="sxs-lookup"><span data-stu-id="1b61a-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="1b61a-214">Notifiche push nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="1b61a-214">Push notifications in the emulator</span></span>
<span data-ttu-id="1b61a-215">Per testare le notifiche push all'interno dell'emulatore, assicurarsi che l'immagine dell'emulatore supporti il livello Google API scelto per l'app.</span><span class="sxs-lookup"><span data-stu-id="1b61a-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="1b61a-216">Se l'immagine non supporta le API di Google in modalità nativa verrà generata l'eccezione **SERVICE\_NOT\_AVAILABLE**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="1b61a-217">Verificare anche di avere aggiunto l'account Google all'emulatore in esecuzione in **Impostazioni** > **Account**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="1b61a-218">In caso contrario, i tentativi di registrazione con GCM potrebbero generare l'eccezione **AUTHENTICATION\_FAILED**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="1b61a-219">Esecuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b61a-219">Running the application</span></span>
1. <span data-ttu-id="1b61a-220">Eseguire l'app e notare l'ID registrazione segnalato per una registrazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="1b61a-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Test in Android: registrazione di canali][18]
2. <span data-ttu-id="1b61a-222">Immettere un messaggio di notifica da inviare a tutti i dispositivi Android registrati con l'hub.</span><span class="sxs-lookup"><span data-stu-id="1b61a-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Test in Android: invio di un messaggio][19]

3. <span data-ttu-id="1b61a-224">Premere **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="1b61a-224">Press **Send Notification**.</span></span> <span data-ttu-id="1b61a-225">Su tutti i dispositivi che eseguono l'app verrà visualizzata un'istanza di `AlertDialog` con il messaggio di notifica push.</span><span class="sxs-lookup"><span data-stu-id="1b61a-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="1b61a-226">I dispositivi che non eseguono l'app, ma che sono stati registrati in precedenza per le notifiche push, riceveranno una notifica in Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="1b61a-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="1b61a-227">Per visualizzarle, scorrere verso il basso dall'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="1b61a-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Test in Android: notifiche][21]

## <a name="next-steps"></a><span data-ttu-id="1b61a-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b61a-229">Next steps</span></span>
<span data-ttu-id="1b61a-230">Come passaggio successivo, è consigliabile vedere l'esercitazione [Uso di Hub di notifica di Azure per inviare notifiche agli utenti] .</span><span class="sxs-lookup"><span data-stu-id="1b61a-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="1b61a-231">Verrà illustrato come inviare notifiche da un back-end ASP.NET destinate a utenti specifici.</span><span class="sxs-lookup"><span data-stu-id="1b61a-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="1b61a-232">Per segmentare gli utenti in base ai gruppi di interesse, vedere l'esercitazione [Usare Hub di notifica per inviare le ultime notizie] .</span><span class="sxs-lookup"><span data-stu-id="1b61a-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="1b61a-233">Per altre informazioni generali sull'uso di Hub di notifica, vedere [Hub di notifica di Azure].</span><span class="sxs-lookup"><span data-stu-id="1b61a-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="1b61a-234">[Hub di notifica di Azure]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="1b61a-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="1b61a-235">[Uso di Hub di notifica di Azure per inviare notifiche agli utenti]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="1b61a-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="1b61a-236">[Usare Hub di notifica per inviare le ultime notizie]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="1b61a-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="1b61a-237">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="1b61a-237">[Azure Portal]: https://portal.azure.com</span></span>
