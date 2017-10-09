---
title: aaaGet avviato con gli hub di notifica di Azure utilizzando Baidu | Documenti Microsoft
description: "In questa esercitazione, è illustrato come toouse gli hub di notifica di Azure toopush notifiche tooAndroid i dispositivi con Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Introduzione ad Hub di notifica tramite Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Push cloud Baidu è un servizio cloud cinese, che è possibile utilizzare i dispositivi toomobile di notifiche push toosend. Questo servizio è utile in Cina, in cui il recapito delle notifiche push tooAndroid è complesso a causa di presenza di hello di diverse app Store e di push dei servizi, inoltre toohello disponibilità dei dispositivi Android che non sono in genere connessi tooGCM (Google Il cloud di messaggistica).

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede:

* Android SDK (si presuppone che si usa Eclipse), che è possibile scaricare da hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sito Android</a>
* [Mobile Services Android SDK]
* [Baidu Push Android SDK]

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Creare un account Baidu
toouse Baidu, è necessario disporre di un account Baidu. Se si dispone già di uno, accedi toohello [Baidu portale] e ignorare il passaggio successivo toohello. In caso contrario, vedere hello attenendosi alle istruzioni su come toocreate un account Baidu.  

1. Passare toohello [Baidu portale] e fare clic su hello**登录**(**accesso**) collegamento. Fare clic su**立即注册**processo di registrazione account toostart hello.
   
   ![][1]
2. Immettere i dettagli necessario hello, telefono o posta elettronica indirizzo e la password e verifica del codice, fare clic su **iscrizione**.
   
   ![][2]
3. Si riceverà un indirizzo di posta elettronica toohello di posta elettronica immesso con un collegamento di tooactivate account Baidu.
   
   ![][3]
4. Accedi tooyour account di posta elettronica, posta elettronica di attivazione Baidu hello scegliere hello attivazione collegamento tooactivate account Baidu.
   
   ![][4]

Dopo aver creato un account Baidu attivato, accedi toohello [Baidu portale].

## <a name="register-as-a-baidu-developer"></a>Registrarsi come sviluppatore Baidu
1. Dopo aver eseguito l'accesso in toohello [Baidu portale], fare clic su**更多 >>** (**più**).
   
      ![][5]
2. Scorrere verso il basso hello**站长与开发者服务 (Webmaster e servizi per sviluppatori)** sezione e fare clic su**百度开放云平台**(**Baidu aprire piattaforma cloud**).
   
      ![][6]
3. Nella pagina successiva di hello, fare clic su**开发者服务**(**servizi per sviluppatori**) nell'angolo superiore destro di hello.
   
      ![][7]
4. Nella pagina successiva di hello, fare clic su**注册开发者**(**gli sviluppatori registrati**) dal menu di hello nell'angolo superiore destro di hello.
   
      ![][8]
5. Immettere il nome, una descrizione e un numero di cellulare per ricevere un messaggio di testo di verifica e quindi fare clic su **送验证码** (**Invia codice di verifica**). Per i numeri di telefono internazionale, è necessario codice paese di hello tooenclose tra parentesi. Per un numero degli Stati Uniti, usare ad esempio **(1)1234567890**.
   
      ![][9]
6. Dovrebbe venire visualizzato un messaggio di testo con un numero di verifica, come illustrato nell'esempio seguente hello:
   
      ![][10]
7. Immettere il numero di verifica hello dal messaggio hello in**验证码**(**codice di conferma**).
8. Infine, completare la registrazione per sviluppatori di hello accettazione hello Baidu contratto e facendo clic su**提交**(**Invia**). Verrà visualizzato hello dopo il corretto completamento della registrazione:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Creare un progetto di Baidu cloud push
Quando si crea un progetto di Baidu cloud push, si ricevono l'ID dell'app, la chiave API e la chiave privata.

1. Dopo aver eseguito l'accesso in toohello [Baidu portale], fare clic su**更多 >>** (**più**).
   
      ![][5]
2. Scorrere verso il basso hello**站长与开发者服务**(**Webmaster e servizi per sviluppatori**) sezione e fare clic su**百度开放云平台**(**Baidu aprire piattaforma cloud**).
   
      ![][6]
3. Nella pagina successiva di hello, fare clic su**开发者服务**(**servizi per sviluppatori**) nell'angolo superiore destro di hello.
   
      ![][7]
4. Nella pagina successiva di hello, fare clic su**云推送**(**Push Cloud**) da hello**云服务**(**servizi Cloud**) sezione.
   
      ![][12]
5. Una volta registrati gli sviluppatori, vedere**管理控制台**(**Console di gestione**) nel menu superiore hello. Fare clic su **开发者服务管理** (**Gestione dei servizi per sviluppatori**).
   
      ![][13]
6. Nella pagina successiva di hello, fare clic su**创建工程**(**Crea progetto**).
   
      ![][14]
7. Immettere un nome di applicazione e fare clic su **创建** (**Crea**).
   
      ![][15]
8. Al termine della creazione di un progetto push cloud Baidu viene visualizzata una pagina con l'**AppID**, la **chiave API** e la **chiave privata**. Prendere nota della chiave API hello e una chiave privata, che verrà utilizzato in un secondo momento.
   
      ![][16]
9. Configurare il progetto hello per le notifiche push facendo**云推送**(**Push Cloud**) nel riquadro di sinistra hello.
   
      ![][31]
10. Nella pagina successiva di hello, fare clic su hello**推送设置**(**Push impostazioni**) pulsante.
    
    ![][32]  
11. Nella pagina di configurazione hello, aggiungere il nome del pacchetto hello che verrà utilizzato nel progetto Android in hello**应用包名**(**pacchetto di applicazione**), campo e quindi fare clic su**保存设置**( **Salvare**).  
    
    ![][33]

Vedrai hello**保存成功!** (**Salvataggio completato**).

## <a name="configure-your-notification-hub"></a>Configurare l'hub di notifica
1. Accedi toohello [portale di Azure classico], quindi fare clic su **+ nuovo** in basso hello hello.
2. Fare clic su **Servizi app**, **Bus di servizio**, **Hub di notifica** e infine su **Creazione rapida**.
3. Specificare un nome per il **Hub di notifica**selezionare hello **area** hello e **Namespace** questo hub di notifica in cui verrà creato e quindi fare clic su  **Creare un nuovo Hub di notifica**.  
   
      ![][17]
4. Fare clic su spazio dei nomi hello in cui è stato creato l'hub di notifica e quindi fare clic su **gli hub di notifica** nella parte superiore di hello.
   
      ![][18]
5. Hub di notifica selezionare hello è creato e quindi fare clic su **configura** menu principale di hello.
   
      ![][19]
6. Scorrere verso il basso toohello **le impostazioni di notifica baidu** sezione e immettere la chiave API hello e una chiave privata che è stato ottenuto da console Baidu hello in precedenza per il progetto di push cloud Baidu. Fare clic su **Salva**.
   
      ![][20]
7. Fare clic su hello **Dashboard** scheda nella parte superiore di hello hub di notifica hello e quindi fare clic su **Visualizza stringa di connessione**.
   
      ![][21]
8. Prendere nota di hello **DefaultListenSharedAccessSignature** e **DefaultFullSharedAccessSignature** da hello **accedere alle informazioni di connessione** finestra.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Connettere l'hub di notifica toohello app
1. Nel plug-in Eclipse ADT creare un nuovo progetto Android selezionando **File** > **New (Nuovo)**  > **Android Application Project (Progetto applicazione Android)** .
   
    ![][23]
2. Immettere un **nome applicazione** e assicurarsi che hello **minimo richiesto SDK** versione è stata impostata troppo**API 16: Android 4.1**.
   
    ![][24]
3. Fare clic su **Avanti** e continuare seguendo la procedura guidata hello finché hello **creare attività** verrà visualizzata la finestra. Assicurarsi che **attività vuota** sia selezionata, infine selezionare **fine** toocreate una nuova applicazione Android.
   
    ![][25]
4. Verificare che tale hello **destinazione di compilazione progetto** sia impostata correttamente.
   
    ![][26]
5. Scaricare il file di notifica-hub-0.4.jar hello da hello **file** scheda di hello [notifica-hub-Android-SDK in Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Aggiungere toohello file hello **librerie** cartella del progetto Eclipse e aggiornamento hello *librerie* cartella.
6. Scaricare e decomprimere hello [Baidu Push Android SDK]aprire hello **librerie** cartella, quindi hello copia **pushservice x.y.z** jar file e hello **armeabi**  &  **mips** cartelle hello **librerie** cartella dell'applicazione Android.
7. Aprire hello **AndroidManifest.xml** file di Android di progetto e aggiungere hello le autorizzazioni richieste da hello SDK Baidu.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Aggiungere hello **android: name** proprietà tooyour **applicazione** elemento **AndroidManifest.xml**, sostituendo *yourprojectname* (per esempio **com.example.BaiduTest**). Verificare che il nome del progetto corrisponda hello uno configurato nella console di hello Baidu.
   
        <application android:name="yourprojectname.DemoApplication"
9. Aggiungere hello seguente configurazione all'interno dell'elemento applicazione hello dopo hello **. MainActivity** elemento activity, sostituendo *yourprojectname* (ad esempio, **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Aggiungere una nuova classe denominata **ConfigurationSettings.java** toohello progetto.
    
     ![][28]
    
     ![][29]
11. Aggiungere hello tooit di codice seguente:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Impostare il valore di hello di **API_KEY** con cosa recuperati dal progetto di cloud Baidu hello in precedenza, **NotificationHubName** con il nome di hub di notifica dal portale di Azure classico hello e  **NotificationHubConnectionString** con DefaultListenSharedAccessSignature da hello portale classico di Azure.
12. Aggiungere una nuova classe denominata **DemoApplication.java**e aggiungere hello tooit di codice seguente:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Aggiungere un'altra nuova classe denominata **MyPushMessageReceiver.java**e aggiungere hello tooit di codice seguente. Classe hello che gestisce hello notifiche push che vengono ricevute dal server di push Baidu hello è.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Aprire **Mainactivity**e aggiungere hello seguente toohello **onCreate** metodo:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Aprire hello seguendo le istruzioni import nella parte superiore di hello:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Inviare notifiche tooyour app
È possibile verificare rapidamente la ricezione di notifiche nell'app mediante l'invio di notifiche in hello [portale di Azure](https://portal.azure.com/) utilizzando hello **inviare** pulsante hub di notifica hello, come illustrato nella seguente schermata hello:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile. Se una libreria non è disponibile per il back-end, è possibile utilizzare l'API REST hello toosend direttamente i messaggi di notifica.

In questa esercitazione è la semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end. Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione. Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:

* **Interfaccia REST**: È possibile supportare la notifica su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).
* **App per dispositivi mobili**: per un esempio di come toosend notifiche da un back-end dell'App Mobile di servizio App di Azure che è integrato con hub di notifica, vedere [app mobile tooyour le notifiche push Aggiungi](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java o PHP**: per un esempio di come le notifiche toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Facoltativo) Inviare notifiche da un'app console .NET
In questa sezione verrà illustrato come inviare notifiche con un'app console .NET.

1. Creare una nuova applicazione console in Visual C#:
   
    ![][30]
2. Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Questa istruzione consente di aggiungere un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. File hello aprire **Program.cs** e aggiungere hello seguente istruzione using:
   
        using Microsoft.Azure.NotificationHubs;
4. Nel `Program` classe, aggiungere al metodo hello e sostituire *DefaultFullSharedAccessSignatureSASConnectionString* e *NotificationHubName* con i valori hello che è necessario.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Aggiungere hello righe in seguito il **Main** metodo:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Test dell'app
connettere questa app con un telefono effettivi solo tootest hello computer tooyour phone tramite un cavo USB. Questa azione Carica l'app nel telefono hello associata.

Fare clic su questa applicazione con l'emulatore di Windows hello, barra degli strumenti hello Eclipse superiore, tootest **eseguire**e quindi selezionare l'app: avvio dell'emulatore hello, caricamenti, e viene eseguito hello app.

app Hello recupera hello 'userId' e 'ID canale' dal servizio di notifica Baidu Push hello e lo registra con hub di notifica hello.

toosend una notifica di prova, è possibile utilizzare una scheda debug hello di hello portale classico di Azure. Se è stata compilata un'applicazione console .NET hello per Visual Studio, premi semplicemente tasto F5 hello in un'applicazione hello toorun Visual Studio. un'applicazione Hello invia una notifica che viene visualizzato nell'area di notifica superiore hello nell'emulatore o dispositivo.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[portale di Azure classico]: https://manage.windowsazure.com/
[Baidu portale]: http://www.baidu.com/
