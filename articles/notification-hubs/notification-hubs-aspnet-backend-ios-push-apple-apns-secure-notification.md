---
title: aaaAzure notifica hub Secure Push
description: Informazioni su come toosend sicura push notifiche tooan iOS app di Azure. Gli esempi di codice sono scritti in Objective-C e C#.
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="53748-104">Push sicuro degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="53748-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53748-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="53748-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="53748-106">iOS</span><span class="sxs-lookup"><span data-stu-id="53748-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="53748-107">Android</span><span class="sxs-lookup"><span data-stu-id="53748-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="53748-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="53748-108">Overview</span></span>
<span data-ttu-id="53748-109">Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura push di semplice utilizzo, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.</span><span class="sxs-lookup"><span data-stu-id="53748-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="53748-110">A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello.</span><span class="sxs-lookup"><span data-stu-id="53748-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="53748-111">In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra il dispositivo di client hello e back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="53748-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="53748-112">In generale, il flusso di hello è il seguente:</span><span class="sxs-lookup"><span data-stu-id="53748-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="53748-113">Hello app back-end:</span><span class="sxs-lookup"><span data-stu-id="53748-113">hello app back-end:</span></span>
   * <span data-ttu-id="53748-114">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="53748-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="53748-115">Invia ID hello del dispositivo notifica toohello (viene inviata alcuna informazione protetta).</span><span class="sxs-lookup"><span data-stu-id="53748-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="53748-116">Hello app sul dispositivo hello, quando si riceve notifica hello:</span><span class="sxs-lookup"><span data-stu-id="53748-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="53748-117">dispositivo di Hello contatta hello back-end richiedente hello sicura payload.</span><span class="sxs-lookup"><span data-stu-id="53748-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="53748-118">app Hello possono mostrare payload hello come una notifica sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="53748-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="53748-119">È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="53748-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="53748-120">In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token.</span><span class="sxs-lookup"><span data-stu-id="53748-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="53748-121">Se l'applicazione non archivia i token di autenticazione nel dispositivo hello, o se i token possono essere scaduti, hello app del dispositivo, al momento della ricezione di notifiche di hello deve essere visualizzato una generica notifica conferma hello utente toolaunch hello app.</span><span class="sxs-lookup"><span data-stu-id="53748-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="53748-122">app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="53748-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="53748-123">Questa esercitazione Secure Push viene illustrato come toosend una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="53748-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="53748-124">Hello esercitazione si basa sulle hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima.</span><span class="sxs-lookup"><span data-stu-id="53748-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="53748-125">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="53748-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="53748-126">Modificare il progetto di iOS hello</span><span class="sxs-lookup"><span data-stu-id="53748-126">Modify hello iOS project</span></span>
<span data-ttu-id="53748-127">Ora che è stato modificato il hello solo toosend back-end di app *id* di una notifica, aver toochange il toohandle app iOS di notifica e chiamare nuovamente il hello tooretrieve back-end protetta toobe messaggio visualizzato.</span><span class="sxs-lookup"><span data-stu-id="53748-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="53748-128">tooachieve questo obiettivo, abbiamo toowrite hello logica tooretrieve hello contenuto protetto da hello app back-end.</span><span class="sxs-lookup"><span data-stu-id="53748-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="53748-129">In **appdelegate. M**, verificare che i registri applicazione hello per le notifiche invisibile all'utente in modo elabora l'id di notifica hello inviato dal back-end hello.</span><span class="sxs-lookup"><span data-stu-id="53748-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="53748-130">Aggiungere hello **UIRemoteNotificationTypeNewsstandContentAvailability** opzione didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="53748-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="53748-131">Nel **appdelegate. M** aggiungere una sezione di implementazione nella parte superiore di hello con hello segue la dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="53748-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="53748-132">Successivamente, aggiungere in hello di sezione implementazione hello codice seguente, sostituendo i segnaposto hello `{back-end endpoint}` con endpoint hello per il back-end ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="53748-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. <span data-ttu-id="53748-133">È ora dispongono di una notifica in ingresso toohandle hello e utilizzare il metodo hello sopra tooretrieve hello contenuto toodisplay.</span><span class="sxs-lookup"><span data-stu-id="53748-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="53748-134">In primo luogo, abbiamo tooenable il toorun app iOS in background hello quando si riceve una notifica push.</span><span class="sxs-lookup"><span data-stu-id="53748-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="53748-135">In **XCode**, selezionare il progetto di app nel riquadro di sinistra hello, quindi scegliere la destinazione dell'applicazione principale in hello **destinazioni** sezione dal riquadro centrale hello.</span><span class="sxs-lookup"><span data-stu-id="53748-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="53748-136">Quindi fare clic sui **funzionalità** scheda nella parte superiore di hello del riquadro centrale e verificare hello **notifiche remoto** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="53748-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="53748-137">In **appdelegate. M** aggiungere hello seguendo le notifiche push toohandle metodo:</span><span class="sxs-lookup"><span data-stu-id="53748-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="53748-138">Si noti che è preferibile toohandle casi di hello di proprietà di intestazione di autenticazione mancante o il rifiuto da hello back-end.</span><span class="sxs-lookup"><span data-stu-id="53748-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="53748-139">gestione di specifica Hello di questi casi dipendono principalmente l'esperienza utente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="53748-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="53748-140">È una notifica con un messaggio generico per notifica effettivo di hello utente tooauthenticate tooretrieve hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="53748-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="53748-141">Eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="53748-141">Run hello Application</span></span>
<span data-ttu-id="53748-142">toorun applicazione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="53748-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="53748-143">In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).</span><span class="sxs-lookup"><span data-stu-id="53748-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="53748-144">Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="53748-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="53748-145">Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="53748-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="53748-146">Nell'app iOS hello dell'interfaccia utente, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="53748-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="53748-147">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="53748-147">Then click **Send push**.</span></span> <span data-ttu-id="53748-148">Dovrebbe essere hello protetto delle notifiche visualizzato nell'elenco il centro notifiche.</span><span class="sxs-lookup"><span data-stu-id="53748-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
