---
title: Panoramica di Azure Mobile Engagement SDK per iOS | Microsoft Docs
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="7cdd6-103">iOS SDK per Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7cdd6-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="7cdd6-104">Da qui, è possibile visualizzare tutti i dettagli su come integrare Azure Mobile Engagement in un'app per iOS.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="7cdd6-105">Se si vuole fare prima una prova, eseguire l' [esercitazione di 15 minuti](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7cdd6-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="7cdd6-106">Fare clic per visualizzare il [contenuto dell'SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="7cdd6-107">Procedure di integrazione</span><span class="sxs-lookup"><span data-stu-id="7cdd6-107">Integration procedures</span></span>
1. <span data-ttu-id="7cdd6-108">Iniziare da qui: [Come integrare Mobile Engagement in un'app per iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="7cdd6-109">Per le notifiche: [Come integrare il servizio di copertura (di notifica) in un'app per iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="7cdd6-110">Implementazione del piano di tag: [Come usare l'API per l'assegnazione di tag avanzata di Mobile Engagement in un'app per iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="7cdd6-111">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="7cdd6-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="7cdd6-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="7cdd6-113">Risolto il problema delle notifiche cancellate in background.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="7cdd6-114">Risolto il problema degli avvisi in XCode 9 sulle API non chiamate nella coda principale.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="7cdd6-115">Risolto un problema di memoria nei poll di copertura.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="7cdd6-116">Eliminazione del supporto per iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="7cdd6-117">A partire da questa versione, la destinazione della distribuzione dell'applicazione deve essere almeno iOS 7.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="7cdd6-118">Per le versioni precedenti, vedere le [note sulla versione complete](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="7cdd6-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="7cdd6-119">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="7cdd6-119">Upgrade procedures</span></span>
<span data-ttu-id="7cdd6-120">Se nell'applicazione è già stata integrata una versione precedente dell'SDK, è necessario considerare i seguenti punti quando si aggiorna l'SDK.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="7cdd6-121">Se non sono state applicate alcune versioni dell'SDK, potrebbe essere necessario eseguire più procedure. Vedere [Procedure di aggiornamento](mobile-engagement-ios-upgrade-procedure.md) per informazioni complete.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="7cdd6-122">Per ogni nuova versione dell'SDK è necessario innanzitutto sostituire (rimuovere e importare nuovamente in Xcode) le cartelle EngagementSDK ed EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="7cdd6-123">Dalla versione 3.0.0 alla 4.0.0</span><span class="sxs-lookup"><span data-stu-id="7cdd6-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="7cdd6-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="7cdd6-124">XCode 8</span></span>
<span data-ttu-id="7cdd6-125">XCode 8 è un componente obbligatorio a partire dalla versione 4.0.0 dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7cdd6-126">Se si dipende davvero da XCode 7, è possibile usare [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="7cdd6-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="7cdd6-127">Esiste un bug noto nel modulo di copertura della versione precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono attivate.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="7cdd6-128">Per risolvere il problema è necessario implementare l'API deprecata `application:didReceiveRemoteNotification:` nel delegato dell'app come segue:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="7cdd6-129">**Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="7cdd6-130">È opportuno passare a XCode 8 il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="7cdd6-131">Framework di UserNotifications</span><span class="sxs-lookup"><span data-stu-id="7cdd6-131">UserNotifications framework</span></span>
<span data-ttu-id="7cdd6-132">È necessario aggiungere il framework di `UserNotifications` nelle fasi di compilazione.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="7cdd6-133">Nell'area di esplorazione dei progetti aprire il riquadro del progetto, quindi selezionare la destinazione corretta.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="7cdd6-134">Aprire quindi la scheda **"Build phases"** e nel menu **"Link Binary With Libraries"** aggiungere il framework `UserNotifications.framework`, quindi impostare il link come `Optional`</span><span class="sxs-lookup"><span data-stu-id="7cdd6-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="7cdd6-135">Funzionalità di push dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7cdd6-135">Application push capability</span></span>
<span data-ttu-id="7cdd6-136">XCode 8 può ripristinare la funzionalità di push dell'app; controllarla attentamente nella scheda `capability` della finestra di destinazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="7cdd6-137">Aggiungere il nuovo codice di registrazione delle notifiche iOS 10</span><span class="sxs-lookup"><span data-stu-id="7cdd6-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="7cdd6-138">Il frammento di codice precedente per registrare l'app per le notifiche funziona ancora, ma usa API deprecate pur essendo eseguito in iOS 10.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="7cdd6-139">Importare il framework `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="7cdd6-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="7cdd6-140">Nel metodo `application:didFinishLaunchingWithOptions` del delegato dell'applicazione sostituire:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="7cdd6-141">con:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="7cdd6-142">Risolvere i conflitti del delegato UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="7cdd6-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="7cdd6-143">*Se né l'applicazione né una delle librerie di terze parti implementa il valore `UNUserNotificationCenterDelegate`, è possibile ignorare questa parte.*</span><span class="sxs-lookup"><span data-stu-id="7cdd6-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="7cdd6-144">Un delegato `UNUserNotificationCenter` viene usato dall'SDK per monitorare il ciclo di vita delle notifiche di Engagement sui dispositivi che eseguono iOS 10 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="7cdd6-145">L'SDK include un'implementazione specifica del protocollo `UNUserNotificationCenterDelegate`, ma può essere presente solo un delegato `UNUserNotificationCenter` per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="7cdd6-146">Qualsiasi altro delegato aggiunto all'oggetto `UNUserNotificationCenter` sarà in conflitto con l'oggetto Engagement.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="7cdd6-147">Se l'SDK rileva il delegato dell'utente o di terze parti, non userà l'implementazione specifica per consentire di risolvere i conflitti.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="7cdd6-148">Sarà necessario aggiungere la logica di Engagement al delegato per risolvere i conflitti.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="7cdd6-149">A questo scopo è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="7cdd6-150">Proposta 1: inoltrare semplicemente le chiamate del delegato all'SDK:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="7cdd6-151">Proposta 2: ereditare dalla classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="7cdd6-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="7cdd6-152">È possibile determinare se una notifica proviene o meno da Engagement passando il suo dizionario `userInfo` al metodo della classe dell'agente `isEngagementPushPayload:`.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="7cdd6-153">Assicurarsi che il delegato dell'oggetto `UNUserNotificationCenter` sia impostato sul delegato nel metodo `application:willFinishLaunchingWithOptions:` o nel metodo `application:didFinishLaunchingWithOptions:` del delegato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7cdd6-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="7cdd6-154">Se, ad esempio, è stata implementata la Proposta 1 precedente:</span><span class="sxs-lookup"><span data-stu-id="7cdd6-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
