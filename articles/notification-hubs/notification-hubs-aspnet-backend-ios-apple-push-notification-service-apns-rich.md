---
title: aaaAzure notifica hub Rich Push
description: Informazioni su come rich toosend push notifiche tooan iOS app di Azure. Gli esempi di codice sono scritti in Objective-C e C#.
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Push avanzato degli hub di notifica di Azure
## <a name="overview"></a>Panoramica
In ordine tooengage gli utenti con contenuto RTF immediata, un'applicazione può essere toopush oltre a testo normale. Queste notifiche promuovono le interazioni con l'utente e presentano contenuti come URL, immagini/buoni e altro ancora. In questa esercitazione si basa su hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) argomento e Mostra come toosend push delle notifiche che incorporano payload (ad esempio, l'immagine).

Questa esercitazione è compatibile con iOS 7 e 8.

  ![][IOS1]

In generale:

1. back-end app Hello:
   * Archivi hello payload avanzati (in questo caso, l'immagine) in archiviazione di database o locale hello back-end
   * Invia l'ID del dispositivo toohello notifica avanzata
2. App sul dispositivo hello:
   * Contatti hello back-end la richiesta di payload avanzati di hello con ID hello riceve
   * Invia notifiche agli utenti sul dispositivo hello quando il recupero dei dati è stata completata e viene illustrato il payload di hello immediatamente quando gli utenti toccano toolearn più

## <a name="webapi-project"></a>Progetto WebAPI
1. In Visual Studio, aprire hello **AppBackend** progetto creato in hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione.
2. Ottenere un'immagine che si desidera che gli utenti toonotify con e inserirlo in un **img** cartella nella directory del progetto.
3. Fare clic su **Mostra tutti i file** in hello Esplora soluzioni e fare clic sulla cartella di hello, troppo**Includi nel progetto**.
4. Con l'immagine di hello selezionata, modificare l'azione di compilazione nella finestra Proprietà troppo**risorsa incorporata**.
   
    ![][IOS2]
5. In **Notifications.cs**, aggiungere hello seguente istruzione using:
   
        using System.Reflection;
6. Hello aggiornamento intero **notifiche** classe con hello seguente codice. Essere tooreplace che segnaposto hello con le credenziali di hub di notifica e un nome di file di immagine.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (facoltativo) Fare riferimento troppo[come tooembed e alle risorse utilizzando Visual c#](http://support.microsoft.com/kb/319292) per ulteriori informazioni su come tooadd e ottenere le risorse del progetto.
   > 
   > 
7. In **NotificationsController.cs**, ridefinire **NotificationsController** con hello frammenti di codice seguente. Si invia un toodevice id la notifica iniziale RTF invisibile all'utente e consente il recupero del client dell'immagine:
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Ora si distribuirà nuovamente questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi. Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.
9. Selezionare un sito Web Azure come destinazione di pubblicazione. Accedere con l'account Azure e selezionare un sito Web nuovo o esistente e prendere nota di hello **URL di destinazione** proprietà hello **connessione** scheda. Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione. Fare clic su **Pubblica**.

## <a name="modify-hello-ios-project"></a>Modificare il progetto di iOS hello
Ora che sono state modificate le hello solo di back-end toosend app *id* di una notifica, si cambia il toohandle app iOS che l'id e recuperare dettagliata del messaggio hello dal back-end.

1. Aprire il progetto iOS e abilitare le notifiche di remote prevede di destinazione principale di un'app tooyour in hello **destinazioni** sezione.
2. Fare clic su **funzionalità**, attivare **modalità di Background**e controllare hello **notifiche remoto** casella di controllo.
   
    ![][IOS3]
3. Andare troppo**Main**e assicurarsi di disporre di un Controller di visualizzazione (di cui tooas Home View Controller in questa esercitazione) da [notifica utente](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione.
4. Aggiungere un **navigazione Controller** tooyour storyboard e trascinamento del controllo tooHome View Controller toomake hello **radice vista** di navigazione. Verificare che hello **è iniziale View Controller** negli attributi di controllo è selezionata per hello navigazione Controller.
5. Aggiungere un **View Controller** toostoryboard e aggiungere un **visualizzazione immagine**. Si tratta hello pagina gli utenti vedranno una volta sceglieranno toolearn più facendo clic su notifiication hello. L'aspetto dello storyboard dovrebbe essere simile al seguente:
   
    ![][IOS4]
6. Fare clic su hello **Home View Controller** nel storyboard e assicurarsi che sia **homeViewController** come relativo **classe personalizzata** e **Storyboard ID**sotto il controllo di identità hello.
7. Hello stesso per il Controller di visualizzazione immagine come **imageViewController**.
8. Quindi, creare una nuova classe di Controller di visualizzazione denominata **imageViewController** toohandle hello dell'interfaccia utente appena creato.
9. In **imageViewController.h**, aggiungere hello dopo le dichiarazioni di interfaccia toohello del controller. Verificare che toocontrol e trascinate dalla hello storyboard immagine vista toothese proprietà toolink hello due:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. In **imageViewController.m**, aggiungere hello segue alla fine di hello del **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. In **appdelegate. M**, controller di immagine hello importazione è stato creato:
    
        #import "imageViewController.h"
12. Aggiungere una sezione dell'interfaccia con hello segue la dichiarazione:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. In **AppDelegate** assicurarsi che l'app esegua la registrazione per le notifiche automatiche in **application: didFinishLaunchingWithOptions**:
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. Sostituire in seguito all'implementazione per hello **applicazione: didRegisterForRemoteNotificationsWithDeviceToken** storyboard hello tootake dell'interfaccia utente viene modificato in considerazione:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Aggiungere quindi hello troppo dei seguenti metodi**appdelegate. M** tooretrieve hello immagine dall'endpoint e inviare una notifica locale una volta completato il recupero. Assicurarsi che segnaposto hello di toosubstitute `{backend endpoint}` con l'endpoint di back-end:
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Gestire la notifica di locale hello sopra aprendo hello immagine Visualizza controller **appdelegate. M** con hello dei seguenti metodi:
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Eseguire l'applicazione hello
1. In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).
2. Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e una password di hello stesso valore per l'autenticazione e fare clic su **Accedi**.
3. Fare clic su **Send push** (Invia push). Verrà visualizzato un avviso nell'app. Se fa clic su **più**, sarà possibile portare toohello immagine scelto tooinclude nel back-end app.
4. È anche possibile fare clic su **inviare push** e premere immediatamente pulsante home di hello del dispositivo. Dopo alcuni istanti si riceverà una notifica push. Se si tocca su di esso o fare clic su altro, verranno portati contenuto dell'immagine rich tooyour app e hello.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
