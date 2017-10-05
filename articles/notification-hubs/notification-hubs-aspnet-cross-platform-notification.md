---
title: Uso di Hub di notifica per inviare notifiche agli utenti tra piattaforme diverse
description: Informazioni su come usare i modelli di Hub di notifica per inviare, in un'unica richiesta, una notifica indipendente dalla piattaforma destinata a tutte le piattaforme.
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
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="104cf-103">Uso di Hub di notifica per inviare notifiche agli utenti tra piattaforme diverse</span><span class="sxs-lookup"><span data-stu-id="104cf-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="104cf-104">Nell'esercitazione precedente, [Utilizzo di Hub di notifica per inviare notifiche agli utenti], si è appreso come inviare notifiche push a tutti i dispositivi registrati da uno specifico utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="104cf-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="104cf-105">In tale esercitazione vengono utilizzate più richieste per inviare una notifica a ogni piattaforma client supportata.</span><span class="sxs-lookup"><span data-stu-id="104cf-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="104cf-106">Hub di notifica supporta i modelli, che consentono di specificare il modo in cui un dispositivo desidera ricevere notifiche.</span><span class="sxs-lookup"><span data-stu-id="104cf-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="104cf-107">Questa capacità semplifica l'invio di notifiche tra piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="104cf-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="104cf-108">Questo argomento descrive come servirsi dei modelli per inviare, in un'unica richiesta, una notifica indipendente dalla piattaforma destinata a tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="104cf-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="104cf-109">Per informazioni dettagliate sui modelli, vedere [Panoramica dell'Hub di notifica][Templates].</span><span class="sxs-lookup"><span data-stu-id="104cf-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="104cf-110">Progetti creati con Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="104cf-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="104cf-111">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="104cf-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="104cf-112">Hub di notifica consente a un dispositivo di registrare più modelli con lo stesso tag.</span><span class="sxs-lookup"><span data-stu-id="104cf-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="104cf-113">In questo caso, un messaggio in arrivo destinato a tale tag ha come esito il recapito al dispositivo di più notifiche, una per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="104cf-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="104cf-114">Questo consente di visualizzare lo stesso messaggio in più notifiche visive, ad esempio sia come notifica badge che come notifica di tipo avviso popup in un'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="104cf-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="104cf-115">Per inviare notifiche tra piattaforme diverse utilizzando i modelli, eseguire la procedure seguente:</span><span class="sxs-lookup"><span data-stu-id="104cf-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="104cf-116">In Esplora soluzioni in Visual Studio espandere la cartella **Controllers** e quindi aprire il file RegisterController.cs.</span><span class="sxs-lookup"><span data-stu-id="104cf-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="104cf-117">Nel metodo **Put** individuare il blocco di codice che crea una nuova registrazione e sostituire il contenuto di `switch` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="104cf-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
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
   
    <span data-ttu-id="104cf-118">In questo codice viene chiamato il metodo specifico della piattaforma per creare una registrazione modello anziché una registrazione nativa.</span><span class="sxs-lookup"><span data-stu-id="104cf-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="104cf-119">Non è necessario modificare le registrazioni esistenti, in quanto le registrazioni modello derivano da registrazioni native.</span><span class="sxs-lookup"><span data-stu-id="104cf-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="104cf-120">Nel controller **Notifications** sostituire il metodo **sendNotification** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="104cf-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="104cf-121">Questo codice invia una notifica a tutte le piattaforme nello stesso momento e senza bisogno di specificare un payload nativo.</span><span class="sxs-lookup"><span data-stu-id="104cf-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="104cf-122">Gli hub di notifica creano il payload corretto e lo distribuiscono a tutti i dispositivi con il valore *tag* specificato, come indicato nei modelli registrati.</span><span class="sxs-lookup"><span data-stu-id="104cf-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="104cf-123">Pubblicare di nuovo il progetto back-end WebApi.</span><span class="sxs-lookup"><span data-stu-id="104cf-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="104cf-124">Eseguire nuovamente l'app client e verificare che la registrazione abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="104cf-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="104cf-125">(Facoltativo) Distribuire l'app client in un secondo dispositivo, quindi eseguirla.</span><span class="sxs-lookup"><span data-stu-id="104cf-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="104cf-126">Si noti che verrà visualizzata una notifica su ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="104cf-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="104cf-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="104cf-127">Next Steps</span></span>
<span data-ttu-id="104cf-128">Dopo avere completato questa esercitazione, è possibile reperire altre informazioni su Hub di notifica e sui modelli nei seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="104cf-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="104cf-129">**[Use Notification Hubs to send breaking news]** (Usare gli hub di notifica per inviare le ultime notizie)</span><span class="sxs-lookup"><span data-stu-id="104cf-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="104cf-130">Questo argomento descrive un altro scenario per l'uso dei modelli.</span><span class="sxs-lookup"><span data-stu-id="104cf-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="104cf-131">**[Panoramica dell'Hub di notifica][Templates]**</span><span class="sxs-lookup"><span data-stu-id="104cf-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="104cf-132">Panoramica con informazioni dettagliate sui modelli.</span><span class="sxs-lookup"><span data-stu-id="104cf-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="104cf-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="104cf-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="104cf-134">[Utilizzo di Hub di notifica per inviare notifiche agli utenti]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="104cf-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
