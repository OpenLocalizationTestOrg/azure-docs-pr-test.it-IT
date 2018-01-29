---
title: Esercitazione sull'invio di ultime notizie mediante Hub di notifica - iOS
description: Informazioni su come usare Hub di notifica del bus di servizio di Azure per inviare notifiche relative alle ultime notizie a dispositivi iOS.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8aec171b46df3e0e7f2a2d3cc9d44084d064e6fd
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a>Uso di Hub di notifica per inviare le ultime notizie
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Panoramica
In questo argomento viene illustrato come utilizzare Hub di notifica di Azure per trasmettere le notifiche relative alle ultime notizie a un'app per iOS. Al termine dell'esercitazione, si sarà appreso a effettuare la registrazione alle categorie di ultime notizie desiderate e ricevere le notifiche push solo da tali categorie. Questo scenario è un modello comune per molte app nelle quali le notifiche devono essere inviate a gruppi di utenti che hanno dichiarato un interesse, ad esempio lettori di feed RSS, app per fan di musica e così via.

È possibile abilitare gli scenari di trasmissione includendo uno o più *tag* durante la creazione di una registrazione nell'hub di notifica. Quando le notifiche vengono inviate a un tag, tutti i dispositivi che hanno effettuato la registrazione al tag riceveranno la notifica. Poiché i tag sono costituiti da stringhe, non è necessario eseguire il provisioning anticipatamente. Per ulteriori informazioni sui tag, vedere [Espressioni di routing e tag  per hub di notifica](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Prerequisiti
Questo argomento si basa sull'app creata nell'esercitazione [Introduzione ad Hub di notifica][get-started]. Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].

## <a name="add-category-selection-to-the-app"></a>Aggiungere la selezione delle categorie all'app
Il primo passaggio prevede l'aggiunta degli elementi dell'interfaccia utente allo storyboard esistente per consentire all'utente di selezionare le categorie per le quali registrarsi. Le categorie selezionate da un utente sono archiviate nel dispositivo. All'avvio dell'app, viene creata una registrazione nell'hub di notifica con le categorie selezionate come tag.

1. Nel file MainStoryboard_iPhone.storyboard aggiungere i componenti seguenti dalla libreria di oggetti:
   
   * Un'etichetta con il testo "Breaking News".
   * Etichette con il testo relativo alle categorie "World", "Politics", "Business", "Technology", "Science", "Sports".
   * Sei opzioni, una per ogni categoria, impostare lo **stato** di ogni opzione su **Off** per impostazione predefinita.
   * Un pulsante con l'etichetta "Subscribe".
     
     L'aspetto dello storyboard dovrebbe essere simile al seguente:
     
     ![][3]
2. Nell'assistente dell'editor creare outlet per tutte le opzioni e denominarli "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch".
3. Creare un'azione per il pulsante denominata "subscribe". BreakingNewsViewController.h deve contenere quanto segue:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Creare una nuova **classe Cocoa Touch** chiamata `Notifications`. Copiare il seguente codice nella sezione dell'interfaccia del file Notifications.h:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Aggiungere la seguente direttiva import a Notifications.m:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Copiare il codice seguente nella sezione di implementazione del file Notifications.m:
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Questa classe usa l'archiviazione locale per archiviare le categorie di notizie che il dispositivo deve ricevere. Contiene inoltre un metodo per effettuare la registrazione per queste categorie tramite una registrazione [Modello](notification-hubs-templates-cross-platform-push-messages.md) .

1. Nel file Appdelegate.h, aggiungere un'istruzione import per Notifications.h e aggiungere una proprietà per un'istanza della classe delle notifiche:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Nel metodo **didFinishLaunchingWithOptions** in AppDelegate.m aggiungere il codice per inizializzare l'istanza di notifiche all'inizio del metodo.  
   
    `HUBNAME` e `HUBLISTENACCESS` (definiti in hubinfo.h) dovrebbero già avere i segnaposto `<hub name>` e `<connection string with listen access>` sostituiti con il nome dell'hub di notifica e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuta in precedenza.
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Poiché le credenziali che sono distribuite con un'app client in genere non sono sicure, distribuire solo la chiave per l'accesso Listen con l'app client. L'accesso Listen consente all'app di registrarsi per le notifiche ma le registrazioni esistenti non possono essere modificate e le notifiche non possono essere inviate. La chiave di accesso completa viene usata in un servizio back-end sicuro per l'invio delle notifiche e la modifica delle registrazioni esistenti.
   > 
   > 
3. Nel metodo **didRegisterForRemoteNotificationsWithDeviceToken** in AppDelegate.m sostituire il codice nel metodo con il codice seguente per passare il token del dispositivo alla classe delle notifiche. La classe delle notifiche eseguirà la registrazione per le notifiche con le categorie. Se l'utente modifica le selezioni delle categorie, chiamare il metodo `subscribeWithCategories` in risposta al pulsante **sottoscrizione** per aggiornarle.
   
   > [!NOTE]
   > Poiché il token di dispositivo assegnato dal servizio di notifica Push di Apple può cambiare in qualsiasi momento, è necessario ripetere la registrazione per le notifiche di frequente per evitare errori di notifica. In questo esempio viene effettuata la registrazione per le notifiche a ogni avvio dell'app. Per le app che vengono eseguite con una frequenza maggiore di una volta al giorno, è possibile ignorare la registrazione per conservare la larghezza di banda qualora sia trascorso meno di un giorno dalla registrazione precedente.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Si noti che a questo punto nel metodo **didRegisterForRemoteNotificationsWithDeviceToken** non dovrebbe essere presente altro codice.

1. I metodi seguenti devono essere già presenti in AppDelegate.m in seguito al completamento dell'esercitazione [Introduzione ad Hub di notifica][get-started].  In caso contrario, aggiungerli.
   
    -(void)MessageBox:(NSString *)title message:(NSString *)messageText  {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * (void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }
   
   This method handles notifications received when the app is running by displaying a simple **UIAlert**.
2. In ViewController.m, aggiungere un'istruzione import per AppDelegate.h e copiare il codice seguente nel metodo **subscribe** generato da XCode. Questo codice aggiornerà la registrazione della notifica per utilizzare i nuovi tag di categoria selezionati dall'utente nell'interfaccia utente.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Questo metodo crea un elenco **NSMutableArray** di categorie e usa la classe **Notifications** per archiviare l'elenco nell'archiviazione locale e registrare i tag corrispondenti nell'hub di notifica. Se le categorie vengono modificate, la registrazione viene ricreata con le nuove categorie.
3. In ViewController.m, aggiungere il codice seguente nel metodo **viewDidLoad** per impostare l'interfaccia utente in base alle categorie salvate in precedenza.

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



Ora l'app può archiviare un insieme di categorie nella risorsa di archiviazione locale del dispositivo utilizzata per la registrazione con l'hub di notifica ogni volta che l'app viene avviata.  L'utente può modificare la selezione di categorie al runtime e scegliere il metodo **subscribe** per aggiornare la registrazione per il dispositivo. Successivamente, si aggiornerà l'app per inviare le notifiche relative alle ultime notizie direttamente nell'applicazione stessa.

## <a name="optional-sending-tagged-notifications"></a>(facoltativo) Invio di notifiche con tag
Se non si ha accesso a Visual Studio, è possibile passare alla sezione successiva e inviare notifiche dall’app stessa. È anche possibile inviare la notifica modello appropriato di [portale di Azure] utilizzando la scheda di debug per l'hub di notifica. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a>(facoltativo) Inviare notifiche dal dispositivo
In genere le notifiche vengono inviate da un servizio di back-end ma per questa esercitazione è possibile inviare notifiche relative alle ultime notizie direttamente dall'applicazione. A tale scopo si aggiornerà il metodo `SendNotificationRESTAPI` definito nell'esercitazione [Introduzione ad Hub di notifica][get-started].

1. In ViewController.m aggiornare il metodo `SendNotificationRESTAPI` come segue in modo che accetti un parametro per il tag di categoria e invii la notifica [modello](notification-hubs-templates-cross-platform-push-messages.md) appropriata.
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. In ViewController.m aggiornare l’azione **Send Notification** nel modo illustrato nel codice seguente. In tal modo si inviano notifiche a più piattaforme utilizzando singolarmente ogni tag.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Ricompilare il progetto e assicurarsi che non siano presenti errori di compilazione.

## <a name="run-the-app-and-generate-notifications"></a>Esecuzione dell'app e generazione di notifiche
1. Premere il pulsante Esegui per compilare il progetto e avviare l'app. Selezionare alcune opzioni di notizie per cui eseguire la sottoscrizione e premere il pulsante **Subscribe** . Verrà visualizzata una finestra di dialogo che indica che è staa effettuata la sottoscrizione alle notifiche.
   
    ![][1]
   
    Quando si fa clic su **Subscribe**, l'app converte le categorie selezionate in tag e richiede una nuova registrazione del dispositivo per i tag selezionati dall'hub di notifica.
2. Immettere un messaggio da inviare come ultime notizie, quindi premere il pulsante **Send Notification** (Invia notifica). In alternativa, eseguire l'app console .NET per generare le notifiche.
   
    ![][2]
3. Ogni dispositivo iscritto alle notizie riceverà le notifiche relative alle ultime notizie appena inviate.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso a trasmettere le ultime novità per categoria. Per informazioni su altri scenari avanzati di Hub di notifica, provare a completare le seguenti esercitazioni:

* **[Usare Hub di notifica per la trasmissione di notizie localizzate]**
  
    Informazioni su come espandere l'app relativa alle ultime novità per abilitare l'invio di notifiche localizzate.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Usare Hub di notifica per la trasmissione di notizie localizzate]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[portale di Azure]: https://portal.azure.com
