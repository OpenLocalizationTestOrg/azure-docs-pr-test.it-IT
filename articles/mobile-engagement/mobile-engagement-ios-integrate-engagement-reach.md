---
title: aaaAzure iOS Mobile Engagement SDK raggiungere integrazione | Documenti Microsoft
description: Ultimi aggiornamenti e procedure relativi a iOS SDK per Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="b9fed-103">La modalità di copertura di Engagement tooIntegrate in iOS</span><span class="sxs-lookup"><span data-stu-id="b9fed-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="b9fed-104">Attenersi alla procedura di integrazione hello descritta in hello [come tooIntegrate Engagement documento iOS](mobile-engagement-ios-integrate-engagement.md) prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="b9fed-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="b9fed-105">Questa documentazione richiede XCode 8.</span><span class="sxs-lookup"><span data-stu-id="b9fed-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="b9fed-106">Se effettivamente dipendono XCode 7, è possibile utilizzare hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="b9fed-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="b9fed-107">Esiste un bug noto nella versione precedente durante l'esecuzione su dispositivi iOS 10: le notifiche di sistema non vengono attivate.</span><span class="sxs-lookup"><span data-stu-id="b9fed-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="b9fed-108">toofix questo sarà necessario tooimplement hello obsoleto API `application:didReceiveRemoteNotification:` nell'app, delegato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b9fed-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="b9fed-109">**Questa soluzione non è consigliata** dal momento che tale comportamento può cambiare in qualsiasi aggiornamento della versione iOS imminente (anche minore), poiché questa API iOS è deprecata.</span><span class="sxs-lookup"><span data-stu-id="b9fed-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="b9fed-110">È necessario passare tooXCode 8 appena possibile.</span><span class="sxs-lookup"><span data-stu-id="b9fed-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="b9fed-111">Abilitare il tooreceive app invisibile all'utente le notifiche Push</span><span class="sxs-lookup"><span data-stu-id="b9fed-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="b9fed-112">Procedura di integrazione</span><span class="sxs-lookup"><span data-stu-id="b9fed-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="b9fed-113">Incorporare hello Engagement Reach SDK nel progetto iOS</span><span class="sxs-lookup"><span data-stu-id="b9fed-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="b9fed-114">Aggiungere hello Reach sdk nel progetto Xcode.</span><span class="sxs-lookup"><span data-stu-id="b9fed-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="b9fed-115">In Xcode, passare troppo**progetto \> aggiungere tooproject** scegliere hello `EngagementReach` cartella.</span><span class="sxs-lookup"><span data-stu-id="b9fed-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="b9fed-116">Modificare il delegato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b9fed-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="b9fed-117">Nella parte superiore di hello del file di implementazione, importare il modulo di copertura di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="b9fed-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="b9fed-118">Metodo `applicationDidFinishLaunching:` o `application:didFinishLaunchingWithOptions:`, creare un modulo di reach e passarlo tooyour linea Engagement inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="b9fed-119">Modificare **'icon.png'** stringa con il nome di immagine hello desiderato come l'icona di notifica.</span><span class="sxs-lookup"><span data-stu-id="b9fed-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="b9fed-120">Se si desidera che l'opzione hello toouse *valore badge aggiornamento* in campagne di copertura o eseguire il push nativo toouse \<formato/nativo di copertura di SaaS/API/campagna Push\> campagne, è necessario gestire modulo Reach hello Hello badge icona stesso (verrà cancellato automaticamente badge applicazione hello e reimposta anche il valore di hello archiviato da Engagement ogni volta che un'applicazione hello è avviato o foregrounded).</span><span class="sxs-lookup"><span data-stu-id="b9fed-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="b9fed-121">Questa operazione viene eseguita aggiungendo hello successiva riga dopo l'inizializzazione del modulo Reach:</span><span class="sxs-lookup"><span data-stu-id="b9fed-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="b9fed-122">Se si desidera toohandle Reach push di dati, è necessario consentire il delegato applicazione conforme toohello `AEReachDataPushDelegate` protocollo.</span><span class="sxs-lookup"><span data-stu-id="b9fed-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="b9fed-123">Aggiungere hello successiva riga dopo l'inizializzazione del modulo Reach:</span><span class="sxs-lookup"><span data-stu-id="b9fed-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="b9fed-124">È possibile implementare i metodi di hello `onDataPushStringReceived:` e `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` nel delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="b9fed-125">Categoria</span><span class="sxs-lookup"><span data-stu-id="b9fed-125">Category</span></span>
<span data-ttu-id="b9fed-126">il parametro di categoria Hello è facoltativo quando si crea una campagna Push di dati e consente che inserisce dati toofilter.</span><span class="sxs-lookup"><span data-stu-id="b9fed-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="b9fed-127">Ciò è utile se si desidera toopush diversi tipi di `Base64` tooidentify dati e si desidera tipo prima dell'analisi li.</span><span class="sxs-lookup"><span data-stu-id="b9fed-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="b9fed-128">**L'applicazione è ora visualizzato e pronto tooreceive raggiunga il contenuto.**</span><span class="sxs-lookup"><span data-stu-id="b9fed-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="b9fed-129">Come tooreceive sondaggi in qualsiasi momento e gli annunci</span><span class="sxs-lookup"><span data-stu-id="b9fed-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="b9fed-130">Engagement possibile inviare notifiche di raggiungere gli utenti finali tooyour in qualsiasi momento utilizzando hello Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="b9fed-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="b9fed-131">tooenable questa funzionalità, verranno tooprepare l'applicazione per le notifiche push di Apple e modificare il delegato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="b9fed-132">Preparare l'applicazione per le notifiche push Apple</span><span class="sxs-lookup"><span data-stu-id="b9fed-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="b9fed-133">Seguire la Guida hello: [come tooPrepare l'applicazione per le notifiche Push di Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="b9fed-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="b9fed-134">Aggiungere il codice client necessario hello</span><span class="sxs-lookup"><span data-stu-id="b9fed-134">Add hello necessary client code</span></span>
<span data-ttu-id="b9fed-135">*A questo punto l'applicazione deve disporre di un certificato Apple push registrato nel server front-end di Engagement hello.*</span><span class="sxs-lookup"><span data-stu-id="b9fed-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="b9fed-136">Se non si è già fatto, è necessario tooregister le notifiche push tooreceive di applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="b9fed-137">Hello importazione `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="b9fed-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="b9fed-138">Aggiungere hello seguente riga all'avvio dell'applicazione (in genere in `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="b9fed-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="b9fed-139">Quindi, è necessario tooprovide token del dispositivo hello tooEngagement restituiti dai server Apple.</span><span class="sxs-lookup"><span data-stu-id="b9fed-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="b9fed-140">Questa operazione viene eseguita nel metodo hello denominato `application:didRegisterForRemoteNotificationsWithDeviceToken:` nel delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="b9fed-141">Infine, è necessario tooinform hello Engagement SDK quando l'applicazione riceve una notifica remota.</span><span class="sxs-lookup"><span data-stu-id="b9fed-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="b9fed-142">toodo che, chiamare hello metodo `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` nel delegato dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="b9fed-143">Per impostazione predefinita, copertura di Engagement controlla completionHandler hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="b9fed-144">Se si desidera toomanually rispondono toohello `handler` blocco nel codice, è possibile passare null per hello `handler` argomento e il controllo completamento hello bloccare manualmente.</span><span class="sxs-lookup"><span data-stu-id="b9fed-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="b9fed-145">Vedere hello `UIBackgroundFetchResult` tipo per un elenco di valori possibili.</span><span class="sxs-lookup"><span data-stu-id="b9fed-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="b9fed-146">Esempio completo</span><span class="sxs-lookup"><span data-stu-id="b9fed-146">Full example</span></span>
<span data-ttu-id="b9fed-147">Di seguito, è riportato un esempio completo sull'integrazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="b9fed-148">Risolvere i conflitti del delegato UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="b9fed-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="b9fed-149">*Se né l'applicazione né una delle librerie di terze parti implementa il valore `UNUserNotificationCenterDelegate`, è possibile ignorare questa parte.*</span><span class="sxs-lookup"><span data-stu-id="b9fed-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="b9fed-150">Oggetto `UNUserNotificationCenter` delegato viene utilizzato da hello SDK toomonitor hello del ciclo di vita di notifiche di Engagement nei dispositivi che eseguono in iOS, 10 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b9fed-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="b9fed-151">Hello SDK è un'implementazione personalizzata di hello `UNUserNotificationCenterDelegate` protocollo ma può essere presente solo una `UNUserNotificationCenter` delegato per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="b9fed-152">Aggiunta di un altro delegato toohello `UNUserNotificationCenter` oggetto è in conflitto con hello Engagement uno.</span><span class="sxs-lookup"><span data-stu-id="b9fed-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="b9fed-153">Se hello SDK rileva delegato l'o eventuali altre terze parti non viene utilizzata la propria implementazione toogive è una possibilità tooresolve hello è in conflitto.</span><span class="sxs-lookup"><span data-stu-id="b9fed-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="b9fed-154">Sarà necessario tooadd hello Engagement logica tooyour proprietari di conflitti di hello tooresolve delegato in ordine.</span><span class="sxs-lookup"><span data-stu-id="b9fed-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="b9fed-155">Esistono due modi tooachieve questo.</span><span class="sxs-lookup"><span data-stu-id="b9fed-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="b9fed-156">Proposta di 1, semplicemente inoltrando il delegato chiama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="b9fed-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="b9fed-157">Proposta 2, ereditando dalla hello o `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="b9fed-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="b9fed-158">È possibile determinare se una notifica proviene da Engagement o meno, il passaggio relativo `userInfo` toohello dizionario agente `isEngagementPushPayload:` metodo della classe.</span><span class="sxs-lookup"><span data-stu-id="b9fed-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="b9fed-159">Verificare che tale hello `UNUserNotificationCenter` delegato dell'oggetto è impostato il delegato tooyour all'interno di uno hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` metodo del delegato di applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="b9fed-160">Ad esempio, se è implementato hello sopra proposta 1:</span><span class="sxs-lookup"><span data-stu-id="b9fed-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="b9fed-161">Come le campagne toocustomize</span><span class="sxs-lookup"><span data-stu-id="b9fed-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="b9fed-162">Notifiche</span><span class="sxs-lookup"><span data-stu-id="b9fed-162">Notifications</span></span>
<span data-ttu-id="b9fed-163">Esistono due tipi di notifiche: quelle di sistema e quelle in-app.</span><span class="sxs-lookup"><span data-stu-id="b9fed-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="b9fed-164">Le notifiche di sistema vengono gestite da iOS e non possono essere personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b9fed-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="b9fed-165">Le notifiche in-app sono costituite da una vista che viene aggiunto in modo dinamico toohello finestra dell'applicazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b9fed-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="b9fed-166">Si tratta di una sovrimpressione di notifica.</span><span class="sxs-lookup"><span data-stu-id="b9fed-166">This is called a notification overlay.</span></span> <span data-ttu-id="b9fed-167">Sovrapposizioni di notifica sono ideali per un'integrazione veloce perché non richiedono si toomodify qualsiasi visualizzazione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="b9fed-168">Layout</span><span class="sxs-lookup"><span data-stu-id="b9fed-168">Layout</span></span>
<span data-ttu-id="b9fed-169">aspetto di hello toomodify delle notifiche nell'applicazione, è sufficiente modificare file hello `AENotificationView.xib` tooyour deve, purché si mantenere i valori di tag hello e tipi di sottoviste esistente hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="b9fed-170">Per impostazione predefinita, nell'applicazione vengono visualizzate in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="b9fed-171">Se si preferisce toodisplay li nella parte superiore di hello della schermata, hello modifica fornita `AENotificationView.xib` e modificare hello `AutoSizing` proprietà di visualizzazione principale di hello in modo possono essere mantenuto nella parte superiore di hello della relativa superview.</span><span class="sxs-lookup"><span data-stu-id="b9fed-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="b9fed-172">Categorie</span><span class="sxs-lookup"><span data-stu-id="b9fed-172">Categories</span></span>
<span data-ttu-id="b9fed-173">Quando si modifica hello fornito layout, modificare aspetto hello di tutte le notifiche.</span><span class="sxs-lookup"><span data-stu-id="b9fed-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="b9fed-174">Le categorie consentono toodefine che vari destinazione Cerca (possibilmente comportamenti) per le notifiche.</span><span class="sxs-lookup"><span data-stu-id="b9fed-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="b9fed-175">Quando si crea una campagna Reach, è possibile specificare una categoria.</span><span class="sxs-lookup"><span data-stu-id="b9fed-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="b9fed-176">Tenere presente che le categorie consentono di personalizzare annunci e sondaggi, come descritto successivamente nel documento.</span><span class="sxs-lookup"><span data-stu-id="b9fed-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="b9fed-177">tooregister un gestore di categoria per le notifiche, è necessario tooadd viene inizializzata una chiamata una volta hello raggiungere modulo.</span><span class="sxs-lookup"><span data-stu-id="b9fed-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="b9fed-178">`myNotifier`deve essere un'istanza di un oggetto conforme al protocollo toohello `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="b9fed-179">È possibile implementare i metodi di protocollo hello personalmente o è possibile scegliere una classe esistente di hello tooreimplement `AEDefaultNotifier` che già esegue la maggior parte del lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="b9fed-180">Ad esempio, se si desidera visualizzazione di notifiche hello tooredefine per una categoria specifica, è possibile seguire questo esempio:</span><span class="sxs-lookup"><span data-stu-id="b9fed-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="b9fed-181">In questo semplice esempio di categoria si presuppone che nel pacchetto dell'applicazione sia presente un file denominato `MyNotificationView.xib` .</span><span class="sxs-lookup"><span data-stu-id="b9fed-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="b9fed-182">Se il metodo hello non è in grado di toofind corrispondente `.xib`, non verrà visualizzata la notifica hello ed Engagement creerà un messaggio nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="b9fed-183">Hello fornito nib file deve rispettare hello seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="b9fed-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="b9fed-184">Deve includere soltanto una visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="b9fed-184">It should only contain one view.</span></span>
* <span data-ttu-id="b9fed-185">Sottoviste devono essere di hello stesso tipi hello quelle all'interno di hello fornito nib file denominato`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="b9fed-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="b9fed-186">Sottoviste devono avere stesso tag come quelle all'interno di hello fornito nib file denominato hello hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="b9fed-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="b9fed-187">È sufficiente copiare i file nib hello fornito, denominato `AENotificationView.xib`e iniziare a utilizzarla da qui.</span><span class="sxs-lookup"><span data-stu-id="b9fed-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="b9fed-188">Ma fare attenzione, hello visualizzazione all'interno di questo file nib è associata la classe toohello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="b9fed-189">Questa classe ridefinito metodo hello `layoutSubViews` toomove e ridimensionare i sottoviste in base toocontext.</span><span class="sxs-lookup"><span data-stu-id="b9fed-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="b9fed-190">È possibile tooreplace con un `UIView` o una classe di visualizzazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b9fed-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="b9fed-191">Se è necessario personalizzare più approfondita delle notifiche (se si desidera ad esempio tooload nella visualizzazione direttamente dal codice hello), è consigliabile tootake un'occhiata hello fornita documentazione di classe e codice sorgente di `Protocol ReferencesDefaultNotifier` e `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="b9fed-192">Si noti che è possibile utilizzare hello stesso notifica per più categorie.</span><span class="sxs-lookup"><span data-stu-id="b9fed-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="b9fed-193">È possibile notifica predefinito anche ridefinito hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b9fed-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="b9fed-194">Gestione delle notifiche</span><span class="sxs-lookup"><span data-stu-id="b9fed-194">Notification handling</span></span>
<span data-ttu-id="b9fed-195">Quando si utilizza categoria predefinita hello, alcuni metodi del ciclo di vita vengono chiamati in hello `AEReachContent` tooreport stato campagna hello statistiche e l'aggiornamento dell'oggetto:</span><span class="sxs-lookup"><span data-stu-id="b9fed-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="b9fed-196">Verrà visualizzata la notifica hello nell'applicazione, hello `displayNotification` metodo viene chiamato (che indica le statistiche) da `AEReachModule` se `handleNotification:` restituisce `YES`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="b9fed-197">Se la notifica hello viene ignorata, hello `exitNotification` metodo viene chiamato, viene segnalata statistica e campagne successiva ora possono essere elaborate.</span><span class="sxs-lookup"><span data-stu-id="b9fed-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="b9fed-198">Se si fa clic notifica hello, `actionNotification` viene chiamato, viene restituita statistica e viene eseguita l'azione di hello associata.</span><span class="sxs-lookup"><span data-stu-id="b9fed-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="b9fed-199">Se l'implementazione di `AENotifier` bypass hello comportamento predefinito, è necessario toocall questi metodi del ciclo di vita da soli.</span><span class="sxs-lookup"><span data-stu-id="b9fed-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="b9fed-200">Hello seguono esempi vengono illustrati alcuni casi in cui viene ignorato il comportamento predefinito di hello:</span><span class="sxs-lookup"><span data-stu-id="b9fed-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="b9fed-201">Il metodo `AEDefaultNotifier` non è stato esteso, ad esempio la gestione delle categorie è stata implementata da zero.</span><span class="sxs-lookup"><span data-stu-id="b9fed-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="b9fed-202">Overrode `prepareNotificationView:forContent:`, toomap che almeno `onNotificationActioned` o `onNotificationExited` tooone dei controlli U.I.</span><span class="sxs-lookup"><span data-stu-id="b9fed-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="b9fed-203">Se `handleNotification:` genera un'eccezione, hello contenuto viene eliminato e `drop` viene chiamato, tale condizione viene segnalata nelle statistiche e campagne successiva ora possono essere elaborate.</span><span class="sxs-lookup"><span data-stu-id="b9fed-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="b9fed-204">Includere la notifica come parte di una visualizzazione esistente</span><span class="sxs-lookup"><span data-stu-id="b9fed-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="b9fed-205">Le sovrimpressioni rappresentano un metodo ottimale per eseguire integrazioni rapide; talvolta, però, non sono convenienti e possono produrre effetti collaterali indesiderati.</span><span class="sxs-lookup"><span data-stu-id="b9fed-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="b9fed-206">Se non si è soddisfatti del sistema di sovrapposizione hello in alcune visualizzazioni, è possibile personalizzarlo per queste viste.</span><span class="sxs-lookup"><span data-stu-id="b9fed-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="b9fed-207">È possibile decidere il layout di notifica tooinclude nelle visualizzazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="b9fed-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="b9fed-208">toodo in tal caso, è due stili di implementazione:</span><span class="sxs-lookup"><span data-stu-id="b9fed-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="b9fed-209">Aggiungi visualizzazione notifiche hello utilizzando Generatore di interfaccia</span><span class="sxs-lookup"><span data-stu-id="b9fed-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="b9fed-210">Aprire lo *strumento di creazione delle interfacce*</span><span class="sxs-lookup"><span data-stu-id="b9fed-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="b9fed-211">Inserire un 320 x 60 (o 768 x 60 se si utilizza iPad) `UIView` in cui si desidera hello notifica tooappear</span><span class="sxs-lookup"><span data-stu-id="b9fed-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="b9fed-212">Impostare il valore di Tag hello per questa vista troppo: **36822491**</span><span class="sxs-lookup"><span data-stu-id="b9fed-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="b9fed-213">Aggiungi visualizzazione notifiche hello a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="b9fed-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="b9fed-214">È sufficiente aggiungere codice dopo la visualizzazione è stata inizializzata hello:</span><span class="sxs-lookup"><span data-stu-id="b9fed-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="b9fed-215">La macro `NOTIFICATION_AREA_VIEW_TAG` è disponibile in `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="b9fed-216">notifica predefinito Hello rileva automaticamente che notifica il layout hello è incluso in questa vista e non verrà aggiunto un overlay relativo.</span><span class="sxs-lookup"><span data-stu-id="b9fed-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="b9fed-217">Annunci e sondaggi</span><span class="sxs-lookup"><span data-stu-id="b9fed-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="b9fed-218">Layout</span><span class="sxs-lookup"><span data-stu-id="b9fed-218">Layouts</span></span>
<span data-ttu-id="b9fed-219">È possibile modificare il file hello `AEDefaultAnnouncementView.xib` e `AEDefaultPollView.xib` come mantenere i valori di tag hello e tipi di sottoviste esistente hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="b9fed-220">Categorie</span><span class="sxs-lookup"><span data-stu-id="b9fed-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="b9fed-221">Layout alternativi</span><span class="sxs-lookup"><span data-stu-id="b9fed-221">Alternate layouts</span></span>
<span data-ttu-id="b9fed-222">Come le notifiche, la categoria della campagna hello può essere utilizzato toohave layout alternativi per gli annunci e viene eseguito il polling.</span><span class="sxs-lookup"><span data-stu-id="b9fed-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="b9fed-223">toocreate una categoria per un annuncio, è necessario estendere **AEAnnouncementViewController** ed effettuare la registrazione una volta inizializzata modulo reach hello:</span><span class="sxs-lookup"><span data-stu-id="b9fed-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="b9fed-224">Ogni volta che un utente farà clic su una notifica per un annuncio con la categoria di hello "my\_categoria", il controller di visualizzazione registrati (in questo caso `MyCustomAnnouncementViewController`) verrà inizializzato chiamando il metodo hello `initWithAnnouncement:` e Visualizza hello è aggiunta toohello finestra dell'applicazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b9fed-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="b9fed-225">Nell'implementazione di hello `AEAnnouncementViewController` classe si disporrà di proprietà hello tooread `announcement` tooinitialize i sottoviste.</span><span class="sxs-lookup"><span data-stu-id="b9fed-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="b9fed-226">Prendere in considerazione hello esempio riportato di seguito, in cui due etichette vengono inizializzate utilizzando `title` e `body` le proprietà di hello `AEReachAnnouncement` classe:</span><span class="sxs-lookup"><span data-stu-id="b9fed-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="b9fed-227">Se non si desidera tooload visualizzazioni da soli ma si desidera layout visualizzazione annuncio di tooreuse hello predefinito, puoi semplicemente far il controller di visualizzazione personalizzato estende la classe hello fornito `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="b9fed-228">In tal caso, duplicato file nib hello `AEDefaultAnnouncementView.xib` e rinominarlo in modo può essere caricato da controller di visualizzazione personalizzata (per un controller denominato `CustomAnnouncementViewController`, è necessario chiamare il file nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="b9fed-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="b9fed-229">categoria di tooreplace hello predefinita di annunci, semplicemente registrare il controller di visualizzazione personalizzata per categoria hello definita in `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="b9fed-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="b9fed-230">Esegue il polling può essere personalizzata hello allo stesso modo:</span><span class="sxs-lookup"><span data-stu-id="b9fed-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="b9fed-231">Questa volta, hello fornito `MyCustomPollViewController` deve estendere `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="b9fed-232">Oppure è possibile scegliere tooextend dal controller predefinito hello: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="b9fed-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9fed-233">Non dimenticare di toocall `action` (`submitAnswers:` per i controller di visualizzazione personalizzata di polling) o `exit` metodo prima di controller di hello visualizzazione viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="b9fed-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="b9fed-234">In caso contrario, le statistiche non verranno inviate (vale a dire non analitica nella campagna hello) e altre campagne importante successiva non verranno notificate fino a quando non viene riavviato il processo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="b9fed-235">Esempio di implementazione</span><span class="sxs-lookup"><span data-stu-id="b9fed-235">Implementation example</span></span>
<span data-ttu-id="b9fed-236">In questa implementazione visualizzazione personalizzata di annuncio hello viene caricato da un file esterno XI.</span><span class="sxs-lookup"><span data-stu-id="b9fed-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="b9fed-237">Ad esempio per la personalizzazione avanzata notifica, è consigliabile toolook al codice sorgente hello dell'implementazione standard di hello.</span><span class="sxs-lookup"><span data-stu-id="b9fed-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
