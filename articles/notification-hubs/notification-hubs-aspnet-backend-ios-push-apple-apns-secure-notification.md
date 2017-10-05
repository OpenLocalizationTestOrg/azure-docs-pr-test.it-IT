---
title: Push sicuro degli hub di notifica di Azure
description: Informazioni su come inviare notifiche push sicure a un'app per iOS da Azure. Gli esempi di codice sono scritti in Objective-C e C#.
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="a90a2-104">Push sicuro degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="a90a2-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a90a2-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a90a2-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="a90a2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a90a2-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="a90a2-107">Android</span><span class="sxs-lookup"><span data-stu-id="a90a2-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a90a2-108">Overview</span><span class="sxs-lookup"><span data-stu-id="a90a2-108">Overview</span></span>
<span data-ttu-id="a90a2-109">Il supporto per le notifiche push in Microsoft Azure consente di accedere a un'infrastruttura push di facile utilizzo, multipiattaforma con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="a90a2-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="a90a2-110">A causa di vincoli normativi o di sicurezza, un'applicazione potrebbe talvolta includere nella notifica informazioni che non è possibile trasmettere attraverso l'infrastruttura di notifiche push standard.</span><span class="sxs-lookup"><span data-stu-id="a90a2-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="a90a2-111">In questa esercitazione viene descritto come conseguire la stessa esperienza inviando informazioni sensibili attraverso una connessione autenticata e sicura tra il dispositivo client e il back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="a90a2-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="a90a2-112">A livello generale, il flusso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a90a2-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="a90a2-113">Il back-end dell'app:</span><span class="sxs-lookup"><span data-stu-id="a90a2-113">The app back-end:</span></span>
   * <span data-ttu-id="a90a2-114">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="a90a2-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="a90a2-115">Invia l'ID di questa notifica al dispositivo (non vengono inviate informazioni sicure).</span><span class="sxs-lookup"><span data-stu-id="a90a2-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="a90a2-116">L'app sul dispositivo, quando riceve la notifica:</span><span class="sxs-lookup"><span data-stu-id="a90a2-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="a90a2-117">Il dispositivo contatta il back-end richiedendo il payload sicuro.</span><span class="sxs-lookup"><span data-stu-id="a90a2-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="a90a2-118">L'app può indicare il payload come una notifica sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a90a2-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="a90a2-119">È importante notare che nel flusso precedente e in questa esercitazione si presuppone che il dispositivo archivi un token di autenticazione nella memoria locale, dopo l’accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a90a2-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="a90a2-120">Ciò garantisce un'esperienza completamente lineare, in quanto il dispositivo può recuperare il payload sicuro della notifica tramite questo token.</span><span class="sxs-lookup"><span data-stu-id="a90a2-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="a90a2-121">Se invece l'applicazione non archivia i token di autenticazione nel dispositivo o se questi hanno una scadenza, l'app per dispositivo, alla ricezione della notifica, dovrà visualizzare una notifica generica in cui si richiede all'utente di avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="a90a2-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="a90a2-122">L'app autentica quindi l'utente e mostra il payload di notifica.</span><span class="sxs-lookup"><span data-stu-id="a90a2-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="a90a2-123">In questa esercitazione sul push sicuro viene illustrato come inviare una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="a90a2-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="a90a2-124">Poiché i passaggi qui descritti si basano sull'esercitazione [Utilizzo di Hub di notifica per inviare notifiche agli utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) , sarà prima necessario completare i passaggi di quest'ultima.</span><span class="sxs-lookup"><span data-stu-id="a90a2-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="a90a2-125">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a90a2-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="a90a2-126">Modifica del progetto iOS</span><span class="sxs-lookup"><span data-stu-id="a90a2-126">Modify the iOS project</span></span>
<span data-ttu-id="a90a2-127">Ora che è stato modificato il back-end dell'app in modo da inviare solo l' *ID* di una notifica, è necessario modificare l'app per iOS in modo da gestire tale notifica e richiamare il back-end per recuperare il messaggio sicuro da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="a90a2-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="a90a2-128">Per conseguire questo obiettivo, è necessario scrivere la logica per recuperare il contenuto sicuro dal back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="a90a2-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="a90a2-129">In **AppDelegate.m**assicurarsi che l'app esegua la registrazione per le notifiche silenziose in modo da elaborare l'ID della notifica inviato dal back-end.</span><span class="sxs-lookup"><span data-stu-id="a90a2-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="a90a2-130">Aggiungere l'opzione **UIRemoteNotificationTypeNewsstandContentAvailability** in didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="a90a2-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="a90a2-131">In **AppDelegate.m** aggiungere una sezione di implementazione in alto con la dichiarazione seguente:</span><span class="sxs-lookup"><span data-stu-id="a90a2-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="a90a2-132">Aggiungere quindi la sezione di implementazione al seguente codice, sostituendo il segnaposto `{back-end endpoint}` con l'endpoint per il back-end ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="a90a2-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="a90a2-133">A questo punto, è necessario gestire la notifica in arrivo e usare il metodo sopra citato per recuperare il contenuto da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="a90a2-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="a90a2-134">In primo luogo, è necessario abilitare l'esecuzione dell'app per iOS in background quando riceve una notifica push.</span><span class="sxs-lookup"><span data-stu-id="a90a2-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="a90a2-135">In **XCode** selezionare il progetto dell'app nel riquadro a sinistra, fare clic sull'app di destinazione principale nella sezione **Targets** (Destinazioni) nel riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="a90a2-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="a90a2-136">Fare quindi clic sulla scheda **Capabilities** (Funzionalità) nella parte superiore del riquadro centrale e selezionare la casella di controllo **Remote Notifications** (Notifiche remote).</span><span class="sxs-lookup"><span data-stu-id="a90a2-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="a90a2-137">In **AppDelegate.m** aggiungere il metodo seguente per gestire le notifiche push:</span><span class="sxs-lookup"><span data-stu-id="a90a2-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="a90a2-138">Notare che è preferibile gestire i casi in cui manca la proprietà dell'intestazione di autenticazione o di rifiuto da parte del back-end.</span><span class="sxs-lookup"><span data-stu-id="a90a2-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="a90a2-139">La gestione specifica di questi casi dipende in larga misura dall'esperienza dell'utente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a90a2-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="a90a2-140">Una delle opzioni consiste nel visualizzare una notifica con un prompt generico affinché l'utente possa autenticarsi per recuperare la notifica effettiva.</span><span class="sxs-lookup"><span data-stu-id="a90a2-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="a90a2-141">Esecuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a90a2-141">Run the Application</span></span>
<span data-ttu-id="a90a2-142">Per eseguire l'applicazione, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a90a2-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="a90a2-143">In XCode eseguire l'app su un dispositivo iOS fisico (le notifiche push non funzioneranno nel simulatore).</span><span class="sxs-lookup"><span data-stu-id="a90a2-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="a90a2-144">Nell'interfaccia utente dell'app per iOS immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="a90a2-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="a90a2-145">Può trattarsi di qualsiasi stringa, ma devono avere lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="a90a2-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="a90a2-146">Nell'interfaccia utente dell'app per iOS fare clic su **Log in**.</span><span class="sxs-lookup"><span data-stu-id="a90a2-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="a90a2-147">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="a90a2-147">Then click **Send push**.</span></span> <span data-ttu-id="a90a2-148">La notifica sicura verrà visualizzata nel Notification Center.</span><span class="sxs-lookup"><span data-stu-id="a90a2-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
