---
title: aaaAzure notifica hub Secure Push
description: Informazioni su come toosend sicuro le notifiche push in Azure. Esempi di codice scritti in c# utilizzando hello API .NET.
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Push sicuro degli hub di notifica di Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura push di semplice utilizzo, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.

A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello. In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra il dispositivo di client hello e back-end app hello.

In generale, il flusso di hello è il seguente:

1. Hello app back-end:
   * Archivia il payload sicuro nel database back-end.
   * Invia ID hello del dispositivo notifica toohello (viene inviata alcuna informazione protetta).
2. Hello app sul dispositivo hello, quando si riceve notifica hello:
   * dispositivo di Hello contatta hello back-end richiedente hello sicura payload.
   * app Hello possono mostrare payload hello come una notifica sul dispositivo hello.

È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso. In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token. Se l'applicazione non archivia i token di autenticazione nel dispositivo hello, o se i token possono essere scaduti, hello app del dispositivo, al momento della ricezione di notifiche di hello deve essere visualizzato una generica notifica conferma hello utente toolaunch hello app. app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.

Questa esercitazione Secure Push viene illustrato come toosend una notifica push in modo sicuro. Hello esercitazione si basa sulle hello [notifica utenti](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima.

> [!NOTE]
> Questa esercitazione presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Si noti inoltre che Windows Phone 8.1 richiede le credenziali di Windows (non di Windows Phone) e che le attività in background non funzionano in Windows Phone 8.0 o Silverlight 8.1. Per le applicazioni Windows Store, è possibile ricevere notifiche tramite un'attività in background solo se l'applicazione hello è abilitato blocco schermo (scegliere la casella di controllo hello in hello Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Modificare hello progetto Windows Phone
1. In hello **NotifyUserWindowsPhone** del progetto, aggiungere hello attività in background push hello tooregister tooApp.xaml.cs codice seguente. Aggiungere hello successiva riga di codice alla fine hello hello `OnLaunched()` metodo:
   
        RegisterBackgroundTask();
2. Ancora in App.xaml.cs, aggiungere hello seguente codice immediatamente dopo hello `OnLaunched()` metodo:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Aggiungere il seguente hello `using` istruzioni alla parte superiore di hello del file App.xaml.cs hello:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Da hello **File** menu in Visual Studio, fare clic su **Salva tutto**.

## <a name="create-hello-push-background-component"></a>Creare hello Push componente in Background
passaggio successivo Hello è componente di toocreate hello push in background.

1. In Esplora soluzioni, fare clic sul nodo di primo livello della soluzione hello hello (**soluzione SecurePush** in questo caso), quindi fare clic su **Aggiungi**, quindi fare clic su **nuovo progetto**.
2. Espandere **Applicazioni Windows Store**, fare clic su **App di Windows Phone** e quindi su **Componente Windows Runtime (Windows Phone)**. Progetto hello nome **PushBackgroundComponent**, quindi fare clic su **OK** progetto hello toocreate.
   
    ![][12]
3. In Esplora soluzioni fare doppio clic su hello **PushBackgroundComponent (Windows Phone 8.1)** del progetto, quindi fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome nuova classe hello **PushBackgroundTask.cs**. Fare clic su **Aggiungi** classe hello toogenerate.
4. Sostituire l'intero contenuto di hello di hello **PushBackgroundComponent** definizione dello spazio dei nomi con hello nel codice seguente, sostituendo i segnaposto hello `{back-end endpoint}` con endpoint di back-end hello ottenuto durante la distribuzione del back-end:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. In Esplora soluzioni fare doppio clic su hello **PushBackgroundComponent (Windows Phone 8.1)** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.
6. Sul lato sinistro di hello, fare clic su **Online**.
7. In hello **ricerca** digitare **Http Client**.
8. Nell'elenco risultati hello, fare clic su **Microsoft HTTP Client Libraries**, quindi fare clic su **installare**. Completare l'installazione di hello.
9. In hello NuGet **ricerca** digitare **Json.net**. Installare hello **Json.NET** pacchetto, quindi finestra di gestione pacchetti NuGet hello Chiudi.
10. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **PushBackgroundTask.cs** file:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. In Esplora soluzioni, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** del progetto, fare doppio clic su **riferimenti**, quindi fare clic su **Aggiungi riferimento...** . Nella finestra di dialogo Gestione riferimenti hello casella di controllo hello accanto troppo**PushBackgroundComponent**, quindi fare clic su **OK**.
12. In Esplora soluzioni fare doppio clic su **package. appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** progetto. In **notifiche**, impostare **in grado di tipo avviso popup** troppo**Sì**.
    
    ![][3]
13. Ancora in **package. appxmanifest**, fare clic su hello **dichiarazioni** menu superiore hello. In hello **dichiarazioni disponibili** elenco a discesa, fare clic su **attività in Background**, quindi fare clic su **Aggiungi**.
14. In **Package.appxmanifest**, in **Proprietà** selezionare **Notifica Push**.
15. In **package. appxmanifest**in **impostazioni App**, tipo **PushBackgroundComponent.PushBackgroundTask** in hello **punto di ingresso** campo.
    
    ![][13]
16. Da hello **File** menu, fare clic su **Salva tutto**.

## <a name="run-hello-application"></a>Eseguire l'applicazione hello
toorun applicazione hello, hello seguenti:

1. In Visual Studio, eseguire hello **AppBackend** applicazione API Web. Verrà visualizzata una pagina Web ASP.NET.
2. In Visual Studio, eseguire hello **NotifyUserWindowsPhone (Windows Phone 8.1)** app di Windows Phone. emulatore Windows Phone Hello viene eseguito e carica app hello automaticamente.
3. In hello **NotifyUserWindowsPhone** app dell'interfaccia utente, immettere un nome utente e password. Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.
4. In hello **NotifyUserWindowsPhone** app dell'interfaccia utente, fare clic su **Accedi e registrare**. Fare clic su **Send push**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
