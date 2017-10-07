---
title: aaaiOS le notifiche Push con hub di notifica per App Xamarin | Documenti Microsoft
description: In questa esercitazione viene illustrato applicazione iOS Xamarin tooa di notifiche push toouse toosend di hub di notifica di Azure.
services: notification-hubs
keywords: notifiche push di ios,messaggi push,notifiche push,messaggio push
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Notifiche push di iOS con Hub di notifica per app Xamarin
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Questa esercitazione illustra applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure.
Creerai un'app xamarin vuota che riceve le notifiche push tramite hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app. Hello codice completato è disponibile in hello [app hub di notifica] [ GitHub] esempio.

Questa esercitazione illustra hello scenario broadcast messaggio push semplice con gli hub di notifica.

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* [Xcode 6.0][Install Xcode]
* Dispositivo compatibile con iOS 7.0 o versione successiva
* Iscrizione a iOS Developer Program
* [Xamarin Studio]
  
  > [!NOTE]
  > A causa dei requisiti di configurazione per le notifiche push iOS, è necessario distribuire e testare l'applicazione di esempio hello in un dispositivo fisico iOS (iPhone o iPad) anziché nel simulatore hello.
  > 
  > 

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per Xamarin.iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Configurare l'hub di notifica
In questa sezione viene illustrata la creazione di un nuovo hub di notifica e la configurazione dell'autenticazione con il servizio APN utilizzando hello **. p12** certificato push creato. Se si desidera toouse un hub di notifica che è già stato creato, è possibile ignorare toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Dal momento che una connessione del servizio APN hello tooconfigure, nel portale di Azure, hello aprire le impostazioni di Hub di notifica, fare clic su ande su <b>Notification Services</b>, quindi fare clic su hello <b>Apple (APNS)</b> elemento nell'elenco di hello. Al termine, fare clic su <b>carica certificato</b> e seleziona hello <b>. p12</b> certificato esportato in precedenza, nonché password hello hello certificato.</p>

<p>Verificare che tooselect <b>Sandbox</b> modalità poiché si inviano push di messaggi in un ambiente di sviluppo. Utilizzare solo hello <b>produzione</b> se si desidera che toousers di notifiche push toosend che hanno già acquistato l'app dall'archivio hello.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Hub di notifica è ora configurato toowork con il servizio APN e aver tooregister stringhe di connessione hello app e inviare notifiche push.

## <a name="connect-your-app-toohello-notification-hub"></a>Connettere l'hub di notifica toohello app
#### <a name="create-a-new-project"></a>Creare un nuovo progetto
1. In Xamarin Studio, creare un nuovo progetto di iOS e selezionare hello **Unified API** > **singola visualizzazione applicazione** modello.
   
     ![Xamarin Studio: selezionare il tipo di applicazione][31]
2. Aggiungere un componente di messaggistica di Azure toohello di riferimento. In visualizzazione soluzione hello, fare clic sul hello **componenti** cartella per il progetto e scegliere **ottenere più componenti**. Ricerca di hello **messaggistica di Azure** componente e aggiungere hello componente tooyour progetto.
3. In **appdelegate. cs**, aggiungere hello seguente istruzione using:
   
        using WindowsAzure.Messaging;
4. Dichiarare un'istanza di **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Creare un **Constants.cs** classe con hello seguenti variabili:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. In **appdelegate. cs**, aggiornare **FinishedLaunching()** seguente hello toomatch:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Eseguire l'override di hello **RegisteredForRemoteNotifications()** metodo **appdelegate. cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Eseguire l'override di hello **ReceivedRemoteNotification()** metodo **appdelegate. cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Creare i seguenti hello **ProcessNotification()** metodo **appdelegate. cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > È possibile scegliere toooverride **FailedToRegisterForRemoteNotifications()** toohandle situazioni, ad esempio alcuna connessione di rete. Ciò è particolarmente importante in utente hello potrebbe avviare l'applicazione in modalità offline (ad esempio aereo) e si desidera push toohandle app tooyour specifici scenari di messaggistica.
   > 
   > 
10. Eseguire l'applicazione hello sul dispositivo.

## <a name="sending-push-notifications"></a>Invio di notifiche push
È possibile eseguire test di ricevere le notifiche push nell'app per l'invio di notifiche in hello [portale Azure] tramite hello **invio di Test** funzionalità hello **risoluzione dei problemi** set di strumenti, a destra nella hello hub pagina di notifica, come illustrato nella schermata di hello riportata di seguito.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Le notifiche push vengono in genere inviate attraverso un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile. Inoltre, è possibile utilizzare hello API REST direttamente push toosend messaggi in caso di una libreria non è disponibile nel proprio scenario. 

In questa esercitazione verrà semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end. Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione. Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:

* **Interfaccia REST**: È possibile supportare la notifica push su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).

**App per dispositivi mobili**: per un esempio di come toosend notifiche da un back-end dell'App Mobile di servizio App di Azure che è integrato con hub di notifica, vedere [app mobile tooyour le notifiche push Aggiungi](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java o PHP**: per un esempio di come le notifiche push toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(Facoltativo) Inviare notifiche push da un'app console .NET.
In questa sezione si invieranno notifiche push con una semplice app console .NET. Ai fini di hello di questo esempio, si passerà tooa ambiente di sviluppo di Windows che è già installato Visual Studio.

1. In Visual Studio creare una nuova applicazione console in Visual C#:
   
       ![Visual Studio - Create a new console application][213]
2. In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.
   
    console di gestione pacchetti Hello dovrebbe essere visualizzato toohello ancorato inferiore dell'area di lavoro di Visual Studio.
3. Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Aprire hello `Program.cs` file e aggiungere il seguente hello `using` istruzione, garantendo che è possibile utilizzare le classi di Azure e le funzioni all'interno della classe principale:
   
        using Microsoft.Azure.NotificationHubs;
5. Nel `Program` classe, aggiungere al metodo hello (non dimenticare hello tooreplace **stringa di connessione** e **nome hub**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Aggiungere hello righe in seguito il `Main` metodo:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Premere hello F5 toorun chiave hello app. Entro pochi secondi dovrebbe essere visualizzata una notifica push nel dispositivo. Se si utilizza Wi-Fi o una rete cellulare dati, assicurarsi di disporre di una connessione internet sul dispositivo hello.

È possibile trovare tutti i payload possibili hello in hello Apple [locali e Guida per programmatori notifica Push].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(Facoltativo) Inviare notifiche da un servizio mobile
In questa sezione si invieranno notifiche push usando un servizio mobile con uno script node.

seguire una notifica tramite un servizio mobile, toosend [Introduzione a servizi mobili]e quindi:

1. Accedi toohello [portale di Azure classico]e selezionare il servizio mobile.
2. Seleziona hello **dell'utilità di pianificazione** scheda nella parte superiore di hello.
   
       ![Azure Classic Portal - Scheduler][215]
3. Creare un nuovo processo pianificato, immettere un nome, quindi scegliere **On demand**.
   
       ![Azure Classic Portal - Create new job][216]
4. Quando viene creato il processo di hello, selezionare il nome di processo hello. Quindi fare clic su hello **Script** scheda nella barra superiore hello.
5. Inserire lo script all'interno di una funzione dell'utilità di pianificazione seguente hello. Segnaposto hello tooreplace che con la notifica hub hello nome e la stringa di connessione per rendere *DefaultFullSharedAccessSignature* ottenuti in precedenza. Fare clic su **Salva**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Fare clic su **Esegui una volta** nella barra inferiore hello. Si dovrebbe ricevere un avviso sul dispositivo.

## <a name="next-steps"></a>Passaggi successivi
In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi iOS. In ordine tootarget utenti specifici, vedere l'esercitazione toohello [toousers le notifiche di utilizzare gli hub di notifica toopush]. Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie]. Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica] e hello [toofor con gli hub di notifica come iOS].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Introduzione a servizi mobili]: /develop/mobile/tutorials/get-started-xamarin-ios
[portale di Azure classico]: https://manage.windowsazure.com/
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[toofor con gli hub di notifica come iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers le notifiche di utilizzare gli hub di notifica toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet

[locali e Guida per programmatori notifica Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[portale Azure]: https://portal.azure.com
