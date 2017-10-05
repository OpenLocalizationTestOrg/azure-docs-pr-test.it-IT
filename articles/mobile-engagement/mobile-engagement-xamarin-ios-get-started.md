---
title: Introduzione ad Azure Mobile Engagement per Xamarin.iOS
description: "Informazioni sull'uso di Azure Mobile Engagement con le funzionalità di analisi e notifiche push per le app Xamarin.iOS."
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
ms.openlocfilehash: 9938c3e994acf31244825b1afb347f8c9f90ebe3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="d97d6-103">Introduzione ad Azure Mobile Engagement per app Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d97d6-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d97d6-104">Questo argomento descrive come usare Azure Mobile Engagement per ottenere informazioni sull'uso dell'app e sull'invio di notifiche push a utenti segmentati di un'applicazione Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="d97d6-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="d97d6-105">In questa esercitazione si creerà un'app Xamarin.iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="d97d6-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="d97d6-106">Il servizio Azure Mobile Engagement verrà ritirato a marzo 2018 ed è attualmente disponibile solo per i clienti esistenti.</span><span class="sxs-lookup"><span data-stu-id="d97d6-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d97d6-107">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="d97d6-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d97d6-108">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="d97d6-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="d97d6-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="d97d6-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="d97d6-110">È anche possibile usare Visual Studio con Xamarin ma questa esercitazione usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="d97d6-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="d97d6-111">Per istruzioni di installazione, vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="d97d6-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="d97d6-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="d97d6-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="d97d6-113">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="d97d6-113">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d97d6-114">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d97d6-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d97d6-115">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="d97d6-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="d97d6-116"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="d97d6-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d97d6-117"><a id="connecting-app"></a>Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d97d6-117"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d97d6-118">Questa esercitazione presenta una "integrazione di base", che è la configurazione minima necessaria per raccogliere i dati e inviare una notifica push.</span><span class="sxs-lookup"><span data-stu-id="d97d6-118">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span>

<span data-ttu-id="d97d6-119">Verrà creata un'app di base con Xamarin per illustrare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="d97d6-119">We will create a basic app with Xamarin to demonstrate the integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="d97d6-120">Creare un nuovo progetto Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d97d6-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="d97d6-121">Avviare Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="d97d6-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="d97d6-122">Passare a **File** -> **New** (Nuovo)  -> **Solution** (Soluzione)</span><span class="sxs-lookup"><span data-stu-id="d97d6-122">Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="d97d6-123">Selezionare **Single View App** (App a visualizzazione singola), assicurarsi che il linguaggio selezionato sia **C#** e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d97d6-123">Select **Single View App**, make sure the selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="d97d6-124">Specificare le informazioni richieste nei campi **App Name** (Nome app) e **Organization Identifier** (Identificatore organizzazione) e quindi fare clic su **Next**(Avanti).</span><span class="sxs-lookup"><span data-stu-id="d97d6-124">Fill in the **App Name** and the **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="d97d6-125">Assicurarsi che il profilo di pubblicazione usato per la distribuzione dell'app iOS abbia un ID app che corrisponde esattamente all'identificatore del bundle riportato qui.</span><span class="sxs-lookup"><span data-stu-id="d97d6-125">Make sure that the publishing profile you eventually use to deploy your iOS app is using an App ID which matches exactly with the Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="d97d6-126">Aggiornare i campi **Project Name** (Nome progetto), **Solution Name** (Nome soluzione) e **Location** (Posizione), se necessario, e fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="d97d6-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="d97d6-127">Xamarin Studio creerà l'app demo in cui verrà integrato Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d97d6-127">Xamarin Studio will create the demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d97d6-128">Connettere l'app al back-end di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d97d6-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d97d6-129">Fare clic con il pulsante destro del mouse sulla cartella **Packages** (Pacchetti) nelle finestre della soluzione, quindi scegliere **Add Packages...** (Aggiungi pacchetti)</span><span class="sxs-lookup"><span data-stu-id="d97d6-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="d97d6-130">Cercare **Microsoft Azure Mobile Engagement Xamarin SDK** e aggiungerlo alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="d97d6-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="d97d6-131">Aprire **AppDelegate.cs** e aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="d97d6-131">Open **AppDelegate.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="d97d6-132">Nel metodo **FinishedLaunching** aggiungere quanto segue per inizializzare la connessione con il back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d97d6-132">In the **FinishedLaunching** method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="d97d6-133">Assicurarsi di aggiungere **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="d97d6-133">Make sure to add your **ConnectionString**.</span></span> <span data-ttu-id="d97d6-134">Questo codice usa anche un oggetto **NotificationIcon** fittizio che viene aggiunto da Mobile Engagement SDK e che è consigliabile sostituire.</span><span class="sxs-lookup"><span data-stu-id="d97d6-134">This code also uses a dummy **NotificationIcon** which is added by the Mobile Engagement SDK which you may want to replace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="d97d6-135"><a id="monitor"></a>Abilitazione del monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="d97d6-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="d97d6-136">Per iniziare a inviare dati e assicurarsi che gli utenti siano attivi, è necessario inviare almeno una schermata al back-end di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d97d6-136">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d97d6-137">Aprire **ViewController.cs** e aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="d97d6-137">Open **ViewController.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="d97d6-138">Sostituire la classe da cui `ViewController` eredita, modificando `UIViewController` in `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="d97d6-138">Replace the class from which `ViewController` inherits from `UIViewController` to `EngagementViewController`.</span></span> 

## <span data-ttu-id="d97d6-139"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="d97d6-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d97d6-140"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="d97d6-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d97d6-141">Mobile Engagement consente di interagire con gli utenti e coinvolgerli tramite notifiche push e messaggistica in-app nel contesto delle campagne.</span><span class="sxs-lookup"><span data-stu-id="d97d6-141">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="d97d6-142">Questo modulo è denominato REACH nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d97d6-142">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="d97d6-143">Le sezioni seguenti consentono di configurare l'app per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="d97d6-143">The following sections set up your app to receive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="d97d6-144">Modificare il delegato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d97d6-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="d97d6-145">Aprire **AppDelegate.cs** e aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="d97d6-145">Open the **AppDelegate.cs** and add the following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="d97d6-146">A questo punto aggiungere il codice seguente all'interno del metodo `FinishedLaunching` per eseguire la registrazione per i messaggi push, dopo `EngagementAgent.init(...)`.</span><span class="sxs-lookup"><span data-stu-id="d97d6-146">Now inside the `FinishedLaunching` method, add the following to register for push messages after `EngagementAgent.init(...)`</span></span>
   
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
3. <span data-ttu-id="d97d6-147">Infine, aggiornare o aggiungere i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d97d6-147">Finally - update or add the following methods:</span></span>
   
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
            Console.WriteLine("Failed to register for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="d97d6-148">Nel file **Info.plist** della soluzione verificare che l'**identificatore del bundle** corrisponda all'**ID app** incluso nel profilo di provisioning nel centro per sviluppatori Apple.</span><span class="sxs-lookup"><span data-stu-id="d97d6-148">In your **Info.plist** file in the solution, confirm that the **Bundle Identifier** matches with the **App ID** you have in your provisioning profile in the Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="d97d6-149">Nello stesso file **Info.plist** assicurarsi di aver selezionato **Enable Background Modes** (Abilita modalità in background) e **Remote Notifications** (Notifiche remote).</span><span class="sxs-lookup"><span data-stu-id="d97d6-149">In the same **Info.plist** file, make sure that you have checked the **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="d97d6-150">Eseguire l'app nel dispositivo associato a questo profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="d97d6-150">Run the app on the device you have associated with this publishing profile.</span></span> 

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
