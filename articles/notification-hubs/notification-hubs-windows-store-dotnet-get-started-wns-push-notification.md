---
title: aaaGet avviato con Azure notifica hub per App universali di Windows piattaforma | Documenti Microsoft
description: "In questa esercitazione, è illustrato come toouse gli hub di notifica di Azure toopush notifiche tooa applicazione piattaforma universale di Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Introduzione ad Hub di notifica per le app della piattaforma UWP (Universal Windows Platform)
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push app Universal Windows Platform (UWP) tooa di notifiche.

In questa esercitazione, si crea un'app di Windows Store vuota che riceve le notifiche push tramite servizio notifica Push Windows (WNS) hello. Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.

## <a name="before-you-begin"></a>Prima di iniziare
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) o versione successiva
* [Strumenti per lo sviluppo di app di Windows universale](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Account Azure attivo  <br/>Se non si dispone di un account Azure, è possibile creare un account di valutazione gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Account di Windows Store attivo

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app della piattaforma UWP (Universal Windows Platform).

## <a name="register-your-app-for-hello-windows-store"></a>Registrare l'app per Windows Store hello
toosend le app tooUWP le notifiche push, è necessario associare il toohello app Windows Store. È quindi necessario configurare il toointegrate di hub di notifica con WNS.

1. Se non è già stato registrato l'app, passare toohello [Windows Dev Center](https://dev.windows.com/overview), accedere con l'account Microsoft e quindi fare clic su **crea una nuova app**.

2. Digitare un nome per l'app e fare clic su **Riserva nome dell'app**. Verrà creata una nuova registrazione a Windows Store per l'app.

3. In Visual Studio, creare un nuovo progetto di Visual c# di App Store utilizzando universali di Windows hello **applicazione vuota** modello e fare clic su **OK**.

4. Accettare i valori predefiniti di hello per le versioni di piattaforma minimo e di destinazione di hello.

5. In Esplora soluzioni, progetti di app Windows Store hello pulsante destro del mouse, fare clic su **archivio**, quindi fare clic su **Associa applicazione a Store hello...** . hello **associare un'App con Windows Store hello** procedura guidata viene visualizzata.

6. Nella procedura guidata hello, accedere con l'account Microsoft.

7. Fare clic su app hello registrato nel passaggio 2, fare clic su **Avanti**, quindi fare clic su **associare**. Consente di aggiungere il manifesto di applicazione toohello hello richiesto Windows Store registrazione informazioni.

8. In hello [Windows Dev Center](http://dev.windows.com/overview) pagina per la nuova app, fare clic su **servizi**, fare clic su **notifiche Push**, quindi fare clic su **WNS o MPNS**.

9. Fare clic su **Nuova notifica**.

10. Fare clic sul modello **Blank (Toast)** (Vuoto - Avviso popup) e quindi fare clic su **OK**.

11. Immettere un **nome** per la notifica e un messaggio **contesto** visivo. Fare clic su **Salva come bozza**.

12. Passare toohello [portale di registrazione applicazione](http://apps.dev.microsoft.com) ed effettuare l'accesso.

13. Fare clic sul nome dell'applicazione. Prendere nota di hello **segreto dell'applicazione** password e hello **ID di pacchetto sicurezza (SID)** si trova in hello **Windows Store** impostazioni piattaforma.

     > [AZURE.WARNING]
    segreto dell'applicazione Hello e il SID pacchetto sono credenziali di sicurezza importanti. Non condividere questi valori con altri utenti né distribuirli con l'app.

## <a name="configure-your-notification-hub"></a>Configurare l'hub di notifica
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Seleziona hello <b>Notification Services</b> opzione e hello <b>Windows (WNS)</b> opzione. Immettere quindi hello <b>segreto dell'applicazione</b> password in hello <b>chiave di sicurezza</b> campo. Immettere il <b>SID pacchetto</b> valore che è stato ottenuto da WNS nella sezione precedente hello e quindi fare clic su <b>salvare</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Hub di notifica è ora configurato toowork con WNS e aver tooregister stringhe di connessione hello app e inviare notifiche.

## <a name="connect-your-app-toohello-notification-hub"></a>Connettere l'hub di notifica toohello app
1. In Visual Studio, fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet**.
   
    Consente di visualizzare hello **Gestisci pacchetti NuGet** la finestra di dialogo.
2. Cercare `WindowsAzure.Messaging.Managed` e fare clic su **installare**e accettare le condizioni di hello d'uso.
   
    ![][20]
   
    Questo download, si installa e si aggiunge una raccolta di informazioni di riferimento toohello messaggistica di Azure per Windows utilizzando hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacchetto WindowsAzure.Messaging.Managed NuGet</a>.
3. Aprire il file di progetto App.xaml.cs hello e aggiungere il seguente hello `using` istruzioni. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Anche in App.xaml.cs, aggiungere il seguente hello **InitNotificationsAsync** toohello definizione di metodo **App** classe:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Questo codice recupera l'URI del canale hello per app hello da WNS e quindi tale URI del canale viene registrata con l'hub di notifica.
   
   > [!NOTE]
   > Verificare che tooreplace hello segnaposto "il nome hub" con il nome di hello dell'hub di notifica hello che viene visualizzato nel portale di Azure hello. Sostituire i segnaposto di stringa di connessione hello anche con hello **DefaultListenSharedAccessSignature** stringa di connessione che è stato ottenuto da hello **criteri di accesso** pagina dell'Hub di notifica in un sezione precedente.
   > 
   > 
5. Nella parte superiore di hello di hello **OnLaunched** gestore dell'evento in App.xaml.cs, aggiungere hello seguente chiamata toohello nuova **InitNotificationsAsync** metodo:
   
        InitNotificationsAsync();
   
    In questo modo si garantisce il canale hello che URI è registrato nell'hub di notifica che viene avviata un'applicazione hello ogni ora.
6. Hello premere **F5** toorun chiave hello app. Viene visualizzata una finestra di dialogo popup che contiene la chiave di registrazione hello.

L'app è pronta tooreceive popup.

## <a name="send-notifications"></a>Inviare notifiche
È possibile verificare rapidamente la ricezione di notifiche nell'app mediante l'invio di notifiche in hello [portale Azure](https://portal.azure.com/) utilizzando hello **invio di Test** pulsante hub di notifica hello, come illustrato nella schermata di hello riportata di seguito.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Le notifiche push vengono in genere inviate in un servizio back-end come Servizi mobili o ASP.NET usando una libreria compatibile. È inoltre possibile utilizzare hello API REST direttamente i messaggi di notifica toosend se una raccolta non è disponibile per il back-end. 

In questa esercitazione verrà semplicità e illustrano solo test dell'app client per l'invio di notifiche tramite hello .NET SDK per gli hub di notifica in un'applicazione console anziché un servizio back-end. Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] come passaggio successivo di hello per l'invio di notifiche da un back-end ASP.NET dell'esercitazione. Tuttavia, è possibile utilizzare hello approcci seguenti per l'invio di notifiche:

* **Interfaccia REST**: È possibile supportare la notifica su qualsiasi piattaforma back-end utilizzando hello [interfaccia REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure notifica hub .NET SDK**: In hello Gestione pacchetti Nuget per Visual Studio, eseguire [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [come hub di notifica da Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).
* **App per dispositivi mobili Azure**: per un esempio di come le notifiche di toosend da un'App Mobile di Azure è integrato con hub di notifica, vedere [aggiungere notifiche push per App per dispositivi mobili](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java o PHP**: per un esempio di come le notifiche toosend utilizzando hello API REST, vedere "come hub di notifica da Java o PHP toouse" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Facoltativo) Inviare notifiche da un'app console
le notifiche toosend tramite un'applicazione console .NET seguono questi passaggi. 

1. Soluzione di hello pulsante destro del mouse, selezionare **Aggiungi** e **nuovo progetto...** , quindi in **Visual c#**, fare clic su **Windows** e **applicazione Console**, fare clic su **OK**.
   
    Aggiunge una nuovo Visual c# toohello soluzione di applicazione console. Questa operazione può essere eseguita anche in una soluzione separata.

2. In Visual Studio fare clic su **Strumenti**, selezionare **Gestione pacchetti NuGet** e quindi **Console di Gestione pacchetti**.
   
    Consente di visualizzare la Console di gestione pacchetti hello in Visual Studio.
3. Nella finestra della Console di gestione pacchetti hello, impostare hello **progetto predefinito** tooyour nuovo progetto applicazione console e quindi nella finestra di console hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Aggiunge un toohello riferimento SDK di hub di notifica di Azure utilizzando hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacchetto NuGet di hub Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Aprire il file Program.cs hello e aggiungere il seguente hello `using` istruzione:
   
        using Microsoft.Azure.NotificationHubs;
5. In hello **programma** classe, aggiungere al metodo hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Assicurarsi di utilizzare una stringa di connessione hello è **completo** non accedere **ascolto** accesso. stringa di accesso listen Hello è notifiche toosend autorizzazioni.
   > 
   > 
6. Aggiungere hello seguenti righe hello **Main** metodo:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Fare clic sul progetto applicazione console hello in Visual Studio e fare clic su **imposta come progetto di avvio** tooset come progetto di avvio hello. Premere quindi hello **F5** applicazione hello toorun della chiave.
   
    Tutti i dispositivi registrati riceveranno una notifica di tipo avviso popup. Banner di tipo avviso popup facendo clic o toccando hello carica app hello.

È possibile trovare tutti i payload hello è supportato in hello [catalogo toast], [riquadro catalogo], e [badge Panoramica] argomenti su MSDN.

## <a name="next-steps"></a>Passaggi successivi
In questo semplice esempio è stata inviata notifiche tooall i dispositivi Windows con il portale di hello o un'applicazione console. Si consiglia di hello [toousers le notifiche di utilizzare gli hub di notifica toopush] esercitazione come passaggio successivo hello. Verrà descritto come toosend notifiche da un back-end ASP.NET usando tag tootarget specifici utenti.

Se si desidera che gli utenti dai gruppi di interesse toosegment, vedere [toosend gli hub di notifica di utilizzare le ultime notizie]. 

toolearn informazioni generali sull'hub di notifica, vedere [materiale sussidiario per gli hub di notifica](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers le notifiche di utilizzare gli hub di notifica toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catalogo toast]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[riquadro catalogo]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[badge Panoramica]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
