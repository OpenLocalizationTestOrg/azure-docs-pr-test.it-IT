---
title: aaaGet avviato con gli hub di notifica per le app xamarin | Documenti Microsoft
description: "In questa esercitazione, è illustrato toouse gli hub di notifica di Azure toosend push notifiche tooa applicazione Android di Xamarin."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Introduzione ad Hub di notifica con Xamarin per Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione illustra applicazione xamarin tooa di notifiche push toouse toosend di hub di notifica di Azure.
Verrà creata un'app per Xamarin.Android vuota che riceve notifiche push tramite il servizio Google Cloud Messaging (GCM). Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app. Hello codice completato è disponibile in hello [app hub di notifica] [ GitHub] esempio.

In questa esercitazione illustra hello semplice scenario di trasmissione con gli hub di notifica.

## <a name="before-you-begin"></a>Prima di iniziare
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* Visual Studio con Xamarin su Windows o Xamarin Studio su Mac OS X. Per istruzioni complete sull'installazione , vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Un account Google attivo
* [Componente di messaggistica di Azure]
* [Componente client di Google Cloud Messaging]

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Xamarin.Android.

> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Abilitare Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Configurare l'hub di notifica
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Fare clic su hello <b>configura</b> scheda nella parte superiore di hello, immettere hello <b>chiave API</b> valore ottenuto nella sezione precedente hello e quindi fare clic su <b>salvare</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Hub di notifica è ora configurato toowork con GCM, e tooboth stringhe di connessione hello necessario registrare l'app tooreceive e alle notifiche toosend push.

## <a name="connect-your-app-toohello-notification-hub"></a>Connettere l'hub di notifica toohello app
### <a name="create-a-new-project"></a>Creare un nuovo progetto
1. In Xamarin Studio fare clic su **New Solution** (Nuova soluzione), **Android App** (App Android) e selezionare **Next** (Avanti).
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Compilare i campi **App Name** (Nome app) e **Identifier** (Identificatore). Fare clic su hello **le piattaforme di destinazione** toosupport desiderato e quindi fare clic su **Avanti** e **crea**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    In questo modo viene creato un nuovo progetto Android.

1. Aprire le proprietà del progetto hello facendo clic di nuovo progetto hello visualizzazione soluzioni e scegliendo **opzioni**. Seleziona hello **applicazione Android** elemento hello **compilare** sezione.
   
    Verificare che la prima lettera di hello del **nome pacchetto** è in minuscolo.
   
   > [!IMPORTANT]
   > Hello prima lettera del nome del pacchetto hello deve essere minuscola. In caso contrario, verranno visualizzati errori del manifesto dell'applicazione al momento della registrazione di **BroadcastReceiver** e **IntentFilter** per le notifiche push più avanti.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Facoltativamente, set hello **minimo Android versione** tooanother livello API.
3. Facoltativamente, set hello **versione di destinazione Android** toohello un'altra versione dell'API che si desidera tootarget (deve essere livello API 8 o versione successiva).

Fare clic su **OK** e finestra di dialogo Project Options hello Chiudi.

### <a name="add-hello-required-components-tooyour-project"></a>Aggiungi progetto tooyour componenti necessari di hello
Hello Google Cloud Messaging Client disponibile in hello archivio componenti Xamarin semplifica il processo di hello di supportare le notifiche push in xamarin.

1. Fare clic sulla cartella componenti hello in app xamarin e scegliere **ottenere più componenti**.
2. Ricerca di hello **messaggistica di Azure** componente e aggiungerlo toohello progetto.
3. Ricerca di hello **Google Cloud Messaging Client** componente e aggiungerlo toohello progetto.

### <a name="set-up-notification-hubs-in-your-project"></a>Configurare Hub di notifica nel progetto
1. Raccogliere le seguenti informazioni per l'hub di notifica e di app Android hello:
   
   * **GoogleProjectNumber**: ottenere questo valore di numero progetto dal dashboard Panoramica hello dell'applicazione hello portale per sviluppatori Google. Durante la creazione di app hello nel portale di hello apportate una nota di questo valore in precedenza.
   * **Stringa di connessione in attesa**: nel dashboard di hello in hello [portale di Azure classico], fare clic su **consente di visualizzare le stringhe di connessione**. Hello copia *DefaultListenSharedAccessSignature* stringa di connessione per questo valore.
   * **Nome dell'hub**: questo è il nome di hello dell'hub da hello [portale di Azure classico]. Ad esempio, *mynotificationhub2*.
     
     Creare un **Constants.cs** classe per il progetto Xamarin e definire i seguenti valori costanti in una classe hello hello. Sostituire i segnaposto hello con i valori.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Aggiungere il seguente hello utilizzando istruzioni troppo**Mainactivity**:
   
        using Android.Util;
        using Gcm.Client;
3. Aggiungere un toohello variabile di istanza `MainActivity` classe che verrà utilizzato tooshow una finestra di dialogo di avviso quando l'applicazione hello è in esecuzione:
   
        public static MainActivity instance;
4. Creare hello al metodo in hello **MainActivity** classe:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. In hello `OnCreate` metodo **Mainactivity**, inizializzare hello `instance` variabile e aggiungere una chiamata troppo`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Creare una nuova classe **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Di seguito è illustrata in dettaglio la creazione da zero di una classe **BroadcastReceiver** . Tuttavia, per la creazione di un rapido toomanually alternativo **MyBroadcastReceiver.cs** è toorefer toohello **GcmService.cs** file è stato trovato nel progetto di xamarin esempio hello incluso hello [Esempi degli hub di notifica][GitHub]. Duplicazione **GcmService.cs** e modifica dei nomi di classe può essere anche un toostart ideale.
   > 
   > 
7. Aggiungere il seguente hello utilizzando istruzioni troppo**MyBroadcastReceiver.cs** (che fa riferimento il componente toohello e assembly aggiunto in precedenza):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. In **MyBroadcastReceiver.cs**, aggiungere hello seguendo le richieste di autorizzazione tra hello **utilizzando** istruzioni e hello **dello spazio dei nomi** dichiarazione:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. In **MyBroadcastReceiver.cs**, modificare hello **MyBroadcastReceiver** classe seguente hello toomatch:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Aggiungere un'altra classe in **MyBroadcastReceiver.cs** denominata **PushHandlerService** che deriva da **GcmServiceBase**. Verificare che hello tooapply **servizio** toohello classe di attributo:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** implementa i metodi **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**. Il nostro **PushHandlerService** classe di implementazione deve eseguire l'override di questi metodi, e questi metodi verranno attivati in risposta toointeracting con hub di notifica hello.
12. Eseguire l'override di hello **OnRegistered()** metodo **PushHandlerService** utilizzando hello seguente codice:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > In hello **OnRegistered()** codice di sopra, è opportuno notare hello possibilità toospecify tag tooregister per i canali di messaggistica specifici.
    > 
    > 
13. Eseguire l'override di hello **OnMessage** metodo **PushHandlerService** utilizzando hello seguente codice:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Aggiungere il seguente hello **createNotification** e **dialogNotify** metodi troppo**PushHandlerService** per informare gli utenti quando viene ricevuta una notifica.
    
    > [!NOTE]
    > La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti. Se si verifica in Android 5.0 o versioni successive, l'applicazione hello sarà necessario toobe installato notification hello tooreceive. Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Eseguire l'override dei membri astratti **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** per consentire la compilazione del codice:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Eseguire l'app nell'emulatore hello
Se si esegue questa app nell'emulatore hello, assicurarsi di utilizzare un dispositivo virtuale Android (AVD) che supporta APIs Google.

> [!IMPORTANT]
> Nelle notifiche di push tooreceive ordine, è necessario impostare un account Google nel dispositivo virtuale Android. (Nell'emulatore hello passare troppo**impostazioni** e fare clic su **Aggiungi Account**.) Assicurarsi inoltre che tale emulatore hello è connesso toohello Internet.
> 
> [!NOTE]
> La progettazione di notifiche in Android versione 5.0 e successive rappresenta un'importante variazione rispetto alle versioni precedenti. Per altre informazioni, vedere [Notifiche di Android](http://go.microsoft.com/fwlink/?LinkId=615880).
> 
> 

1. In **Tools** (Strumenti) fare clic su **Open Android Emulator Manager** (Apri Gestione emulatori Android), selezionare il dispositivo e quindi fare clic su **Edit** (Modifica).
   
      ![][18]
2. Selezionare **Google APIs** (API Google) in **Target** (Destinazione) e quindi fare clic su **OK**.
   
      ![][19]
3. Nella barra degli strumenti superiore hello, fare clic su **eseguire**e quindi selezionare l'app. Questo Avvia emulatore hello e si esegue l'applicazione hello.
   
   app Hello recupera hello *registrationId* da GCM e i registri con hub di notifica hello.

## <a name="send-notifications-from-your-backend"></a>Inviare notifiche dal back-end
È possibile testare una ricezione di notifiche dell'App per l'invio di notifiche in hello [portale di Azure classico] tramite hello debug scheda hub di notifica hello, come illustrato nella schermata di hello riportata di seguito.

![][30]

Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile. È inoltre possibile utilizzare hello API REST direttamente i messaggi di notifica toosend se una raccolta non è disponibile per il back-end.

Di seguito è riportato un elenco di alcune altre esercitazioni è consigliabile tooreview per l'invio di notifiche:

* ASP.NET: Vedere [toousers le notifiche di utilizzare gli hub di notifica toopush].
* Java di hub di notifica Azure SDK: vedere [come hub di notifica da Java toouse](notification-hubs-java-push-notification-tutorial.md) per l'invio di notifiche da Java. È stato testato in Eclipse per lo sviluppo per Android.
* PHP: Vedere [come hub di notifica da PHP toouse](notification-hubs-php-push-notification-tutorial.md).

Nelle sottosezioni riportate avanti di hello di esercitazione hello, inviare notifiche tramite un'applicazione console .NET e tramite un servizio mobile tramite uno script di nodo.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Facoltativo) Inviare notifiche tramite un'app .NET
In questa sezione si invieranno notifiche con un'app console .NET.

1. Creare una nuova applicazione console in Visual C#:
   
      ![][20]
2. In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.
   
    Consente di visualizzare la Console di gestione pacchetti hello in Visual Studio.
3. Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Aprire il file Program.cs hello e aggiungere il seguente hello `using` istruzione:
   
        using Microsoft.Azure.NotificationHubs;
5. Nel `Program` classe, aggiungere al metodo hello. Aggiornamento del testo segnaposto hello con il *DefaultFullSharedAccessSignature* nome hub e di stringa di connessione da hello [portale di Azure classico].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Aggiungere hello righe in seguito il **Main** metodo:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Premere hello F5 toorun chiave hello app. Si riceverà una notifica nell'app hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Facoltativo) Inviare notifiche tramite un servizio mobile
1. Guardare [Introduzione a Servizi mobili].
2. Accedi toohello [portale di Azure classico]e selezionare il servizio mobile.
3. Seleziona hello **dell'utilità di pianificazione** scheda nella parte superiore di hello.
   
      ![][22]
4. Creare un nuovo processo pianificato, immettere un nome, quindi scegliere **On demand**.
   
      ![][23]
5. Quando viene creato il processo di hello, selezionare il nome di processo hello. Quindi fare clic su hello **Script** scheda nella barra superiore hello.
6. Inserire lo script all'interno di una funzione dell'utilità di pianificazione seguente hello. Segnaposto hello tooreplace che con la notifica hub hello nome e la stringa di connessione per rendere *DefaultFullSharedAccessSignature* ottenuti in precedenza. Fare clic su **Salva**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Fare clic su **Esegui una volta** nella barra inferiore hello. Si dovrebbe ricevere una notifica di tipo avviso popup.

## <a name="next-steps"></a>Passaggi successivi
In questo semplice esempio, si trasmessa tooall notifiche con i dispositivi Android. In ordine tootarget utenti specifici, vedere l'esercitazione toohello [toousers le notifiche di utilizzare gli hub di notifica toopush]. Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie]. Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica] e hello [gli hub di notifica come toofor Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introduzione a Servizi mobili]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[portale di Azure classico]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[gli hub di notifica come toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers le notifiche di utilizzare gli hub di notifica toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente client di Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/
[Componente di messaggistica di Azure]: http://components.xamarin.com/view/azure-messaging
