---
title: Procedure di aggiornamento di Azure Mobile Engagement SDK per iOS | Microsoft Docs
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="6a792-103">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="6a792-103">Upgrade procedures</span></span>
<span data-ttu-id="6a792-104">Se nell'applicazione è già stata integrata una versione precedente dell'SDK, è necessario considerare i seguenti punti quando si aggiorna l'SDK.</span><span class="sxs-lookup"><span data-stu-id="6a792-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="6a792-105">Per ogni nuova versione dell'SDK è necessario innanzitutto sostituire (rimuovere e importare nuovamente in Xcode) le cartelle EngagementSDK ed EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="6a792-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="6a792-106">Dalla versione 3.0.0 alla 4.0.0</span><span class="sxs-lookup"><span data-stu-id="6a792-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="6a792-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="6a792-107">XCode 8</span></span>
<span data-ttu-id="6a792-108">XCode 8 è un componente obbligatorio a partire dalla versione 4.0.0 dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="6a792-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="6a792-109">Se si dipende davvero da XCode 7, è possibile usare [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="6a792-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="6a792-110">Esiste un bug noto nel modulo di copertura della versione precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono attivate.</span><span class="sxs-lookup"><span data-stu-id="6a792-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="6a792-111">Per risolvere il problema è necessario implementare l'API deprecata `application:didReceiveRemoteNotification:` nel delegato dell'app come segue:</span><span class="sxs-lookup"><span data-stu-id="6a792-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="6a792-112">**Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata.</span><span class="sxs-lookup"><span data-stu-id="6a792-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="6a792-113">È opportuno passare a XCode 8 il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="6a792-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="6a792-114">Framework di UserNotifications</span><span class="sxs-lookup"><span data-stu-id="6a792-114">UserNotifications framework</span></span>
<span data-ttu-id="6a792-115">È necessario aggiungere il framework di `UserNotifications` nelle fasi di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6a792-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="6a792-116">Nell'area di esplorazione dei progetti aprire il riquadro del progetto, quindi selezionare la destinazione corretta.</span><span class="sxs-lookup"><span data-stu-id="6a792-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="6a792-117">Aprire quindi la scheda **"Build phases"** e nel menu **"Link Binary With Libraries"** aggiungere il framework `UserNotifications.framework`, quindi impostare il link come `Optional`</span><span class="sxs-lookup"><span data-stu-id="6a792-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="6a792-118">Funzionalità di push dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6a792-118">Application push capability</span></span>
<span data-ttu-id="6a792-119">XCode 8 può ripristinare la funzionalità di push dell'app; controllarla attentamente nella scheda `capability` della finestra di destinazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="6a792-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="6a792-120">Aggiungere il nuovo codice di registrazione delle notifiche iOS 10</span><span class="sxs-lookup"><span data-stu-id="6a792-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="6a792-121">Il frammento di codice precedente per registrare l'app per le notifiche funziona ancora, ma usa API deprecate pur essendo eseguito in iOS 10.</span><span class="sxs-lookup"><span data-stu-id="6a792-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="6a792-122">Importare il framework `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="6a792-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="6a792-123">Nel metodo `application:didFinishLaunchingWithOptions` del delegato dell'applicazione sostituire:</span><span class="sxs-lookup"><span data-stu-id="6a792-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="6a792-124">con:</span><span class="sxs-lookup"><span data-stu-id="6a792-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="6a792-125">Risolvere i conflitti del delegato UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="6a792-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="6a792-126">*Se né l'applicazione né una delle librerie di terze parti implementa il valore `UNUserNotificationCenterDelegate`, è possibile ignorare questa parte.*</span><span class="sxs-lookup"><span data-stu-id="6a792-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="6a792-127">Un delegato `UNUserNotificationCenter` viene usato dall'SDK per monitorare il ciclo di vita delle notifiche di Engagement sui dispositivi che eseguono iOS 10 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6a792-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="6a792-128">L'SDK include un'implementazione specifica del protocollo `UNUserNotificationCenterDelegate`, ma può essere presente solo un delegato `UNUserNotificationCenter` per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a792-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="6a792-129">Qualsiasi altro delegato aggiunto all'oggetto `UNUserNotificationCenter` sarà in conflitto con l'oggetto Engagement.</span><span class="sxs-lookup"><span data-stu-id="6a792-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="6a792-130">Se l'SDK rileva il delegato dell'utente o di terze parti, non userà l'implementazione specifica per consentire di risolvere i conflitti.</span><span class="sxs-lookup"><span data-stu-id="6a792-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="6a792-131">Sarà necessario aggiungere la logica di Engagement al delegato per risolvere i conflitti.</span><span class="sxs-lookup"><span data-stu-id="6a792-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="6a792-132">A questo scopo è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="6a792-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="6a792-133">Proposta 1: inoltrare semplicemente le chiamate del delegato all'SDK:</span><span class="sxs-lookup"><span data-stu-id="6a792-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="6a792-134">Proposta 2: ereditare dalla classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="6a792-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="6a792-135">È possibile determinare se una notifica proviene o meno da Engagement passando il suo dizionario `userInfo` al metodo della classe dell'agente `isEngagementPushPayload:`.</span><span class="sxs-lookup"><span data-stu-id="6a792-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="6a792-136">Assicurarsi che il delegato dell'oggetto `UNUserNotificationCenter` sia impostato sul delegato nel metodo `application:willFinishLaunchingWithOptions:` o nel metodo `application:didFinishLaunchingWithOptions:` del delegato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a792-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="6a792-137">Se, ad esempio, è stata implementata la Proposta 1 precedente:</span><span class="sxs-lookup"><span data-stu-id="6a792-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="6a792-138">Dalla versione 2.0.0 alla 3.0.0</span><span class="sxs-lookup"><span data-stu-id="6a792-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="6a792-139">Eliminazione del supporto per iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="6a792-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="6a792-140">A partire da questa versione, la destinazione della distribuzione dell'applicazione deve essere almeno iOS 6.</span><span class="sxs-lookup"><span data-stu-id="6a792-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="6a792-141">Se si usa Reach nell'applicazione, è necessario aggiungere il valore `remote-notification` alla matrice `UIBackgroundModes` nel file Info.plist per ricevere notifiche remote.</span><span class="sxs-lookup"><span data-stu-id="6a792-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="6a792-142">Il metodo `application:didReceiveRemoteNotification:` deve essere sostituito da `application:didReceiveRemoteNotification:fetchCompletionHandler:` nel delegato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a792-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="6a792-143">"AEPushDelegate.h" è un'interfaccia deprecata ed è necessario rimuovere tutti i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="6a792-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="6a792-144">Ciò include la rimozione di `[[EngagementAgent shared] setPushDelegate:self]` e dei metodi delegati dal delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="6a792-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="6a792-145">Dalla versione 1.16.0 alla 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6a792-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="6a792-146">La sezione seguente illustra come eseguire la migrazione di un'integrazione dell'SDK dal servizio Capptain offerto da Capptain SAS a un'app basata su Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6a792-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="6a792-147">Se si esegue la migrazione da una versione precedente, visitare il sito Web di Capptain per eseguire prima la migrazione alla versione 1.16 e quindi applicare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="6a792-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a792-148">Capptain e Mobile Engagement sono servizi diversi e la procedura seguente illustra solo come eseguire la migrazione dell'app client.</span><span class="sxs-lookup"><span data-stu-id="6a792-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="6a792-149">La migrazione dell'SDK nell'app NON comporta la migrazione dei dati dai server di Capptain ai server di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6a792-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="6a792-150">Agente</span><span class="sxs-lookup"><span data-stu-id="6a792-150">Agent</span></span>
<span data-ttu-id="6a792-151">Il metodo `registerApp:` è stato sostituito dal nuovo metodo `init:`.</span><span class="sxs-lookup"><span data-stu-id="6a792-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="6a792-152">È necessario aggiornare il delegato dell'applicazione di conseguenza e usare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="6a792-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="6a792-153">Se il rilevamento di SmartAd è stato rimosso dall'SDK, è sufficiente rimuovere tutte le istanze della classe `AETrackModule` .</span><span class="sxs-lookup"><span data-stu-id="6a792-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="6a792-154">Modifiche del nome della classe</span><span class="sxs-lookup"><span data-stu-id="6a792-154">Class Name Changes</span></span>
<span data-ttu-id="6a792-155">Durante la procedura di rebranding, è necessario modificare alcuni nomi di classi/file.</span><span class="sxs-lookup"><span data-stu-id="6a792-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="6a792-156">A tutte le classi con prefisso "CP" viene assegnato quello "AE".</span><span class="sxs-lookup"><span data-stu-id="6a792-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="6a792-157">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6a792-157">Example:</span></span>

* <span data-ttu-id="6a792-158">`CPModule.h` viene rinominata come `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="6a792-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="6a792-159">Tutte le classi con prefisso "Capptain" vengono rinominate con il prefisso "Engagement".</span><span class="sxs-lookup"><span data-stu-id="6a792-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="6a792-160">Esempi:</span><span class="sxs-lookup"><span data-stu-id="6a792-160">Examples:</span></span>

* <span data-ttu-id="6a792-161">La classe `CapptainAgent` viene rinominata come `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="6a792-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="6a792-162">La classe `CapptainTableViewController` viene rinominata come `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="6a792-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="6a792-163">La classe `CapptainUtils` viene rinominata come `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="6a792-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="6a792-164">La classe `CapptainViewController` viene rinominata come `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="6a792-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

