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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Introduzione ad Hub di notifica per le app per Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push applicazione Kindle tooa di notifiche.
Verrà creata un'app Kindle vuota che riceve notifiche push tramite Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* Ottenere hello Android SDK (si presuppone che si utilizzerà Eclipse) da hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sito Android</a>.
* Seguire i passaggi di hello in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">impostazione delle variabili di sviluppo ambiente</a> tooset l'ambiente di sviluppo per Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Aggiungere un nuovo portale per sviluppatori di app toohello
1. Innanzitutto, creare un'app in hello [portale per gli sviluppatori Amazon].
   
    ![][0]
2. Hello copia **chiave applicazione**.
   
    ![][1]
3. Nel portale di hello, fare clic sul nome dell'applicazione hello e quindi fare clic su hello **Device Messaging** scheda.
   
    ![][2]
4. Fare clic su **Create a New Security Profile**, quindi creare un nuovo profilo di sicurezza, ad esempio il **profilo di sicurezza TestAdm**. Fare quindi clic su **Salva**.
   
    ![][3]
5. Fare clic su **profili sicurezza** profilo di sicurezza hello tooview appena creato. Hello copia **ID Client** e **segreto Client** valori per un uso successivo.
   
    ![][4]

## <a name="create-an-api-key"></a>Creazione di una chiave API
1. Aprire un prompt dei comandi con privilegi di amministratore.
2. Esplorazione delle cartelle di Android SDK toohello.
3. Immettere hello comando seguente:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Per hello **keystore** password, digitare **android**.
5. Hello copia **MD5** impronta digitale.
6. Nel portale per sviluppatori di hello in hello **messaggistica** scheda, fare clic su **Android/Kindle** e immettere il nome di hello del pacchetto di hello per l'applicazione (ad esempio, **com.sample.notificationhubtest**) hello e **MD5** valore e quindi fare clic su **generare la chiave API**.

## <a name="add-credentials-toohello-hub"></a>Aggiungere le credenziali toohello hub
Nel portale hello aggiungere toohello ID client e il segreto hello client **configura** scheda di hub di notifica.

## <a name="set-up-your-application"></a>Configurazione dell'applicazione
> [!NOTE]
> Quando si crea un'applicazione, usare come requisito minimo il livello API 17.
> 
> 

Aggiungere il progetto Eclipse tooyour di hello ADM librerie:

1. libreria ADM hello tooobtain [scaricare hello SDK]. Estrarre il file zip SDK hello.
2. In Eclipse fare clic con il pulsante destro del mouse sul progetto e scegliere **Properties**. Selezionare **Java Build Path** hello a sinistra e quindi seleziona hello * * librerie * * scheda nella parte superiore di hello. Fare clic su **aggiungere Jar esterna**e file hello selezionare `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` dalla directory hello in cui è stato estratto hello Amazon SDK.
3. Scaricare hello degli hub di notifica Android SDK (collegamento).
4. Decomprimere il pacchetto di hello e quindi trascinare file hello `notification-hubs-sdk.jar` in hello `libs` cartella in Eclipse.

Modificare il toosupport manifesto app ADM:

1. Aggiungere lo spazio dei nomi di Amazon hello nell'elemento di manifesto radice hello:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Aggiungere le autorizzazioni al primo elemento hello nell'elemento manifesto hello. Substitute **[nome pacchetto]** con pacchetto hello utilizzato toocreate l'app.
   
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
2. Inserire hello successivo elemento come figlio di primo hello dell'elemento applicazione hello. Ricordare toosubstitute **[nome servizio]** con nome hello del gestore di messaggi in formato ADM creati nella sezione successiva hello (pacchetto hello inclusi), e sostituire **[nome pacchetto]** con hello nome del pacchetto con cui è stato creato l'app.
   
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

## <a name="create-your-adm-message-handler"></a>Creazione del gestore di messaggi ADM
1. Creare una nuova classe che eredita da `com.amazon.device.messaging.ADMMessageHandlerBase` e denominarlo `MyADMMessageHandler`, come illustrato nella seguente illustrazione hello:
   
    ![][6]
2. Aggiungere il seguente hello `import` istruzioni:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Aggiungere hello seguente codice nella classe hello creato. Ricorda toosubstitute hello hub nome stringa di connessione e (ascolto):
   
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
4. Aggiungere i seguenti toohello codice hello `OnMessage()` metodo:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Aggiungere i seguenti toohello codice hello `OnRegistered` metodo:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Aggiungere i seguenti toohello codice hello `OnUnregistered` metodo:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. In hello `MainActivity` metodo, aggiungere hello successiva istruzione di importazione:
   
        import com.amazon.device.messaging.ADM;
8. Aggiungere hello seguente codice alla fine hello hello `OnCreate` metodo:
   
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

## <a name="add-your-api-key-tooyour-app"></a>Aggiungere app tooyour chiave API
1. In Eclipse, creare un nuovo file denominato **api_key.txt** nell'asset di hello directory del progetto.
2. Aprire hello file e copia hello chiave API che è stato generato nel portale per sviluppatori Amazon hello.

## <a name="run-hello-app"></a>Eseguire app hello
1. Avviare l'emulatore hello.
2. Nell'emulatore hello, scorrere verso il dalla parte superiore di hello e fare clic su **impostazioni**, quindi fare clic su **il mio account** e registrare con un account di Amazon valido.
3. In Eclipse, eseguire l'applicazione hello.

> [!NOTE]
> Se si verifica un problema, controllare il momento di hello dell'emulatore hello (o dispositivo). il valore di ora Hello deve essere accurato. tempo di hello toochange dell'emulatore Kindle hello, è possibile eseguire hello il seguente comando dalla directory di strumenti della piattaforma Android SDK:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Inviare un messaggio
toosend un messaggio tramite .NET:

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
