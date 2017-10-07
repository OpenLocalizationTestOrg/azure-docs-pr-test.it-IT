---
title: aaaAdd push notifiche tooyour xamarin app con il servizio App di Azure
description: Informazioni su app xamarin tooyour di notifiche push toouse toosend di servizio App di Azure
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="ca3f5-103">Aggiungere le notifiche di push tooyour Xamarin.iOS App</span><span class="sxs-lookup"><span data-stu-id="ca3f5-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="ca3f5-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ca3f5-104">Overview</span></span>
<span data-ttu-id="ca3f5-105">In questa esercitazione, si aggiunge toohello le notifiche push [xamarin introduttiva](app-service-mobile-xamarin-ios-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="ca3f5-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="ca3f5-107">Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca3f5-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ca3f5-108">Prerequisites</span></span>
* <span data-ttu-id="ca3f5-109">Hello completo [delle Guide rapide xamarin](app-service-mobile-xamarin-ios-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="ca3f5-110">Un dispositivo iOS fisico.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-110">A physical iOS device.</span></span> <span data-ttu-id="ca3f5-111">Notifiche push non sono supportate dal simulatore iOS hello.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="ca3f5-112">Registrare l'applicazione hello per le notifiche push nel portale per sviluppatori di Apple</span><span class="sxs-lookup"><span data-stu-id="ca3f5-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="ca3f5-113">Configurare le notifiche push toosend di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="ca3f5-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="ca3f5-114">Aggiornare le notifiche push di hello server progetto toosend</span><span class="sxs-lookup"><span data-stu-id="ca3f5-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="ca3f5-115">Configurare il progetto Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="ca3f5-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="ca3f5-116">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="ca3f5-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="ca3f5-117">In **QSTodoService**, aggiungere hello seguente proprietà in modo che **AppDelegate** può acquisire client mobili hello:</span><span class="sxs-lookup"><span data-stu-id="ca3f5-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="ca3f5-118">Aggiungere il seguente hello `using` hello cima toohello istruzione **appdelegate. cs** file.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="ca3f5-119">In **AppDelegate**, eseguire l'override di hello **FinishedLaunching** evento:</span><span class="sxs-lookup"><span data-stu-id="ca3f5-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="ca3f5-120">In hello stesso file, eseguire l'override di hello **RegisteredForRemoteNotifications** evento.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="ca3f5-121">In questo codice si sta registrando per una notifica modello semplice che verrà inviata dal server hello in tutte le piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="ca3f5-122">Per ulteriori informazioni sui modelli con Hub di notifica, vedere [Modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ca3f5-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="ca3f5-123">Quindi, eseguire l'override hello **DidReceivedRemoteNotification** evento:</span><span class="sxs-lookup"><span data-stu-id="ca3f5-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="ca3f5-124">L'app è notifiche push toosupport aggiornato.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="ca3f5-125"><a name="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="ca3f5-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="ca3f5-126">Hello premere **eseguire** progetto hello toobuild e avviare l'applicazione hello in un dispositivo in grado di iOS, quindi scegliere **OK** tooaccept le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ca3f5-127">È necessario accettare le notifiche push in modo esplicito dall'app.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="ca3f5-128">Questa richiesta si verifica solo hello prima volta che l'esecuzione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="ca3f5-129">Nell'app hello, digitare un'attività e quindi fare clic su hello segno più (**+**) icona.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="ca3f5-130">Verificare che viene ricevuta una notifica, quindi fare clic su **OK** toodismiss hello notifica.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="ca3f5-131">Ripetere il passaggio 2 e chiusura immediatamente hello app, quindi verificare che sia visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="ca3f5-132">L'esercitazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ca3f5-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



