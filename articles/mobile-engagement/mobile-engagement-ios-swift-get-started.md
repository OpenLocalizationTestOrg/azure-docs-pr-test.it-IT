---
title: aaaGet avviato con Azure Mobile Engagement per iOS in Swift | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per App iOS.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="63a5b-103">Introduzione a Azure Mobile Engagement per app per iOS in Swift</span><span class="sxs-lookup"><span data-stu-id="63a5b-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="63a5b-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push applicazione notifiche di toosegmented utenti tooan iOS.</span><span class="sxs-lookup"><span data-stu-id="63a5b-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="63a5b-105">In questa esercitazione si creerà un'app per iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="63a5b-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="63a5b-106">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="63a5b-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="63a5b-107">XCode 8, che è possibile installare da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="63a5b-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="63a5b-108">Hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="63a5b-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="63a5b-109">Certificato per notifiche push (.p12) che è possibile ottenere nell'Apple Dev Center.</span><span class="sxs-lookup"><span data-stu-id="63a5b-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="63a5b-110">Questa esercitazione usa Swift versione 3.0.</span><span class="sxs-lookup"><span data-stu-id="63a5b-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="63a5b-111">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Mobile Engagement relative ad app per iOS.</span><span class="sxs-lookup"><span data-stu-id="63a5b-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="63a5b-112">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="63a5b-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="63a5b-113">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="63a5b-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="63a5b-114">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="63a5b-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="63a5b-115"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="63a5b-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="63a5b-116"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="63a5b-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="63a5b-117">Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="63a5b-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="63a5b-118">la documentazione completa integrazione Hello è reperibile in hello [integrazione SDK iOS di Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="63a5b-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="63a5b-119">Verrà creata un'applicazione di base con l'integrazione di XCode toodemonstrate hello:</span><span class="sxs-lookup"><span data-stu-id="63a5b-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="63a5b-120">Creare un nuovo progetto iOS</span><span class="sxs-lookup"><span data-stu-id="63a5b-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="63a5b-121">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="63a5b-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="63a5b-122">Scaricare hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="63a5b-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="63a5b-123">Estrarre hello. gz file tooa cartella computer</span><span class="sxs-lookup"><span data-stu-id="63a5b-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="63a5b-124">Fare clic con il pulsante destro progetto hello e selezionare "Aggiungi file troppo..."</span><span class="sxs-lookup"><span data-stu-id="63a5b-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="63a5b-125">Esplorazione delle cartelle toohello in cui è stato estratto hello SDK e seleziona hello `EngagementSDK` cartella, quindi premere OK.</span><span class="sxs-lookup"><span data-stu-id="63a5b-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="63a5b-126">Aprire hello `Build Phases` scheda in hello `Link Binary With Libraries` menu aggiungere il framework di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="63a5b-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="63a5b-127">Creare un Bridging intestazione toobe toouse in grado di hello dell'obiettivo C API SDK, scegliere File > Nuovo > File > iOS > origine > File di intestazione.</span><span class="sxs-lookup"><span data-stu-id="63a5b-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="63a5b-128">Modifica hello bridging intestazione file tooexpose Mobile Engagement Objective-C tooyour Swift codice, aggiungere hello importazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="63a5b-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="63a5b-129">In impostazioni di compilazione, assicurarsi che hello Objective-C Bridging intestazione impostazione nel compilatore Swift - la generazione del codice di compilazione include un'intestazione di toothis percorso.</span><span class="sxs-lookup"><span data-stu-id="63a5b-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="63a5b-130">Di seguito è riportato un esempio di percorso: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (a seconda del percorso hello)**</span><span class="sxs-lookup"><span data-stu-id="63a5b-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="63a5b-131">Tornare indietro toohello portale di Azure dell'app *le informazioni di connessione* pagina e copia hello stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="63a5b-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="63a5b-132">A questo punto incollare la stringa di connessione hello in hello `didFinishLaunchingWithOptions` delegato</span><span class="sxs-lookup"><span data-stu-id="63a5b-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="63a5b-133"><a id="monitor"></a>Abilitazione del monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="63a5b-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="63a5b-134">In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).</span><span class="sxs-lookup"><span data-stu-id="63a5b-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="63a5b-135">Aprire hello **ViewController.swift** file e sostituire la classe base hello di **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="63a5b-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="63a5b-136"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="63a5b-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="63a5b-137"><a id="integrate-push"></a>Abilitazione delle notifiche push e della messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="63a5b-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="63a5b-138">Engagement mobile permette di toointeract e con gli utenti con le notifiche Push e la messaggistica In-app nel contesto di hello delle campagne.</span><span class="sxs-lookup"><span data-stu-id="63a5b-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="63a5b-139">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="63a5b-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="63a5b-140">Hello nelle sezioni seguenti installerà il tooreceive app li.</span><span class="sxs-lookup"><span data-stu-id="63a5b-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="63a5b-141">Abilitare il tooreceive app invisibile all'utente le notifiche Push</span><span class="sxs-lookup"><span data-stu-id="63a5b-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="63a5b-142">Aggiungi progetto di hello Reach libreria tooyour</span><span class="sxs-lookup"><span data-stu-id="63a5b-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="63a5b-143">Fare clic con il pulsante destro del mouse sul progetto.</span><span class="sxs-lookup"><span data-stu-id="63a5b-143">Right click your project</span></span>
2. <span data-ttu-id="63a5b-144">Selezionare `Add file too...`.</span><span class="sxs-lookup"><span data-stu-id="63a5b-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="63a5b-145">Esplorazione delle cartelle toohello in cui è stato estratto hello SDK</span><span class="sxs-lookup"><span data-stu-id="63a5b-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="63a5b-146">Seleziona hello `EngagementReach` cartella</span><span class="sxs-lookup"><span data-stu-id="63a5b-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="63a5b-147">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="63a5b-147">Click Add</span></span>
6. <span data-ttu-id="63a5b-148">Modificare hello bridging intestazioni di copertura di Mobile Engagement Objective-C intestazione file tooexpose e aggiungere hello importazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="63a5b-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="63a5b-149">Modificare il delegato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="63a5b-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="63a5b-150">Inside hello `didFinishLaunchingWithOptions` : creare un modulo di copertura e passarlo tooyour linea Engagement inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="63a5b-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="63a5b-151">Abilitare il tooreceive app le notifiche Push APNS</span><span class="sxs-lookup"><span data-stu-id="63a5b-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="63a5b-152">Aggiungere i seguenti toohello riga hello `didFinishLaunchingWithOptions` metodo:</span><span class="sxs-lookup"><span data-stu-id="63a5b-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="63a5b-153">Aggiungere hello `didRegisterForRemoteNotificationsWithDeviceToken` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="63a5b-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="63a5b-154">Aggiungere hello `didReceiveRemoteNotification:fetchCompletionHandler:` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="63a5b-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
