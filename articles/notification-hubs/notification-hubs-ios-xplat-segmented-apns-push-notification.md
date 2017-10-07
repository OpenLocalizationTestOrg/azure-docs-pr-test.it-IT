---
title: aaaNotification hub ultime notizie esercitazione - iOS
description: Informazioni su come toouse hub di notifica di Azure Service Bus toosend dispositivi tooiOS le notifiche di notizie di rilievo.
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
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilizzare gli hub di notifica toosend le ultime notizie
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Panoramica
In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooan app iOS. Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie. Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per ventole musica e così via.

Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello. Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello. Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza. Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Prerequisiti
In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica][get-started]. Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].

## <a name="add-category-selection-toohello-app"></a>Aggiungi categoria selezione toohello app
primo passaggio Hello è tooadd hello UI elementi tooyour storyboard esistente che consentono di hello utente tooselect categorie tooregister. categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello. Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.

1. Nel MainStoryboard_iPhone.storyboard aggiungere hello seguendo i componenti dalla libreria di oggetti hello:
   
   * Un'etichetta con il testo "Breaking News".
   * Etichette con il testo relativo alle categorie "World", "Politics", "Business", "Technology", "Science", "Sports".
   * Sei switch, uno per ogni categoria, impostare ogni switch **stato** toobe **Off** per impostazione predefinita.
   * Un pulsante con l'etichetta "Subscribe".
     
     L'aspetto dello storyboard dovrebbe essere simile al seguente:
     
     ![][3]
2. Nell'editor di Assistente hello, creare prese per tutte le opzioni di hello e chiamarli "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. Creare un'azione per il pulsante denominata "subscribe". Il ViewController.h deve contenere i seguenti hello:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Creare una nuova **classe Cocoa Touch** chiamata `Notifications`. Copiare hello seguente codice nella sezione dell'interfaccia hello del file hello Notifications.h:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Aggiungere hello tooNotifications.m direttiva import seguente:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Copiare hello seguente codice nella sezione di implementazione hello del file hello Notifications.m.
   
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



    Questa classe utilizza toostore di archiviazione locale e recuperare le categorie di hello delle news che riceverà questo dispositivo. Contiene inoltre un metodo tooregister per queste categorie utilizzando un [modello](notification-hubs-templates-cross-platform-push-messages.md) registrazione.

1. Nel file appdelegate. H hello, aggiungere un'istruzione di importazione per Notifications.h e aggiungere una proprietà di un'istanza della classe notifiche hello:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. In hello **didFinishLaunchingWithOptions** metodo appdelegate. M, aggiungere l'istanza di notifiche hello di tooinitialize di hello codice all'inizio di hello del metodo hello.  
   
    `HUBNAME`e `HUBLISTENACCESS` (definito in hubinfo.h) dovrebbe già disporre hello `<hub name>` e `<connection string with listen access>` segnaposto sostituiti con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature*ottenuti in precedenza
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client. Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche. chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.
   > 
   > 
3. In hello **didRegisterForRemoteNotificationsWithDeviceToken** metodo appdelegate. M, sostituire il codice di hello nel metodo hello con hello seguenti classi di codice toopass hello dispositivo toohello token notifiche. classe notifiche Hello eseguirà hello registrazione per le notifiche con categorie hello. Se l'utente di hello cambia le selezioni delle categorie, definiamo hello `subscribeWithCategories` metodo nella risposta toohello **sottoscrizione** tooupdate pulsante li.
   
   > [!NOTE]
   > Perché il token di dispositivo hello assegnato da hello Apple Push Notification Service (APNS) è possibile modificare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid. Questo esempio viene registrato per notifica ogni volta che viene avviata l'applicazione hello. Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Si noti che a questo punto non dovrebbe esistere alcun altro codice in hello **didRegisterForRemoteNotificationsWithDeviceToken** metodo.

1. Hello metodi seguenti devono essere già presenti in appdelegate. M completamento hello [iniziare con gli hub di notifica] [ get-started] esercitazione.  In caso contrario, aggiungerli.
   
    -(void) MessageBox:(NSString *) titolo messaggio:(NSString *) messageText {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification: (NSDictionary *) userInfo {NSLog (@"% @", userInfo);   [self MessageBox:@"Notification" messaggio: [valueForKey:@"alert [userInfo objectForKey:@"aps"]"]]; }
   
   Questo metodo gestisce le notifiche ricevute durante l'esecuzione mediante la visualizzazione di una semplice applicazione hello **UIAlert**.
2. In ViewController.m, aggiungere un'istruzione di importazione per appdelegate. H e copia hello seguente di codice in hello generato XCode **sottoscrizione** metodo. Questo codice aggiornerà hello notifica registrazione toouse hello nuova categoria tag hello utente ha scelto nell'interfaccia utente di hello.
   
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
   
   Questo metodo crea un **NSMutableArray** di categorie e utilizza hello **notifiche** toostore hello elenco classe hello locale archiviazione registri hello corrispondente tag e con l'hub di notifica. Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.
3. In ViewController.m, aggiungere hello seguente di codice hello **viewDidLoad** interfaccia utente di metodo tooset hello in base alle categorie di hello salvato in precedenza.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



app Hello ora possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che viene avviata l'applicazione hello.  utente di Hello può modificare hello selezione di categorie in fase di esecuzione e fare clic su hello **sottoscrizione** metodo tooupdate hello registrazione dispositivo hello. Aggiornare quindi hello toosend di app hello rilievo notifiche notizie direttamente in hello app stessa.

## <a name="optional-sending-tagged-notifications"></a>(facoltativo) Invio di notifiche con tag
Se non si dispone di accesso tooVisual Studio, è possibile ignorare la sezione successiva toohello e inviare notifiche da hello app stessa. È anche possibile inviare notifica di hello modello corretto da hello [portale di Azure classico] utilizzo scheda debug hello per l'hub di notifica. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(facoltativo) Inviare notifiche dal dispositivo hello
In genere le notifiche potrebbero essere inviate da un servizio back-end, tuttavia, è possibile inviare notifiche sulle ultime notizie direttamente dall'applicazione hello. toodo questo verrà aggiornato hello `SendNotificationRESTAPI` metodo che è stato definito in hello [iniziare con gli hub di notifica] [ get-started] esercitazione.

1. In hello aggiornamento ViewController.m `SendNotificationRESTAPI` metodo come segue in modo che accetta un parametro per il tag di categoria hello e le invia hello corretto [modello](notification-hubs-templates-cross-platform-push-messages.md) notifica.
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. In hello aggiornamento ViewController.m **invia una notifica** azione, come illustrato nel codice hello che segue. In modo che verranno inviate notifiche hello con ogni tag singolarmente e inviare toomultiple piattaforme.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Ricompilare il progetto e assicurarsi che non siano presenti errori di compilazione.

## <a name="run-hello-app-and-generate-notifications"></a>Eseguire app hello e generare le notifiche
1. Hello premere eseguire pulsante toobuild hello progetto e avviare l'applicazione hello. Selezionare alcune toosubscribe tooand di rilievo notizie opzioni e quindi premere hello **Sottoscrivi** pulsante. Verrà visualizzata una finestra di dialogo che indica le notifiche sono stati sottoscritti hello.
   
    ![][1]
   
    Quando si sceglie **Sottoscrivi**, hello app converte hello selezionata categorie nei tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato da hub di notifica hello.
2. Immettere un toobe messaggio inviato come notizie premere hello **invia una notifica** pulsante. In alternativa, eseguire le notifiche tramite toogenerate app hello .NET console.
   
    ![][2]
3. Ogni notizie toobreaking dispositivo sottoscritto riceverà notifiche sulle ultime hello notizie che appena stata inviata.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato appreso come toobroadcast le ultime notizie per categoria. Provare a eseguire una delle seguenti esercitazioni che evidenziano altri scenari avanzati di hub di notifica hello:

* **[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]**
  
    Informazioni su come hello tooexpand interrompere l'invio di notizie app tooenable localizzata notifiche.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[portale di Azure classico]: https://manage.windowsazure.com
