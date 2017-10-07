---
title: aaaGet avviato con Azure Mobile Engagement per xamarin
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app xamarin. IOS.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="9e2bd-103">Introduzione ad Azure Mobile Engagement per app Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="9e2bd-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9e2bd-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche in un'applicazione di xamarin. IOS.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="9e2bd-105">In questa esercitazione si creerà un'app Xamarin.iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="9e2bd-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="9e2bd-106">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="9e2bd-107">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="9e2bd-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="9e2bd-108">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9e2bd-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="9e2bd-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="9e2bd-110">È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="9e2bd-111">Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e2bd-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="9e2bd-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="9e2bd-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="9e2bd-113">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9e2bd-114">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e2bd-115">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9e2bd-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="9e2bd-116"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="9e2bd-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9e2bd-117"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="9e2bd-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="9e2bd-118">Questa esercitazione viene illustrato un "integrazione di base" hello minimo imposta dati toocollect necessarie e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="9e2bd-119">Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Xamarin:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="9e2bd-120">Creare un nuovo progetto Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="9e2bd-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="9e2bd-121">Avviare Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="9e2bd-122">Andare troppo**File** -> **New** -> **soluzione**</span><span class="sxs-lookup"><span data-stu-id="9e2bd-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="9e2bd-123">Selezionare **singola vista App**, assicurarsi che sia il linguaggio selezionato hello **c#** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="9e2bd-124">Compilare hello **nome App** hello e **identificatore organizzazione** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="9e2bd-125">Verificare che tale hello è alla fine di utilizzare toodeploy che App iOS con un ID di App che corrisponde esattamente hello identificatore Bundle è qui profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="9e2bd-126">Hello aggiornamento **nome progetto**, **Nome soluzione** e **percorso** se necessario, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="9e2bd-127">Xamarin Studio creerà app demo hello in cui integrare Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="9e2bd-128">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="9e2bd-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="9e2bd-129">Fare clic con il pulsante destro hello **pacchetti** cartella windows soluzione hello e selezionare **Aggiungi pacchetti...**</span><span class="sxs-lookup"><span data-stu-id="9e2bd-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="9e2bd-130">Ricerca di hello **Xamarin SDK di Microsoft Azure Mobile Engagement** e aggiungerlo tooyour soluzione.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="9e2bd-131">Aprire **appdelegate. cs** e aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="9e2bd-132">In hello **FinishedLaunching** metodo, aggiungere hello seguente connessione di hello tooinitialize con back-end Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="9e2bd-133">Verificare che tooadd il **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="9e2bd-134">Questo codice usa anche un dummy **NotificationIcon** che viene aggiunto da Mobile Engagement SDK è hello tooreplace.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="9e2bd-135"><a id="monitor"></a>Abilitazione del monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9e2bd-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="9e2bd-136">In ordine toostart l'invio dei dati e garantire agli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello dello schermo.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="9e2bd-137">Aprire **ViewController.cs** e aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="9e2bd-138">Sostituire la classe hello da cui `ViewController` eredita da `UIViewController` troppo`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="9e2bd-139"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9e2bd-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9e2bd-140"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="9e2bd-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9e2bd-141">Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="9e2bd-142">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="9e2bd-143">Hello nelle sezioni seguenti impostarle backup tooreceive l'app.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="9e2bd-144">Modificare il delegato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9e2bd-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="9e2bd-145">Aprire hello **appdelegate. cs** e aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="9e2bd-146">A questo punto all'interno di hello `FinishedLaunching` metodo, aggiungere hello seguente tooregister per i messaggi push dopo`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="9e2bd-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="9e2bd-147">Infine, aggiornare o aggiungere hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="9e2bd-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="9e2bd-148">Nel **Info. plist** file nella soluzione hello, confermare che hello **identificatore Bundle** corrisponde alla hello **ID App** aver nel profilo di provisioning in hello Dev Apple Al centro.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="9e2bd-149">In hello stesso **Info. plist** , assicurarsi di aver selezionato hello **abilitare la modalità di Background** e **notifiche remoto**.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="9e2bd-150">Eseguire l'applicazione hello sul dispositivo hello che è stata associata a questo profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="9e2bd-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
