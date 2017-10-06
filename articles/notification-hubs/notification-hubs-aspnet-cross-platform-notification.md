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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="f5921-103">Inviare notifiche multipiattaforma toousers con gli hub di notifica</span><span class="sxs-lookup"><span data-stu-id="f5921-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="f5921-104">Nell'esercitazione precedente hello [notificare agli utenti con gli hub di notifica], si è appreso come dispositivi di tooall notifiche toopush registrata da un utente autenticato specifico.</span><span class="sxs-lookup"><span data-stu-id="f5921-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="f5921-105">In tale esercitazione più richieste sono state necessarie toosend una piattaforma client supportata tooeach di notifica.</span><span class="sxs-lookup"><span data-stu-id="f5921-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="f5921-106">Notifica gli hub supporta modelli, che consentono di specificare come un dispositivo specifico richiede tooreceive notifiche.</span><span class="sxs-lookup"><span data-stu-id="f5921-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="f5921-107">Questa capacità semplifica l'invio di notifiche tra piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="f5921-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="f5921-108">Questo argomento viene illustrato come usare tootake toosend di modelli, in una singola richiesta, una notifica indipendente dalla piattaforma per tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="f5921-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="f5921-109">Per informazioni dettagliate sui modelli, vedere [Panoramica dell'Hub di notifica][Templates].</span><span class="sxs-lookup"><span data-stu-id="f5921-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5921-110">Progetti creati con Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f5921-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="f5921-111">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="f5921-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="f5921-112">Gli hub di notifica consente un tooregister dispositivo più modelli con hello stesso tag.</span><span class="sxs-lookup"><span data-stu-id="f5921-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="f5921-113">In questo caso, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitate dispositivo toohello, uno per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="f5921-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="f5921-114">In questo modo si toodisplay hello stesso messaggio in più notifiche visive, ad esempio come un badge e come notifica di tipo avviso popup in un'applicazione Windows Store.</span><span class="sxs-lookup"><span data-stu-id="f5921-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="f5921-115">Completare hello notifiche passaggi toosend multipiattaforma utilizzando i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5921-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="f5921-116">In Esplora soluzioni in Visual Studio hello, espandere hello **controller** cartella, il file di RegisterController.cs hello aperto.</span><span class="sxs-lookup"><span data-stu-id="f5921-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="f5921-117">Individuare il blocco di hello di codice in hello **inserire** metodo che crea una nuova registrazione sostituire hello `switch` contenuto con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f5921-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="f5921-118">Questo codice chiama hello metodo specifico della piattaforma toocreate una registrazione di modello anziché una registrazione nativa.</span><span class="sxs-lookup"><span data-stu-id="f5921-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="f5921-119">Non è necessario modificare le registrazioni esistenti, in quanto le registrazioni modello derivano da registrazioni native.</span><span class="sxs-lookup"><span data-stu-id="f5921-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="f5921-120">In hello **notifiche** controller, sostituire hello **sendNotification** metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f5921-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="f5921-121">Questo codice viene inviata una notifica tooall piattaforme in hello stesso e senza toospecify un payload nativo.</span><span class="sxs-lookup"><span data-stu-id="f5921-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="f5921-122">Compila gli hub di notifica e recapita hello dispositivo tooevery payload corretto con hello fornito *tag* valore, come indicato nei modelli di hello registrato.</span><span class="sxs-lookup"><span data-stu-id="f5921-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="f5921-123">Pubblicare di nuovo il progetto back-end WebApi.</span><span class="sxs-lookup"><span data-stu-id="f5921-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="f5921-124">Eseguire nuovamente l'applicazione client hello e verificare che la registrazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f5921-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="f5921-125">(Facoltativo) Distribuire hello client app tooa secondo dispositivo, quindi eseguire l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f5921-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="f5921-126">Si noti che verrà visualizzata una notifica su ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5921-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5921-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5921-127">Next Steps</span></span>
<span data-ttu-id="f5921-128">Dopo avere completato questa esercitazione, è possibile reperire altre informazioni su Hub di notifica e sui modelli nei seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="f5921-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="f5921-129">**[Utilizzare gli hub di notifica toosend le ultime notizie]**</span><span class="sxs-lookup"><span data-stu-id="f5921-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="f5921-130">Questo argomento descrive un altro scenario per l'uso dei modelli.</span><span class="sxs-lookup"><span data-stu-id="f5921-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="f5921-131">**[Panoramica dell'Hub di notifica][Templates]**</span><span class="sxs-lookup"><span data-stu-id="f5921-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="f5921-132">Panoramica con informazioni dettagliate sui modelli.</span><span class="sxs-lookup"><span data-stu-id="f5921-132">Overview topic has more detailed information on templates.</span></span>

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
