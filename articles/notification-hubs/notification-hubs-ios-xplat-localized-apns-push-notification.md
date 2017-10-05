---
title: Esercitazione sull'invio di ultime notizie localizzate per iOS mediante Hub di notifica
description: Informazioni su come usare Hub di notifica del bus di servizio di Azure per inviare notifiche relative alle ultime notizie localizzate (iOS).
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: fd2b7d9dfd4f432bbcbaa3ed76f8bec0b9677e17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="300a1-103">Uso di Hub di notifica per inviare le ultime notizie localizzate ai dispositivi iOS</span><span class="sxs-lookup"><span data-stu-id="300a1-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="300a1-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="300a1-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="300a1-105">iOS</span><span class="sxs-lookup"><span data-stu-id="300a1-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="300a1-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="300a1-106">Overview</span></span>
<span data-ttu-id="300a1-107">In questo argomento viene illustrato come utilizzare la funzionalità relativa ai [modelli](notification-hubs-templates-cross-platform-push-messages.md) di Hub di notifica di Azure per trasmettere notifiche relative alle ultime notizie localizzate in base alla lingua e al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="300a1-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="300a1-108">In questa esercitazione verrà utilizzata l'app di iOS creata in [Utilizzo di Hub di notifica per inviare le e ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="300a1-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="300a1-109">Al termine, sarà possibile effettuare la registrazione per le categorie di proprio interesse, specificare la lingua in cui ricevere le notifiche e ricevere solo notifiche push per le categorie selezionate nella lingua scelta.</span><span class="sxs-lookup"><span data-stu-id="300a1-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="300a1-110">Lo scenario è composto da due parti:</span><span class="sxs-lookup"><span data-stu-id="300a1-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="300a1-111">l'app per iOS consente ai dispositivi client di specificare una lingua e di sottoscrivere categorie diverse di ultime notizie;</span><span class="sxs-lookup"><span data-stu-id="300a1-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="300a1-112">il back-end trasmette le notifiche usando le funzionalità relative ai **tag** e ai **modelli** di Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="300a1-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="300a1-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="300a1-113">Prerequisites</span></span>
<span data-ttu-id="300a1-114">È necessario aver completato l'esercitazione [Utilizzo di Hub di notifica per inviare le e ultime notizie] e disporre del relativo codice, in quanto questa esercitazione è basata direttamente su tale codice.</span><span class="sxs-lookup"><span data-stu-id="300a1-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="300a1-115">Visual Studio 2012 o versione successiva è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="300a1-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="300a1-116">Concetti relativi ai modelli</span><span class="sxs-lookup"><span data-stu-id="300a1-116">Template concepts</span></span>
<span data-ttu-id="300a1-117">In [Utilizzo di Hub di notifica per inviare le e ultime notizie] è stata creata un'app che utilizza i **tag** per sottoscrivere le notifiche per diverse categorie di notizie.</span><span class="sxs-lookup"><span data-stu-id="300a1-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="300a1-118">Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle.</span><span class="sxs-lookup"><span data-stu-id="300a1-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="300a1-119">Questo significa che il contenuto delle notifiche deve essere localizzato e inviato al set di dispositivi corretto.</span><span class="sxs-lookup"><span data-stu-id="300a1-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="300a1-120">In questo argomento verrà illustrato come usare la funzionalità relativa ai **modelli** di Hub di notifica per inviare facilmente notifiche relative alle ultime notizie localizzate.</span><span class="sxs-lookup"><span data-stu-id="300a1-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="300a1-121">Nota: un possibile modo per inviare notifiche localizzate consiste nel creare più versioni di ogni tag.</span><span class="sxs-lookup"><span data-stu-id="300a1-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="300a1-122">Per supportare l'inglese, il francese e il mandarino, ad esempio, sono necessari tre tag diversi per le ultime notizie internazionali: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="300a1-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="300a1-123">È quindi necessario inviare una versione localizzata delle ultime notizie internazionali a ogni tag.</span><span class="sxs-lookup"><span data-stu-id="300a1-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="300a1-124">In questo argomento verranno utilizzati i modelli per evitare la proliferazione di tag e la necessità di inviare più messaggi.</span><span class="sxs-lookup"><span data-stu-id="300a1-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="300a1-125">In linea generale, i modelli consentono di specificare in che modo uno specifico dispositivo deve ricevere una notifica.</span><span class="sxs-lookup"><span data-stu-id="300a1-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="300a1-126">Il modello definisce lo specifico formato di payload da utilizzare, facendo riferimento alle proprietà del messaggio inviato dal back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="300a1-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="300a1-127">In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="300a1-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="300a1-128">Si procederà quindi a verificare che i dispositivi effettuino la registrazione con un modello che faccia riferimento alla proprietà corretta.</span><span class="sxs-lookup"><span data-stu-id="300a1-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="300a1-129">Per un'app per iOS che deve essere registrata per le notizie in francese, ad esempio, si effettuerà la registrazione nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="300a1-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="300a1-130">I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="300a1-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="300a1-131">Interfaccia utente dell'app</span><span class="sxs-lookup"><span data-stu-id="300a1-131">The app user interface</span></span>
<span data-ttu-id="300a1-132">L'app Breaking News creata nell'argomento [Utilizzo di Hub di notifica per inviare le e ultime notizie] verrà ora modificata in modo da inviare notizie localizzate mediante modelli.</span><span class="sxs-lookup"><span data-stu-id="300a1-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="300a1-133">In MainStoryboard_iPhone.storyboard aggiungere un controllo Segmented con le tre lingue che saranno supportate: inglese, francese e mandarino.</span><span class="sxs-lookup"><span data-stu-id="300a1-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="300a1-134">Assicurarsi quindi di aggiungere un elemento IBOutlet in ViewController.h come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="300a1-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="300a1-135">Compilazione dell'app per iOS</span><span class="sxs-lookup"><span data-stu-id="300a1-135">Building the iOS app</span></span>
1. <span data-ttu-id="300a1-136">In Notification.h aggiungere il metodo *retrieveLocale* , quindi modificare i metodi store e subscribe come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="300a1-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="300a1-137">In Notification.m modificare il metodo *storeCategoriesAndSubscribe* aggiungendo il parametro relativo alle impostazioni locali e archiviandolo nelle impostazioni predefinite dell'utente:</span><span class="sxs-lookup"><span data-stu-id="300a1-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="300a1-138">Modificare quindi il metodo *subscribe* in modo da includere le impostazioni locali:</span><span class="sxs-lookup"><span data-stu-id="300a1-138">Then modify the *subscribe* method to include the locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="300a1-139">Si noti che si sta ora usando il metodo *registerTemplateWithDeviceToken* anziché *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="300a1-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="300a1-140">Quando si effettua la registrazione per un modello, è necessario fornire il modello json e un nome per il modello. Questo perché l'app potrebbe richiedere la registrazione di modelli diversi.</span><span class="sxs-lookup"><span data-stu-id="300a1-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="300a1-141">Assicurarsi di registrare le categorie come tag, poiché è necessario ricevere notifiche per le notizie.</span><span class="sxs-lookup"><span data-stu-id="300a1-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="300a1-142">Aggiungere un metodo per recuperare le impostazioni locali dalle impostazioni predefinite dell'utente:</span><span class="sxs-lookup"><span data-stu-id="300a1-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="300a1-143">Ora che è stata modificata la classe Notifications, è necessario assicurarsi che ViewController utilizzi il nuovo UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="300a1-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="300a1-144">Aggiungere la riga seguente nel metodo *viewDidLoad* per assicurarsi che vengano mostrate le impostazioni locali attualmente selezionate:</span><span class="sxs-lookup"><span data-stu-id="300a1-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="300a1-145">Nel metodo *subscribe* modificare quindi la chiamata a *storeCategoriesAndSubscribe* come segue:</span><span class="sxs-lookup"><span data-stu-id="300a1-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="300a1-146">Aggiornare infine il metodo *didRegisterForRemoteNotificationsWithDeviceToken* in AppDelegate.m, affinché sia possibile aggiornare correttamente la registrazione all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="300a1-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="300a1-147">Modificare la chiamata al metodo *subscribe* delle notifiche come segue:</span><span class="sxs-lookup"><span data-stu-id="300a1-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="300a1-148">(facoltativo) Invio di notifiche modello localizzate dall’app console .NET.</span><span class="sxs-lookup"><span data-stu-id="300a1-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="300a1-149">(facoltativo) Invio di notifiche modello localizzato dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="300a1-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="300a1-150">Se non si ha accesso a Visual Studio o si desidera solo l'invio di notifiche modello localizzato direttamente dall'app sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="300a1-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="300a1-151">È possibile aggiungere semplicemente i parametri di modello localizzato per il metodo `SendNotificationRESTAPI` definito nell'esercitazione precedente.</span><span class="sxs-lookup"><span data-stu-id="300a1-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];

            [dataTask resume];
        }




## <a name="next-steps"></a><span data-ttu-id="300a1-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="300a1-152">Next Steps</span></span>
<span data-ttu-id="300a1-153">Per altre informazioni sull'uso dei modelli, vedere:</span><span class="sxs-lookup"><span data-stu-id="300a1-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="300a1-154">[Usare Hub di notifica per inviare notifiche agli utenti: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="300a1-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="300a1-155">[Usare Hub di notifica per inviare notifiche agli utenti: Servizi mobili]</span><span class="sxs-lookup"><span data-stu-id="300a1-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="300a1-156">[Utilizzo di Hub di notifica per inviare le e ultime notizie]: /manage/services/notification-hubs/breaking-news-ios</span><span class="sxs-lookup"><span data-stu-id="300a1-156">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
<span data-ttu-id="300a1-157">[Usare Hub di notifica per inviare notifiche agli utenti: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="300a1-157">[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="300a1-158">[Usare Hub di notifica per inviare notifiche agli utenti: Servizi mobili]: /manage/services/notification-hubs/notify-users</span><span class="sxs-lookup"><span data-stu-id="300a1-158">[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users</span></span>
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
