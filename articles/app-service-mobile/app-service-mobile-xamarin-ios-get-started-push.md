---
title: Aggiungere notifiche push all'app Xamarin.iOS tramite il servizio app di Azure
description: Informazioni su come usare il servizio app di Azure per inviare notifiche push all'app Xamarin.iOS.
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
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="0176a-103">Aggiungere notifiche push all'app Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="0176a-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0176a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0176a-104">Overview</span></span>
<span data-ttu-id="0176a-105">In questa esercitazione vengono aggiunte notifiche push al progetto [avvio rapido di Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md), in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="0176a-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="0176a-106">Se non si usa il progetto server di avvio rapido scaricato, sarà necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="0176a-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="0176a-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0176a-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0176a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0176a-108">Prerequisites</span></span>
* <span data-ttu-id="0176a-109">Completare l'esercitazione della [guida introduttiva di Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="0176a-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="0176a-110">Un dispositivo iOS fisico.</span><span class="sxs-lookup"><span data-stu-id="0176a-110">A physical iOS device.</span></span> <span data-ttu-id="0176a-111">Le notifiche push non sono supportate dal simulatore iOS.</span><span class="sxs-lookup"><span data-stu-id="0176a-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="0176a-112">Registrare l'app per le notifiche push nel portale per sviluppatori Apple</span><span class="sxs-lookup"><span data-stu-id="0176a-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="0176a-113">Configurare l'app per dispositivi mobili per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="0176a-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="0176a-114">Aggiornare il progetto server per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="0176a-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="0176a-115">Configurare il progetto Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="0176a-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="0176a-116">Aggiungere notifiche push all'app</span><span class="sxs-lookup"><span data-stu-id="0176a-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="0176a-117">In **QSTodoService** aggiungere la proprietà seguente in modo che l'oggetto **AppDelegate** possa acquisire il client per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="0176a-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
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
2. <span data-ttu-id="0176a-118">Aggiungere l'istruzione `using` seguente all'inizio del file **AppDelegate.cs** .</span><span class="sxs-lookup"><span data-stu-id="0176a-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="0176a-119">In **AppDelegate** eseguire l'override dell'evento **FinishedLaunching**:</span><span class="sxs-lookup"><span data-stu-id="0176a-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="0176a-120">Nello stesso file, eseguire l'override dell'evento **RegisteredForRemoteNotifications** .</span><span class="sxs-lookup"><span data-stu-id="0176a-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="0176a-121">In questo codice ci si sta registrando per una semplice notifica del modello che verrà inviata a tutte le piattaforme supportate dal server.</span><span class="sxs-lookup"><span data-stu-id="0176a-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="0176a-122">Per ulteriori informazioni sui modelli con Hub di notifica, vedere [Modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="0176a-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="0176a-123">Sovrascrivere quindi l'evento **DidReceivedRemoteNotification** :</span><span class="sxs-lookup"><span data-stu-id="0176a-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="0176a-124">L'app è ora aggiornata per il supporto delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="0176a-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="0176a-125"><a name="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="0176a-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="0176a-126">Scegliere **Run** (Esegui) per generare il progetto e avviare l'app in un dispositivo con iOS, quindi fare clic su **OK** per accettare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="0176a-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0176a-127">È necessario accettare le notifiche push in modo esplicito dall'app.</span><span class="sxs-lookup"><span data-stu-id="0176a-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="0176a-128">Questa richiesta viene visualizzata solo la prima volta che si esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="0176a-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="0176a-129">Nell'app digitare un'attività e fare clic sull'icona con il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="0176a-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="0176a-130">Verificare che venga ricevuta una notifica, quindi fare clic su **OK** per eliminarla.</span><span class="sxs-lookup"><span data-stu-id="0176a-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="0176a-131">Ripetere il passaggio 2 e chiudere immediatamente l'app, quindi verificare che venga visualizzata una notifica push.</span><span class="sxs-lookup"><span data-stu-id="0176a-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="0176a-132">L'esercitazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="0176a-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



