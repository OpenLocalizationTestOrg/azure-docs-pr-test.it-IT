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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Usare gli hub di notifica toosend localizzata rilievo notizie tooiOS dispositivi
> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
In questo argomento illustra come hello toouse [modelli](notification-hubs-templates-cross-platform-push-messages.md) funzionalità di hub di notifica di Azure toobroadcast importanti notifiche di notizie che sono state localizzate per lingua e dispositivo. In questa esercitazione si comincia con app iOS hello creato in [toosend gli hub di notifica di utilizzare le ultime notizie]. Al termine, che si sarà in grado di tooregister per le categorie che si è interessati, specificare una lingua in cui le notifiche hello tooreceive e ricevere notifiche di push solo per le categorie di hello selezionata in tale lingua.

Esistono due parti toothis scenario:

* app per iOS consente client dispositivi toospecify una lingua e toodifferent toosubscribe importanti categorie di notizie.
* back-end Hello trasmette hello le notifiche, hello **tag** e **modello** funzionalità di Azure degli hub di notifica.

## <a name="prerequisites"></a>Prerequisiti
È necessario aver già completato hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione e dispone di codice hello disponibile, poiché in questa esercitazione si basa direttamente su tale codice.

Visual Studio 2012 o versione successiva è facoltativo.

## <a name="template-concepts"></a>Concetti relativi ai modelli
In [toosend gli hub di notifica di utilizzare le ultime notizie] è stata compilata un'applicazione che utilizzato **tag** toonotifications toosubscribe per le categorie di notizie diverso.
Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle. Ciò significa che contenuto hello di notifiche di hello stessi toobe localizzato e recapitato toohello correggere set di dispositivi.
In questo argomento viene illustrato come hello toouse **modello** funzionalità degli hub di notifica tooeasily recapitare localizzata notifiche sulle ultime notizie.

Nota: un modo toosend localizzata notifiche è toocreate più versioni di ogni tag. Ad esempio, toosupport in lingua inglese, francese e Mandarino, sarà necessaria e tre i tag diversi per notizie world: "world_en", "world_fr" e "world_ch". È quindi necessario toosend una versione localizzata di hello world news tooeach dei tag. In questo argomento vengono utilizzati modelli tooavoid hello aumentare del numero di tag e il requisito di hello di inviare più messaggi.

A un livello elevato, i modelli sono un modo toospecify come un dispositivo specifico deve ricevere una notifica. modello Hello specifica il formato di payload esatta hello riferendosi tooproperties che fanno parte di messaggio hello inviato dal back-end di app. In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Quindi si garantisce che i dispositivi è registrato con un modello che fa riferimento la proprietà corretta toohello. Ad esempio, un'app iOS che vuole tooregister per francese notizie registrerà seguente hello:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo [Modelli](notification-hubs-templates-cross-platform-push-messages.md).

## <a name="hello-app-user-interface"></a>interfaccia utente di app Hello
Si modificherà ora hello delle ultime notizie app creata nell'argomento hello [toosend gli hub di notifica di utilizzare le ultime notizie] toosend localizzata aggiornate utilizzando i modelli.

Nel MainStoryboard_iPhone.storyboard, aggiungere un controllo segmentata con linguaggi hello tre che saranno supportati: inglese, francese e mandarino.

![][13]

Quindi apportare tooadd che un IBOutlet il ViewController.h come illustrato di seguito:

![][14]

## <a name="building-hello-ios-app"></a>App iOS hello di compilazione
1. Aggiungere il Notification.h hello *retrieveLocale* (metodo) e la modifica dell'archivio di hello e sottoscrivere metodi, come illustrato di seguito:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    Nel Notification.m, modificare hello *storeCategoriesAndSubscribe* (metodo), aggiungendo il parametro delle impostazioni locali hello e archiviarla in hello impostazioni predefinite dell'utente:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Modificare quindi hello *sottoscrizione* internazionali di hello tooinclude metodo:
   
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
   
    Si noti come ora viene usato il metodo hello *registerTemplateWithDeviceToken*, invece di *registerNativeWithDeviceToken*. Quando si registra per un modello abbiamo modello json di tooprovide hello e anche un nome per il modello di hello (come l'app potrebbe essere necessario tooregister diversi modelli). Verificare tooregister che le categorie come tag, dal momento che toomake che tooreceive hello notifciations per le notizie.
   
    Aggiungere le impostazioni locali hello tooretrieve metodo rispetto alle impostazioni predefinite di hello utente:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Ora che la classe delle notifiche modificato, è necessario assicurarsi che il nostro ViewController rende toomake utilizzare hello UISegmentControl nuovo. Aggiungere hello seguente riga hello *viewDidLoad* metodo toomake che tooshow hello delle impostazioni locali attualmente selezionato:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Quindi, nel *sottoscrizione* (metodo), modificare la chiamata toohello *storeCategoriesAndSubscribe* toohello seguente:
   
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
3. Infine, si dispone di hello tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* metodo gli appdelegate. M, in modo che è possibile aggiornare correttamente la registrazione all'avvio dell'app. Modificare la chiamata toohello *sottoscrizione* metodo delle notifiche con seguenti hello:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(facoltativo) Invio di notifiche modello localizzate dall’app console .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(facoltativo) Inviare notifiche modello localizzato dal dispositivo hello
Se si non dispongono di accesso tooVisual Studio o desidera test toojust l'invio di notifiche di modello hello localizzata direttamente dall'app hello sul dispositivo hello.  È possibile semplice aggiungere toohello parametri di modello hello localizzata `SendNotificationRESTAPI` metodo è definito nell'esercitazione precedente hello.

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




## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei modelli, vedere:

* [Usare Hub di notifica per inviare notifiche agli utenti: ASP.NET]
* [Usare Hub di notifica per inviare notifiche agli utenti: Servizi mobili]

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
