---
title: aaaSend multipiattaforma notifiche toousers con gli hub di notifica (ASP.NET)
description: Informazioni su come toouse gli hub di notifica modelli toosend, in una singola richiesta, una notifica indipendente dalla piattaforma per tutte le piattaforme.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Inviare notifiche multipiattaforma toousers con gli hub di notifica
Nell'esercitazione precedente hello [notificare agli utenti con gli hub di notifica], si è appreso come dispositivi di tooall notifiche toopush registrata da un utente autenticato specifico. In tale esercitazione più richieste sono state necessarie toosend una piattaforma client supportata tooeach di notifica. Notifica gli hub supporta modelli, che consentono di specificare come un dispositivo specifico richiede tooreceive notifiche. Questa capacità semplifica l'invio di notifiche tra piattaforme diverse. Questo argomento viene illustrato come usare tootake toosend di modelli, in una singola richiesta, una notifica indipendente dalla piattaforma per tutte le piattaforme. Per informazioni dettagliate sui modelli, vedere [Panoramica dell'Hub di notifica][Templates].
> [!IMPORTANT]
> Progetti creati con Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017. Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Gli hub di notifica consente un tooregister dispositivo più modelli con hello stesso tag. In questo caso, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitate dispositivo toohello, uno per ogni modello. In questo modo si toodisplay hello stesso messaggio in più notifiche visive, ad esempio come un badge e come notifica di tipo avviso popup in un'applicazione Windows Store.
> 
> 

Completare hello notifiche passaggi toosend multipiattaforma utilizzando i modelli seguenti:

1. In Esplora soluzioni in Visual Studio hello, espandere hello **controller** cartella, il file di RegisterController.cs hello aperto.
2. Individuare il blocco di hello di codice in hello **inserire** metodo che crea una nuova registrazione sostituire hello `switch` contenuto con hello seguente codice:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Questo codice chiama hello metodo specifico della piattaforma toocreate una registrazione di modello anziché una registrazione nativa. Non è necessario modificare le registrazioni esistenti, in quanto le registrazioni modello derivano da registrazioni native.
3. In hello **notifiche** controller, sostituire hello **sendNotification** metodo con hello seguente codice:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Questo codice viene inviata una notifica tooall piattaforme in hello stesso e senza toospecify un payload nativo. Compila gli hub di notifica e recapita hello dispositivo tooevery payload corretto con hello fornito *tag* valore, come indicato nei modelli di hello registrato.
4. Pubblicare di nuovo il progetto back-end WebApi.
5. Eseguire nuovamente l'applicazione client hello e verificare che la registrazione ha esito positivo.
6. (Facoltativo) Distribuire hello client app tooa secondo dispositivo, quindi eseguire l'applicazione hello.
   
    Si noti che verrà visualizzata una notifica su ogni dispositivo.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere completato questa esercitazione, è possibile reperire altre informazioni su Hub di notifica e sui modelli nei seguenti argomenti:

* **[Utilizzare gli hub di notifica toosend le ultime notizie]** <br/>Questo argomento descrive un altro scenario per l'uso dei modelli.
* **[Panoramica dell'Hub di notifica][Templates]**<br/>Panoramica con informazioni dettagliate sui modelli.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Utilizzare gli hub di notifica toosend le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[notificare agli utenti con gli hub di notifica]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
