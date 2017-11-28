---
title: aaaNotification hub localizzata ultime notizie esercitazione per iOS
description: Informazioni su come toouse hub di notifica di Azure Service Bus toosend localizzata notifiche sulle ultime notizie (iOS).
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
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="03c9a-103">Usare gli hub di notifica toosend localizzata rilievo notizie tooiOS dispositivi</span><span class="sxs-lookup"><span data-stu-id="03c9a-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03c9a-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="03c9a-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="03c9a-105">iOS</span><span class="sxs-lookup"><span data-stu-id="03c9a-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="03c9a-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="03c9a-106">Overview</span></span>
<span data-ttu-id="03c9a-107">In questo argomento illustra come hello toouse [modelli](notification-hubs-templates-cross-platform-push-messages.md) funzionalità di hub di notifica di Azure toobroadcast importanti notifiche di notizie che sono state localizzate per lingua e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="03c9a-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="03c9a-108">In questa esercitazione si comincia con app iOS hello creato in [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="03c9a-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="03c9a-109">Al termine, che si sarà in grado di tooregister per le categorie che si è interessati, specificare una lingua in cui le notifiche hello tooreceive e ricevere notifiche di push solo per le categorie di hello selezionata in tale lingua.</span><span class="sxs-lookup"><span data-stu-id="03c9a-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="03c9a-110">Esistono due parti toothis scenario:</span><span class="sxs-lookup"><span data-stu-id="03c9a-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="03c9a-111">app per iOS consente client dispositivi toospecify una lingua e toodifferent toosubscribe importanti categorie di notizie.</span><span class="sxs-lookup"><span data-stu-id="03c9a-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="03c9a-112">back-end Hello trasmette hello le notifiche, hello **tag** e **modello** funzionalità di Azure degli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="03c9a-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03c9a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="03c9a-113">Prerequisites</span></span>
<span data-ttu-id="03c9a-114">È necessario aver già completato hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione e dispone di codice hello disponibile, poiché in questa esercitazione si basa direttamente su tale codice.</span><span class="sxs-lookup"><span data-stu-id="03c9a-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="03c9a-115">Visual Studio 2012 o versione successiva è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="03c9a-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="03c9a-116">Concetti relativi ai modelli</span><span class="sxs-lookup"><span data-stu-id="03c9a-116">Template concepts</span></span>
<span data-ttu-id="03c9a-117">In [toosend gli hub di notifica di utilizzare le ultime notizie] è stata compilata un'applicazione che utilizzato **tag** toonotifications toosubscribe per le categorie di notizie diverso.</span><span class="sxs-lookup"><span data-stu-id="03c9a-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="03c9a-118">Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle.</span><span class="sxs-lookup"><span data-stu-id="03c9a-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="03c9a-119">Ciò significa che contenuto hello di notifiche di hello stessi toobe localizzato e recapitato toohello correggere set di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="03c9a-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="03c9a-120">In questo argomento viene illustrato come hello toouse **modello** funzionalità degli hub di notifica tooeasily recapitare localizzata notifiche sulle ultime notizie.</span><span class="sxs-lookup"><span data-stu-id="03c9a-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="03c9a-121">Nota: un modo toosend localizzata notifiche è toocreate più versioni di ogni tag.</span><span class="sxs-lookup"><span data-stu-id="03c9a-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="03c9a-122">Ad esempio, toosupport in lingua inglese, francese e Mandarino, sarà necessaria e tre i tag diversi per notizie world: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="03c9a-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="03c9a-123">È quindi necessario toosend una versione localizzata di hello world news tooeach dei tag.</span><span class="sxs-lookup"><span data-stu-id="03c9a-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="03c9a-124">In questo argomento vengono utilizzati modelli tooavoid hello aumentare del numero di tag e il requisito di hello di inviare più messaggi.</span><span class="sxs-lookup"><span data-stu-id="03c9a-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="03c9a-125">A un livello elevato, i modelli sono un modo toospecify come un dispositivo specifico deve ricevere una notifica.</span><span class="sxs-lookup"><span data-stu-id="03c9a-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="03c9a-126">modello Hello specifica il formato di payload esatta hello riferendosi tooproperties che fanno parte di messaggio hello inviato dal back-end di app.</span><span class="sxs-lookup"><span data-stu-id="03c9a-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="03c9a-127">In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="03c9a-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="03c9a-128">Quindi si garantisce che i dispositivi è registrato con un modello che fa riferimento la proprietà corretta toohello.</span><span class="sxs-lookup"><span data-stu-id="03c9a-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="03c9a-129">Ad esempio, un'app iOS che vuole tooregister per francese notizie registrerà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="03c9a-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="03c9a-130">I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="03c9a-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="03c9a-131">interfaccia utente di app Hello</span><span class="sxs-lookup"><span data-stu-id="03c9a-131">hello app user interface</span></span>
<span data-ttu-id="03c9a-132">Si modificherà ora hello delle ultime notizie app creata nell'argomento hello [toosend gli hub di notifica di utilizzare le ultime notizie] toosend localizzata aggiornate utilizzando i modelli.</span><span class="sxs-lookup"><span data-stu-id="03c9a-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="03c9a-133">Nel MainStoryboard_iPhone.storyboard, aggiungere un controllo segmentata con linguaggi hello tre che saranno supportati: inglese, francese e mandarino.</span><span class="sxs-lookup"><span data-stu-id="03c9a-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="03c9a-134">Quindi apportare tooadd che un IBOutlet il ViewController.h come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="03c9a-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="03c9a-135">App iOS hello di compilazione</span><span class="sxs-lookup"><span data-stu-id="03c9a-135">Building hello iOS app</span></span>
1. <span data-ttu-id="03c9a-136">Aggiungere il Notification.h hello *retrieveLocale* (metodo) e la modifica dell'archivio di hello e sottoscrivere metodi, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="03c9a-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="03c9a-137">Nel Notification.m, modificare hello *storeCategoriesAndSubscribe* (metodo), aggiungendo il parametro delle impostazioni locali hello e archiviarla in hello impostazioni predefinite dell'utente:</span><span class="sxs-lookup"><span data-stu-id="03c9a-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="03c9a-138">Modificare quindi hello *sottoscrizione* internazionali di hello tooinclude metodo:</span><span class="sxs-lookup"><span data-stu-id="03c9a-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="03c9a-139">Si noti come ora viene usato il metodo hello *registerTemplateWithDeviceToken*, invece di *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="03c9a-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="03c9a-140">Quando si registra per un modello abbiamo modello json di tooprovide hello e anche un nome per il modello di hello (come l'app potrebbe essere necessario tooregister diversi modelli).</span><span class="sxs-lookup"><span data-stu-id="03c9a-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="03c9a-141">Verificare tooregister che le categorie come tag, dal momento che toomake che tooreceive hello notifciations per le notizie.</span><span class="sxs-lookup"><span data-stu-id="03c9a-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="03c9a-142">Aggiungere le impostazioni locali hello tooretrieve metodo rispetto alle impostazioni predefinite di hello utente:</span><span class="sxs-lookup"><span data-stu-id="03c9a-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="03c9a-143">Ora che la classe delle notifiche modificato, è necessario assicurarsi che il nostro ViewController rende toomake utilizzare hello UISegmentControl nuovo.</span><span class="sxs-lookup"><span data-stu-id="03c9a-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="03c9a-144">Aggiungere hello seguente riga hello *viewDidLoad* metodo toomake che tooshow hello delle impostazioni locali attualmente selezionato:</span><span class="sxs-lookup"><span data-stu-id="03c9a-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="03c9a-145">Quindi, nel *sottoscrizione* (metodo), modificare la chiamata toohello *storeCategoriesAndSubscribe* toohello seguente:</span><span class="sxs-lookup"><span data-stu-id="03c9a-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="03c9a-146">Infine, si dispone di hello tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* metodo gli appdelegate. M, in modo che è possibile aggiornare correttamente la registrazione all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="03c9a-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="03c9a-147">Modificare la chiamata toohello *sottoscrizione* metodo delle notifiche con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="03c9a-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="03c9a-148">(facoltativo) Invio di notifiche modello localizzate dall’app console .NET.</span><span class="sxs-lookup"><span data-stu-id="03c9a-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="03c9a-149">(facoltativo) Inviare notifiche modello localizzato dal dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="03c9a-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="03c9a-150">Se si non dispongono di accesso tooVisual Studio o desidera test toojust l'invio di notifiche di modello hello localizzata direttamente dall'app hello sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="03c9a-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="03c9a-151">È possibile semplice aggiungere toohello parametri di modello hello localizzata `SendNotificationRESTAPI` metodo è definito nell'esercitazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="03c9a-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
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

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
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




## <a name="next-steps"></a><span data-ttu-id="03c9a-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03c9a-152">Next Steps</span></span>
<span data-ttu-id="03c9a-153">Per altre informazioni sull'uso dei modelli, vedere:</span><span class="sxs-lookup"><span data-stu-id="03c9a-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="03c9a-154">[Usare Hub di notifica per inviare notifiche agli utenti: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="03c9a-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="03c9a-155">[Usare Hub di notifica per inviare notifiche agli utenti: Servizi mobili]</span><span class="sxs-lookup"><span data-stu-id="03c9a-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Usare Hub di notifica per inviare notifiche agli utenti: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Usare Hub di notifica per inviare notifiche agli utenti: Servizi mobili]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
