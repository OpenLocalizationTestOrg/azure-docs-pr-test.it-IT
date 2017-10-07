---
title: notifiche push aaaSending con gli hub di notifica di Azure in Windows Phone | Documenti Microsoft
description: "In questa esercitazione, è illustrato come le notifiche di toopush gli hub di notifica di Azure toouse tooa Windows Phone 8 o applicazione Silverlight di Windows Phone 8.1."
services: notification-hubs
documentationcenter: windows
keywords: notifica push, inviare notifiche push, push per windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Invio di notifiche push con Hub di notifica di Azure in Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Questa esercitazione illustra come applicazione Windows Phone 8 o Windows Phone 8.1 Silverlight tooa notifiche push toouse toosend di hub di notifica di Azure. Se la destinazione è Windows Phone 8.1 (non Silverlight), quindi fare riferimento toohello [universali di Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versione.
In questa esercitazione, si crea un'app di Windows Phone 8 vuota che riceve le notifiche push tramite hello Microsoft Push Notification Service (MPNS). Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.

> [!NOTE]
> Hello SDK di Windows Phone hub di notifica non supporta l'utilizzo di hello Windows Push Notification Service (WNS) con App Windows Phone 8.1 Silverlight. toouse WNS (anziché MPNS) con App Windows Phone 8.1 Silverlight, seguire hello [gli hub di notifica - esercitazione di Windows Phone Silverlight], che utilizza le API REST.
> 
> 

esercitazione Hello illustra hello semplice scenario di trasmissione con gli hub di notifica.

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* [Visual Studio 2012 Express per Windows Phone]o versione successiva

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub notifica relative ad app per Windows Phone 8.

## <a name="create-your-notification-hub"></a>Creare l'hub di notifica
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Fare clic su hello <b>Notification Services</b> sezione (all'interno di <i>impostazioni</i>), fare clic su <b>Windows Phone (MPNS)</b> e quindi fare clic su hello <b>abilitare push non autenticate </b> casella di controllo.</p>
</li>
</ol>

&emsp;&emsp;![Portale di Azure - Abilita notifiche push non autenticate](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

L'hub è creato e configurato toosend non autenticati di notifica per Windows Phone.

> [!NOTE]
> In questa esercitazione verrà usato il Servizio notifica Push Microsoft in modalità senza autenticazione. Modalità non autenticata MPNS prevede restrizioni delle notifiche che è possibile inviare tooeach canale. Hub di notifica supporta [MPNS autenticato modalità](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) consentendo tooupload il certificato.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Connessione hub di notifica toohello app
1. In Visual Studio creare una nuova applicazione per Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    In Visual Studio 2013 Update 2 o versioni successive verrà invece creata un'applicazione per Windows Phone Silverlight.
   
    ![Visual Studio - Nuovo progetto - App vuota - Windows Phone Silverlight][11]
2. In Visual Studio, fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet**.
   
    Consente di visualizzare hello **Gestisci pacchetti NuGet** la finestra di dialogo.
3. Cercare `WindowsAzure.Messaging.Managed` e fare clic su **installare**, quindi accettare i termini di hello di utilizzo.
   
    ![Visual Studio - Gestione pacchetti NuGet][20]
   
    Questo download, si installa e si aggiunge una raccolta di informazioni di riferimento toohello messaggistica di Azure per Windows utilizzando hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacchetto WindowsAzure.Messaging.Managed NuGet</a>.
4. Aprire il file di hello App.xaml.cs e aggiungere il seguente hello `using` istruzioni:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Aggiungere hello seguente di codice in cima hello **Application_Launching** metodo App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > valore di Hello **MyPushChannel** è un indice che non toolookup usato un canale esistente in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) insieme. Se non è disponibile, creare una nuova voce con lo stesso nome.
   > 
   > 
   
    Verificare che la stringa di connessione hub e hello tooinsert hello nome **DefaultListenSharedAccessSignature** ottenuto nella sezione precedente hello.
    Questo codice recupera l'URI del canale hello per app hello da MPNS e quindi tale URI del canale viene registrata con l'hub di notifica. Garantisce inoltre il canale hello che URI è registrato nell'hub di notifica che viene avviata un'applicazione hello ogni ora.
   
   > [!NOTE]
   > In questa esercitazione invia un dispositivo toohello notifica di tipo avviso popup. Quando si invia una notifica di tipo riquadro, è necessario chiamare invece hello **BindToShellTile** metodo sul canale hello. toosupport le notifiche di tipo avviso popup e riquadro, chiamare sia **BindToShellTile** e **BindToShellToast**.
   > 
   > 
6. In Esplora soluzioni, espandere **proprietà**aprire hello `WMAppManifest.xml` file, fare clic su hello **funzionalità** scheda e verificare che tale hello **ID_CAP_PUSH_NOTIFICATION** funzionalità è selezionata.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Hello premere `F5` toorun chiave hello app.
   
    Viene visualizzato un messaggio di registrazione nell'app hello.
8. Chiudi hello app.  
   
   > [!NOTE]
   > tooreceive una notifica push di tipo avviso popup, un'applicazione hello non deve essere in esecuzione in primo piano hello.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Inviare notifiche push dal back-end
È possibile inviare notifiche push tramite hub di notifica da qualsiasi back-end tramite hello pubblico <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaccia REST</a>. In questa esercitazione vengono inviate notifiche push con un'applicazione console .NET. 

Per un esempio di come toosend notifiche push da un back-end ASP.NET WebAPI integrata con gli hub di notifica, vedere [notifica hub di notifica gli utenti di Azure con back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Per un esempio di come le notifiche push toosend utilizzando hello [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), estrarre [come toouse gli hub di notifica da Java](notification-hubs-java-push-notification-tutorial.md) e [come toouse gli hub di notifica da PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Soluzione di hello pulsante destro del mouse, selezionare **Aggiungi** e **nuovo progetto...** , quindi in **Visual c#**, fare clic su **Windows** e **applicazione Console**, fare clic su **OK**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Aggiunge una nuovo Visual c# toohello soluzione di applicazione console. Questa operazione può essere eseguita anche in una soluzione separata.
2. Fare clic su **Strumenti**, su **Gestione pacchetti libreria** e quindi su **Console di Gestione Pacchetti**.
   
    Consente di visualizzare hello Console di gestione pacchetti.
3. In hello **Package Manager Console** finestra, hello set **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
4. Aprire hello `Program.cs` file e aggiungere il seguente hello `using` istruzione:
   
        using Microsoft.Azure.NotificationHubs;
5. In hello `Program` classe, aggiungere al metodo hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Verificare che hello tooreplace `<hub name>` con nome hello dell'hub di notifica hello visualizzata nel portale di hello. Inoltre, sostituire i segnaposto di stringa di connessione hello con hello stringa di connessione denominata **DefaultFullSharedAccessSignature** ottenuto nella sezione hello "Configurare l'hub di notifica".
   
   > [!NOTE]
   > Assicurarsi di utilizzare la stringa di connessione hello con **completo** non accedere **ascolto** accesso. stringa di accesso listen Hello non dispone di notifiche push toosend di autorizzazioni.
   > 
   > 
6. Aggiungere hello seguente riga del `Main` metodo:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Con il Windows Phone emulatore in esecuzione e il progetto di applicazione console di app hello chiuso, impostare come hello predefinito di progetto di avvio e quindi premere hello `F5` toorun chiave hello app.
   
    Verrà visualizzata una notifica push di tipo avviso popup. Toccando il banner di tipo avviso popup hello carica app hello.

È possibile trovare tutti i payload possibili hello in hello [catalogo toast] e [riquadro catalogo] argomenti su MSDN.

## <a name="next-steps"></a>Passaggi successivi
In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi Windows Phone 8. 

In ordine tootarget utenti specifici, vedere toohello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione. 

Se si desidera toosegment utenti dai gruppi di interesse, è possibile leggere [toosend gli hub di notifica di utilizzare le ultime notizie]. 

Altre informazioni su come hub di notifica toouse in [materiale sussidiario per gli hub di notifica].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express per Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers le notifiche di utilizzare gli hub di notifica toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catalogo toast]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[riquadro catalogo]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[gli hub di notifica - esercitazione di Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

