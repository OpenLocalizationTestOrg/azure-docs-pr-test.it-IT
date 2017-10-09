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
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>TooAndroid l'invio di notifiche push con hub di notifica di Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> Questo argomento illustra le notifiche push con Google Firebase Cloud Messaging (FCM). Se si sta ancora utilizzando Google Cloud Messaging (GCM), vedere [tooAndroid le notifiche push di invio con gli hub di notifica di Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure e Cloud Firebase Messaging toosend push applicazione Android tooan di notifiche.
In questa esercitazione verrà creata un'app per Android vuota che riceve notifiche push tramite Firebase Cloud Messaging (FCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

codice Hello completata per questa esercitazione può essere scaricato da GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

## <a name="prerequisites"></a>Prerequisiti
> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

* Inoltre account Azure active tooan indicati sopra, in questa esercitazione richiede la versione più recente di hello di [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).
* Android 2.3 o versione successiva per Firebase Cloud Messaging.
* Google Repository revision 27 o versione successiva è richiesta per Firebase Cloud Messaging.
* Google Play Services 9.0.2 o versione successiva per Firebase Cloud Messaging.
* Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Android.

## <a name="create-a-new-android-studio-project"></a>Creare un nuovo progetto di Android Studio
1. In Android Studio avviare un nuovo progetto Android Studio.
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Scegliere hello **Tablet e telefoni** form factor e hello **minimo SDK** che si desidera toosupport. Quindi fare clic su **Next**.
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Scegliere **attività vuota** per l'attività principale hello, fare clic su **Avanti**, quindi fare clic su **fine**.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Creare un progetto che supporta Google Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configurare un nuovo hub di notifica
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. In hello **impostazioni** blade di hub di notifica, selezionare **Notification Services** e quindi **Google (GCM)**. Immetterne hello FCM server precedentemente copiati da hello [console Firebase](https://firebase.google.com/console/) e fare clic su **salvare**.

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

Hub di notifica è ora configurato toowork con Firebase Cloud Messagin, e si dispone di tooboth stringhe di connessione hello registrare tooreceive l'app e inviare notifiche push.

## <a id="connecting-app"></a>Connettere l'hub di notifica toohello app
### <a name="add-google-play-services-toohello-project"></a>Aggiungi progetto toohello di Google Play services
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Aggiunta di librerie dell'Hub di notifica di Azure
1. In hello `Build.Gradle` file per hello **app**, aggiungere hello seguenti righe hello **dipendenze** sezione.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Aggiungere hello seguenti repository dopo hello **dipendenze** sezione.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Aggiornamento hello androidmanifest. Xml.
1. toosupport FCM, è necessario implementare un servizio di listener di ID istanza nel codice viene utilizzato troppo[ottenere i token di registrazione](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) utilizzando [Google FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). In questa esercitazione verrà assegnato un nome classe hello `MyInstanceIDService`. 
   
    Aggiungere hello seguente toohello AndroidManifest.xml file di definizione servizio all'interno di hello `<application>` tag. 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. Una volta che è stato ricevuto il token di registrazione FCM da hello FirebaseInstanceId API, verrà usato troppo[registrare con l'Hub di notifica di Azure hello](notification-hubs-push-notification-registration-management.md). Saranno supportati la registrazione in background hello utilizzando un `IntentService` denominato `RegistrationIntentService`. Il servizio sarà anche responsabile dell'aggiornamento del token di registrazione di FCM.
   
    Aggiungere hello seguente toohello AndroidManifest.xml file di definizione servizio all'interno di hello `<application>` tag. 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. Verrà inoltre definito un notifiche tooreceive ricevitore. Aggiungere hello seguente ricevitore toohello AndroidManifest.xml file di definizione, all'interno di hello `<application>` tag. Sostituire hello `<your package>` hello di segnaposto con il nome del pacchetto effettivo visualizzato nella parte superiore di hello di hello `AndroidManifest.xml` file.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Aggiungere hello seguente FCM necessarie relative autorizzazioni seguito hello `</application>` tag. Verificare che tooreplace `<your package>` con il nome di pacchetto hello visualizzato nella parte superiore di hello di hello `AndroidManifest.xml` file.
   
    Per ulteriori informazioni su queste autorizzazioni, vedere [configurazione di un'app Client GCM per Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [eseguire la migrazione di un'App Client GCM per Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a>Aggiunta di codice
1. Nella visualizzazione progetto hello, espandere **app** > **src** > **principale** > **java**. Fare clic con il pulsante destro del mouse sulla cartella del pacchetto in **java**, scegliere **Nuovo**, quindi selezionare **Java Class** (Classe Java). Aggiungere una nuova classe denominata `NotificationSettings`. 
   
    ![Android Studio: nuova classe Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    Assicurarsi che questi tre segnaposto nel seguente codice per hello hello di hello tooupdate `NotificationSettings` classe:
   
   * **ID mittente**: hello Id mittente è ottenuto in precedenza hello **Cloud Messaging** scheda delle impostazioni di progetto in hello [console Firebase](https://firebase.google.com/console/).
   * **HubListenConnectionString**: hello **DefaultListenAccessSignature** stringa di connessione per l'hub. È possibile copiare la stringa di connessione, fare clic su **criteri di accesso** su hello **impostazioni** blade di hub di su hello [portale Azure].
   * **HubName**: utilizza il nome dell'hub di notifica che viene visualizzato nel Pannello di hub hello in hello hello [portale Azure].
     
     `NotificationSettings` :
     
       classe pubblica NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
2. Seguendo i passaggi di hello sopra riportati, aggiungere un'altra nuova classe denominata `MyInstanceIDService`. Questa sarà l'implementazione del servizio listener Instance ID.
   
    codice Hello per questa classe chiamerà il nostro `IntentService` troppo[token di aggiornamento hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in background hello.
   
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


1. Aggiungere un altro nuovo progetto tooyour di classe denominato, `RegistrationIntentService`. Questo sarà l'implementazione di hello per il nostro `IntentService` che gestirà [aggiornati i token FCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registrazione con hub di notifica hello](notification-hubs-push-notification-registration-management.md).
   
    Utilizzare hello seguente codice per questa classe.
   
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
2. Nel `MainActivity` classe, aggiungere il seguente hello `import` istruzioni sopra hello dichiarazione di classe.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Aggiungere i seguenti membri privati della classe hello lato superiore hello hello. Si utilizzerà questi [verificare la disponibilità di hello di Google Play Services come consigliato da Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. Nel `MainActivity` classe, aggiungere hello successivi la disponibilità di toohello metodo di Google Play Services. 
   
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
5. Nel `MainActivity` classe, aggiungere hello seguente di codice che verrà archiviata per Google Play Services prima di chiamare il `IntentService` tooget il token di registrazione FCM e la registrazione con l'hub di notifica.
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. In hello `OnCreate` metodo hello `MainActivity` classe, aggiungere hello successivo processo di registrazione hello toostart codice quando viene creato l'attività.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Aggiungere questi altri metodi toohello `MainActivity` tooverify app lo stato e segnalare lo stato dell'app.
   
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
8. Hello `ToastNotify` metodo utilizza hello *"Hello World"* `TextView` controllare lo stato di tooreport e notifiche in modo permanente in app hello. Nel layout activity_main.xml, aggiungere hello seguente id per tale controllo.
   
       android:id="@+id/text_hello"
9. Successivamente sarà necessario aggiungere una sottoclasse per il ricevitore che è stato definito in hello androidmanifest. Xml. Aggiungere un altro nuovo progetto tooyour di classe denominato `MyHandler`.
10. Aggiungere hello seguendo le istruzioni import in cima hello `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Aggiungere hello seguente codice per hello `MyHandler` rendendola una sottoclasse della classe `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Questo codice esegue l'override di hello `OnReceive` metodo, pertanto il gestore di hello indicheranno le notifiche ricevute. gestore Hello invia anche di gestione delle notifiche Android hello push notifica toohello utilizzando hello `sendNotification()` metodo. Hello `sendNotification()` (metodo) deve essere eseguito quando l'applicazione hello non è in esecuzione e viene ricevuta una notifica.
    
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
12. In Android Studio hello barra dei menu, fare clic su **compilare** > **ricompilare progetto** toomake assicurarsi che non sono presenti errori nel codice.
13. Eseguire l'applicazione hello sul dispositivo e verificare che con hub di notifica hello registra correttamente. 
    
    > [!NOTE]
    > Registrazione potrebbe non riuscire all'avvio iniziale hello finché hello `onTokenRefresh()` viene chiamato metodo del servizio di Id di istanza. aggiornamento di Hello deve avviare una registrazione ha esito positivo con hub di notifica hello.
    > 
    > 

## <a name="sending-push-notifications"></a>Invio di notifiche push
È possibile verificare la ricezione di notifiche push nell'app inviando tramite hello [portale Azure] -cercare hello **Troubleshooting** sezione nel Pannello di hub hello, come illustrato di seguito.

![Hub di notifica di Azure: test dell'invio](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Facoltativo) Inviare notifiche push direttamente dall'app hello
> [!IMPORTANT]
> Questo esempio l'invio di notifiche da app client hello viene fornito solo a scopo illustrativo. Poiché questo richiederà hello `DefaultFullSharedAccessSignature` toobe presente sull'app client hello, che espone il rischio di toohello hub di notifica che un utente può ottenere le notifiche di accesso non autorizzato toosend tooyour client.
> 
> 

In genere, le notifiche vengono inviate tramite un server back-end. In alcuni casi, potrebbe essere toobe in grado di toosend le notifiche push direttamente da un'applicazione hello client. Questa sezione viene illustrato come le notifiche di toosend da client hello utilizzando hello [API REST di Hub di notifica di Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **layout**. Aprire hello `activity_main.xml` layout di file e fare clic su hello **testo** scheda contenuto di testo hello tooupdate del file hello. Aggiornarlo con codice hello seguente, che aggiunge nuove `Button` e `EditText` controlli per l'invio di push hub di notifica toohello i messaggi di notifica. Aggiungere questo codice nella parte inferiore di hello, subito prima `</RelativeLayout>`.
   
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
2. Nella visualizzazione del progetto in Android Studio espandere **App** > **src** > **main** > **res** > **values**. Aprire hello `strings.xml` file e aggiungere i valori stringa hello che fanno riferimento hello nuovo `Button` e `EditText` controlli. Aggiungi queste nella parte inferiore di hello del file hello, appena prima `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. Nel `NotificationSetting.java` file, aggiungere hello seguente impostazione toohello `NotificationSettings` classe.
   
    Aggiornamento `HubFullAccess` con hello **DefaultFullSharedAccessSignature** stringa di connessione per l'hub. La stringa di connessione può essere copiata da hello [portale Azure] facendo **criteri di accesso** su hello **impostazioni** pannello per l'hub di notifica.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. Nel `MainActivity.java` file, aggiungere il seguente hello `import` istruzioni sopra hello `MainActivity` classe.
   
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
5. Nel `MainActivity.java` file, aggiungere i seguenti membri nella parte superiore di hello di hello hello `MainActivity` classe.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Creare un hub di notifica POST richiesta toosend messaggi tooyour un tooauthenticate token di firma di accesso di Software (SaS). Questa operazione viene eseguita mediante l'analisi di dati della chiave hello dalla stringa di connessione hello e quindi creare hello token SaS, come indicato in hello [concetti comuni](http://msdn.microsoft.com/library/azure/dn495627.aspx) riferimento all'API REST. Hello seguente di codice è un'implementazione di esempio.
   
    In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` classe tooparse la stringa di connessione.
   
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
7. In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` toocreate classe un token di autenticazione della firma di accesso condiviso.
   
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
8. In `MainActivity.java`, aggiungere hello seguente metodo toohello `MainActivity` hello toohandle classe **invia una notifica** fare clic su pulsante e inviare la notifica push hello hub toohello messaggio utilizzando hello incorporato API REST.
   
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

## <a name="testing-your-app"></a>Testare l'app
#### <a name="push-notifications-in-hello-emulator"></a>Le notifiche push nell'emulatore hello
Se si desidera tootest le notifiche push all'interno di un emulatore, assicurarsi che l'immagine dell'emulatore supporta livello API Google hello scelto per l'app. Se l'immagine non supporta native Google APIs, si finirà con hello **servizio\_non\_disponibile** eccezione.

Inoltre toohello precedente, assicurarsi di aver aggiunto il tooyour account Google emulatore in esecuzione **impostazioni** > **account**. In caso contrario, i tentativi tooregister con GCM può comportare hello **autenticazione\_FAILED** eccezione.

#### <a name="running-hello-application"></a>Esecuzione di un'applicazione hello
1. Eseguire app hello e notare che l'ID registrazione hello viene segnalato per la registrazione ha esito positivo.
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Immettere un toobe messaggio di notifica inviati tooall i dispositivi Android registrati con hub hello.
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Premere **Send Notification**. Verranno visualizzati tutti i dispositivi che sono in esecuzione app hello un `AlertDialog` istanza con un messaggio di notifica push di hello. I dispositivi che non sono in esecuzione app hello ma sono stati registrati in precedenza per le notifiche push riceverà una notifica in hello Android Notification Manager. Quelli visualizzabili scorrendo verso il basso nell'angolo superiore sinistro hello.
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Passaggi successivi
Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione come passaggio successivo hello. Verrà descritto come toosend notifiche da un back-end ASP.NET usando tag tootarget specifici utenti.

Se si desidera che gli utenti dai gruppi di interesse toosegment, estrarre hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione.

toolearn informazioni generali sull'hub di notifica, vedere il nostro [materiale sussidiario per gli hub di notifica].

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
