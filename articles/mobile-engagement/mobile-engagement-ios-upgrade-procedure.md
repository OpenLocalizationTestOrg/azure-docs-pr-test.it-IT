---
title: aaaAzure iOS Mobile Engagement SDK aggiornare Procedure | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="d451e-103">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="d451e-103">Upgrade procedures</span></span>
<span data-ttu-id="d451e-104">Se è già stata integrata una versione precedente di Engagement all'interno dell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d451e-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="d451e-105">Per ogni nuova versione di hello SDK è necessario sostituire (rimuovere e importare di nuovo in xcode) hello cartelle EngagementSDK ed EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="d451e-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="d451e-106">Da 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="d451e-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="d451e-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="d451e-107">XCode 8</span></span>
<span data-ttu-id="d451e-108">XCode 8 è obbligatoria a partire dalla versione 4.0.0 di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d451e-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d451e-109">Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="d451e-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="d451e-110">È presente un bug noto nel modulo reach hello di questa versione di precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono prese in considerazione.</span><span class="sxs-lookup"><span data-stu-id="d451e-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="d451e-111">toofix questo sarà necessario tooimplement hello obsoleto API `application:didReceiveRemoteNotification:` nell'app, delegato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d451e-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="d451e-112">**Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata.</span><span class="sxs-lookup"><span data-stu-id="d451e-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="d451e-113">È necessario passare tooXCode 8 appena possibile.</span><span class="sxs-lookup"><span data-stu-id="d451e-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="d451e-114">Framework di UserNotifications</span><span class="sxs-lookup"><span data-stu-id="d451e-114">UserNotifications framework</span></span>
<span data-ttu-id="d451e-115">È necessario tooadd hello `UserNotifications` framework le fasi di compilazione.</span><span class="sxs-lookup"><span data-stu-id="d451e-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="d451e-116">in project explorer di hello, aprire il riquadro di progetto e selezionare la destinazione corretta hello.</span><span class="sxs-lookup"><span data-stu-id="d451e-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="d451e-117">Aprire quindi hello **"Fasi di compilazione"** scheda in hello **"Binario con librerie di collegamento"** menu, aggiungere framework `UserNotifications.framework` -collegamento hello set come`Optional`</span><span class="sxs-lookup"><span data-stu-id="d451e-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="d451e-118">Funzionalità di push dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d451e-118">Application push capability</span></span>
<span data-ttu-id="d451e-119">XCode 8 può reimpostare l'app push capacità,. ricontrollarlo in hello `capability` scheda la destinazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="d451e-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="d451e-120">Aggiungere hello nuovo iOS 10 registrazione Cod</span><span class="sxs-lookup"><span data-stu-id="d451e-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="d451e-121">Hello precedente codice frammento tooregister app hello toonotifications funziona comunque ma usa le API deprecate durante l'esecuzione in iOS 10.</span><span class="sxs-lookup"><span data-stu-id="d451e-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="d451e-122">Hello importazione `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="d451e-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="d451e-123">Nel metodo `application:didFinishLaunchingWithOptions` del delegato dell'applicazione sostituire:</span><span class="sxs-lookup"><span data-stu-id="d451e-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="d451e-124">con:</span><span class="sxs-lookup"><span data-stu-id="d451e-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="d451e-125">Risolvere i conflitti del delegato UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="d451e-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="d451e-126">*Se né l'applicazione né una delle librerie di terze parti implementa il valore `UNUserNotificationCenterDelegate`, è possibile ignorare questa parte.*</span><span class="sxs-lookup"><span data-stu-id="d451e-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="d451e-127">Oggetto `UNUserNotificationCenter` delegato viene utilizzato da hello SDK toomonitor hello del ciclo di vita di notifiche di Engagement nei dispositivi che eseguono in iOS, 10 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d451e-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="d451e-128">Hello SDK è un'implementazione personalizzata di hello `UNUserNotificationCenterDelegate` protocollo ma può essere presente solo una `UNUserNotificationCenter` delegato per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="d451e-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="d451e-129">Aggiunta di un altro delegato toohello `UNUserNotificationCenter` oggetto è in conflitto con hello Engagement uno.</span><span class="sxs-lookup"><span data-stu-id="d451e-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="d451e-130">Se hello SDK rileva delegato l'o eventuali altre terze parti non viene utilizzata la propria implementazione toogive è una possibilità tooresolve hello è in conflitto.</span><span class="sxs-lookup"><span data-stu-id="d451e-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="d451e-131">Sarà necessario tooadd hello Engagement logica tooyour proprietari di conflitti di hello tooresolve delegato in ordine.</span><span class="sxs-lookup"><span data-stu-id="d451e-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="d451e-132">Esistono due modi tooachieve questo.</span><span class="sxs-lookup"><span data-stu-id="d451e-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="d451e-133">Proposta di 1, semplicemente inoltrando il delegato chiama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="d451e-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="d451e-134">Proposta 2, ereditando dalla hello o `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="d451e-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="d451e-135">È possibile determinare se una notifica proviene da Engagement o meno, il passaggio relativo `userInfo` toohello dizionario agente `isEngagementPushPayload:` metodo della classe.</span><span class="sxs-lookup"><span data-stu-id="d451e-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="d451e-136">Verificare che tale hello `UNUserNotificationCenter` delegato dell'oggetto è impostato il delegato tooyour all'interno di uno hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` metodo del delegato di applicazione.</span><span class="sxs-lookup"><span data-stu-id="d451e-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="d451e-137">Ad esempio, se è implementato hello sopra proposta 1:</span><span class="sxs-lookup"><span data-stu-id="d451e-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="d451e-138">Da 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="d451e-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="d451e-139">Eliminazione del supporto per iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="d451e-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="d451e-140">A partire da questa destinazione di distribuzione hello versione dell'applicazione deve essere almeno iOS 6.</span><span class="sxs-lookup"><span data-stu-id="d451e-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="d451e-141">Se si utilizza portata dell'applicazione, è necessario aggiungere `remote-notification` toohello valore `UIBackgroundModes` matrice nel file Info. plist nelle notifiche di ordine tooreceive remoto.</span><span class="sxs-lookup"><span data-stu-id="d451e-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="d451e-142">metodo Hello `application:didReceiveRemoteNotification:` deve toobe sostituito `application:didReceiveRemoteNotification:fetchCompletionHandler:` nel delegato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d451e-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="d451e-143">"AEPushDelegate.h" è deprecata e interfaccia necessario tooremove tutti i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="d451e-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="d451e-144">Ciò include la rimozione `[[EngagementAgent shared] setPushDelegate:self]` e delegare i metodi dal delegato dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="d451e-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="d451e-145">Da 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="d451e-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="d451e-146">Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d451e-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="d451e-147">Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.16 quindi applicare hello seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="d451e-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d451e-148">Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client.</span><span class="sxs-lookup"><span data-stu-id="d451e-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="d451e-149">Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d451e-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="d451e-150">Agente</span><span class="sxs-lookup"><span data-stu-id="d451e-150">Agent</span></span>
<span data-ttu-id="d451e-151">metodo Hello `registerApp:` è stato sostituito dal nuovo metodo hello `init:`.</span><span class="sxs-lookup"><span data-stu-id="d451e-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="d451e-152">È necessario aggiornare il delegato dell'applicazione di conseguenza e usare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="d451e-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="d451e-153">Rilevamento SmartAd è stato rimosso dal SDK, è sufficiente tooremove tutte le istanze di `AETrackModule` classe</span><span class="sxs-lookup"><span data-stu-id="d451e-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="d451e-154">Modifiche del nome della classe</span><span class="sxs-lookup"><span data-stu-id="d451e-154">Class Name Changes</span></span>
<span data-ttu-id="d451e-155">Come parte di hello rebranding, esistono alcuni nomi di classe o il file che devono toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="d451e-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="d451e-156">A tutte le classi con prefisso "CP" viene assegnato quello "AE".</span><span class="sxs-lookup"><span data-stu-id="d451e-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="d451e-157">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d451e-157">Example:</span></span>

* <span data-ttu-id="d451e-158">`CPModule.h`è stato rinominato troppo`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="d451e-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="d451e-159">Tutte le classi con prefisso "Capptain" vengono rinominate con il prefisso "Engagement".</span><span class="sxs-lookup"><span data-stu-id="d451e-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="d451e-160">Esempi:</span><span class="sxs-lookup"><span data-stu-id="d451e-160">Examples:</span></span>

* <span data-ttu-id="d451e-161">classe Hello `CapptainAgent` viene rinominato troppo`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="d451e-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="d451e-162">classe Hello `CapptainTableViewController` viene rinominato troppo`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="d451e-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="d451e-163">classe Hello `CapptainUtils` viene rinominato troppo`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="d451e-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="d451e-164">classe Hello `CapptainViewController` viene rinominato troppo`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="d451e-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

