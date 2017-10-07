---
title: aaaGet avviato con Azure Mobile Engagement per iOS in Objective C | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le app iOS.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="e79ce-103">Introduzione a Azure Mobile Engagement per app per iOS in Objective C</span><span class="sxs-lookup"><span data-stu-id="e79ce-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e79ce-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push applicazione notifiche di toosegmented utenti tooan iOS.</span><span class="sxs-lookup"><span data-stu-id="e79ce-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="e79ce-105">In questa esercitazione si creerà un'app per iOS vuota che raccoglie dati di base e riceve notifiche push tramite Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="e79ce-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="e79ce-106">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e79ce-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e79ce-107">XCode 8, che è possibile installare da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="e79ce-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="e79ce-108">Hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="e79ce-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="e79ce-109">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Mobile Engagement relative ad app per iOS.</span><span class="sxs-lookup"><span data-stu-id="e79ce-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="e79ce-110">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="e79ce-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e79ce-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e79ce-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e79ce-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="e79ce-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="e79ce-113"><a id="setup-azme"></a>Configurare Mobile Engagement per l'app iOS</span><span class="sxs-lookup"><span data-stu-id="e79ce-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e79ce-114"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="e79ce-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e79ce-115">Questa esercitazione viene illustrato una "integrazione di base", che viene hello minima set di dati obbligatorio toocollect e invia una notifica push.</span><span class="sxs-lookup"><span data-stu-id="e79ce-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="e79ce-116">la documentazione completa integrazione Hello è reperibile in hello [integrazione SDK iOS di Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e79ce-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="e79ce-117">Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate XCode.</span><span class="sxs-lookup"><span data-stu-id="e79ce-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="e79ce-118">Creare un nuovo progetto iOS</span><span class="sxs-lookup"><span data-stu-id="e79ce-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="e79ce-119">La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="e79ce-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="e79ce-120">Scaricare hello [iOS Mobile Engagement SDK].</span><span class="sxs-lookup"><span data-stu-id="e79ce-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="e79ce-121">Estrarre hello. cartella di tooa GZ file nel computer.</span><span class="sxs-lookup"><span data-stu-id="e79ce-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="e79ce-122">Fare clic sul progetto hello e quindi selezionare **aggiungere file al**.</span><span class="sxs-lookup"><span data-stu-id="e79ce-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="e79ce-123">Passare toohello cartella in cui è stato estratto hello SDK, selezionare hello `EngagementSDK` cartella, fare clic su **opzioni** hello angolo inferiore sinistro e assicurarsi che tale casella di controllo di hello **copiare gli elementi, se necessario** e hello casella di controllo per la destinazione siano selezionate, quindi premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="e79ce-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="e79ce-124">Aprire hello **Build Phases** scheda hello in **binario con librerie di collegamento** menu, aggiungere il framework di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e79ce-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="e79ce-125">Tornare indietro toohello portale di Azure dell'app **le informazioni di connessione** pagina e copia la stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e79ce-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="e79ce-126">Hello successiva riga di codice aggiungere il **appdelegate. M** file.</span><span class="sxs-lookup"><span data-stu-id="e79ce-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="e79ce-127">A questo punto incollare la stringa di connessione hello in hello `didFinishLaunchingWithOptions` delegato.</span><span class="sxs-lookup"><span data-stu-id="e79ce-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="e79ce-128">`setTestLogEnabled`è un'istruzione facoltativa che consente di abilitare i registri SDK a tooidentify problemi.</span><span class="sxs-lookup"><span data-stu-id="e79ce-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="e79ce-129"><a id="monitor"></a>Abilitare il monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="e79ce-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="e79ce-130">In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).</span><span class="sxs-lookup"><span data-stu-id="e79ce-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e79ce-131">Aprire hello **ViewController.h** file e importare **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="e79ce-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="e79ce-132">Questo punto, sostituire superclassi hello di hello **ViewController** interfaccia da `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="e79ce-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="e79ce-133"><a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="e79ce-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e79ce-134"><a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app</span><span class="sxs-lookup"><span data-stu-id="e79ce-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e79ce-135">Engagement mobile permette di REACH e toointeract con gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app.</span><span class="sxs-lookup"><span data-stu-id="e79ce-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="e79ce-136">Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="e79ce-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="e79ce-137">Hello nelle sezioni seguenti impostarle backup tooreceive l'app.</span><span class="sxs-lookup"><span data-stu-id="e79ce-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="e79ce-138">Abilitare il tooreceive app invisibile all'utente le notifiche Push</span><span class="sxs-lookup"><span data-stu-id="e79ce-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="e79ce-139">Aggiungi progetto di hello Reach libreria tooyour</span><span class="sxs-lookup"><span data-stu-id="e79ce-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="e79ce-140">Fare clic con il pulsante destro sul progetto.</span><span class="sxs-lookup"><span data-stu-id="e79ce-140">Right-click your project.</span></span>
2. <span data-ttu-id="e79ce-141">Selezionare **Aggiungi file**.</span><span class="sxs-lookup"><span data-stu-id="e79ce-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="e79ce-142">Passare toohello cartella in cui è stato estratto hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e79ce-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="e79ce-143">Seleziona hello `EngagementReach` cartella.</span><span class="sxs-lookup"><span data-stu-id="e79ce-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="e79ce-144">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e79ce-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e79ce-145">Modificare il delegato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e79ce-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="e79ce-146">In **AppDeletegate.m** file, importare il modulo di copertura di Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="e79ce-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="e79ce-147">Inside hello `application:didFinishLaunchingWithOptions` (metodo), creare un modulo di Reach e passarlo tooyour linea Engagement inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="e79ce-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="e79ce-148">Abilitare il tooreceive app le notifiche Push APNS</span><span class="sxs-lookup"><span data-stu-id="e79ce-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="e79ce-149">Aggiungere i seguenti toohello riga hello `application:didFinishLaunchingWithOptions` metodo:</span><span class="sxs-lookup"><span data-stu-id="e79ce-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="e79ce-150">Aggiungere hello `application:didRegisterForRemoteNotificationsWithDeviceToken` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e79ce-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="e79ce-151">Aggiungere hello `didFailToRegisterForRemoteNotificationsWithError` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e79ce-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="e79ce-152">Aggiungere hello `didReceiveRemoteNotification:fetchCompletionHandler` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e79ce-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
