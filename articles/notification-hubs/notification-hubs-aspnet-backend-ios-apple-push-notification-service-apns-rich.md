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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="f405a-104">Push avanzato degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="f405a-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="f405a-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f405a-105">Overview</span></span>
<span data-ttu-id="f405a-106">In ordine tooengage gli utenti con contenuto RTF immediata, un'applicazione può essere toopush oltre a testo normale.</span><span class="sxs-lookup"><span data-stu-id="f405a-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="f405a-107">Queste notifiche promuovono le interazioni con l'utente e presentano contenuti come URL, immagini/buoni e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f405a-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="f405a-108">In questa esercitazione si basa su hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) argomento e Mostra come toosend push delle notifiche che incorporano payload (ad esempio, l'immagine).</span><span class="sxs-lookup"><span data-stu-id="f405a-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="f405a-109">Questa esercitazione è compatibile con iOS 7 e 8.</span><span class="sxs-lookup"><span data-stu-id="f405a-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="f405a-110">In generale:</span><span class="sxs-lookup"><span data-stu-id="f405a-110">At a high level:</span></span>

1. <span data-ttu-id="f405a-111">back-end app Hello:</span><span class="sxs-lookup"><span data-stu-id="f405a-111">hello app backend:</span></span>
   * <span data-ttu-id="f405a-112">Archivi hello payload avanzati (in questo caso, l'immagine) in archiviazione di database o locale hello back-end</span><span class="sxs-lookup"><span data-stu-id="f405a-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="f405a-113">Invia l'ID del dispositivo toohello notifica avanzata</span><span class="sxs-lookup"><span data-stu-id="f405a-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="f405a-114">App sul dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="f405a-114">App on hello device:</span></span>
   * <span data-ttu-id="f405a-115">Contatti hello back-end la richiesta di payload avanzati di hello con ID hello riceve</span><span class="sxs-lookup"><span data-stu-id="f405a-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="f405a-116">Invia notifiche agli utenti sul dispositivo hello quando il recupero dei dati è stata completata e viene illustrato il payload di hello immediatamente quando gli utenti toccano toolearn più</span><span class="sxs-lookup"><span data-stu-id="f405a-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="f405a-117">Progetto WebAPI</span><span class="sxs-lookup"><span data-stu-id="f405a-117">WebAPI Project</span></span>
1. <span data-ttu-id="f405a-118">In Visual Studio, aprire hello **AppBackend** progetto creato in hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f405a-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="f405a-119">Ottenere un'immagine che si desidera che gli utenti toonotify con e inserirlo in un **img** cartella nella directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="f405a-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="f405a-120">Fare clic su **Mostra tutti i file** in hello Esplora soluzioni e fare clic sulla cartella di hello, troppo**Includi nel progetto**.</span><span class="sxs-lookup"><span data-stu-id="f405a-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="f405a-121">Con l'immagine di hello selezionata, modificare l'azione di compilazione nella finestra Proprietà troppo**risorsa incorporata**.</span><span class="sxs-lookup"><span data-stu-id="f405a-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="f405a-122">In **Notifications.cs**, aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="f405a-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="f405a-123">Hello aggiornamento intero **notifiche** classe con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="f405a-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="f405a-124">Essere tooreplace che segnaposto hello con le credenziali di hub di notifica e un nome di file di immagine.</span><span class="sxs-lookup"><span data-stu-id="f405a-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="f405a-125">(facoltativo) Fare riferimento troppo[come tooembed e alle risorse utilizzando Visual c#](http://support.microsoft.com/kb/319292) per ulteriori informazioni su come tooadd e ottenere le risorse del progetto.</span><span class="sxs-lookup"><span data-stu-id="f405a-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="f405a-126">In **NotificationsController.cs**, ridefinire **NotificationsController** con hello frammenti di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="f405a-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="f405a-127">Si invia un toodevice id la notifica iniziale RTF invisibile all'utente e consente il recupero del client dell'immagine:</span><span class="sxs-lookup"><span data-stu-id="f405a-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="f405a-128">Ora si distribuirà nuovamente questo tooan app sito Web di Azure in ordine toomake sia accessibile da tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="f405a-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="f405a-129">Fare clic su hello **AppBackend** del progetto e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f405a-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="f405a-130">Selezionare un sito Web Azure come destinazione di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f405a-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="f405a-131">Accedere con l'account Azure e selezionare un sito Web nuovo o esistente e prendere nota di hello **URL di destinazione** proprietà hello **connessione** scheda. Si farà riferimento toothis URL come il *endpoint di back-end* più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f405a-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="f405a-132">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f405a-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="f405a-133">Modificare il progetto di iOS hello</span><span class="sxs-lookup"><span data-stu-id="f405a-133">Modify hello iOS project</span></span>
<span data-ttu-id="f405a-134">Ora che sono state modificate le hello solo di back-end toosend app *id* di una notifica, si cambia il toohandle app iOS che l'id e recuperare dettagliata del messaggio hello dal back-end.</span><span class="sxs-lookup"><span data-stu-id="f405a-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="f405a-135">Aprire il progetto iOS e abilitare le notifiche di remote prevede di destinazione principale di un'app tooyour in hello **destinazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="f405a-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="f405a-136">Fare clic su **funzionalità**, attivare **modalità di Background**e controllare hello **notifiche remoto** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="f405a-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="f405a-137">Andare troppo**Main**e assicurarsi di disporre di un Controller di visualizzazione (di cui tooas Home View Controller in questa esercitazione) da [notifica utente](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f405a-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="f405a-138">Aggiungere un **navigazione Controller** tooyour storyboard e trascinamento del controllo tooHome View Controller toomake hello **radice vista** di navigazione.</span><span class="sxs-lookup"><span data-stu-id="f405a-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="f405a-139">Verificare che hello **è iniziale View Controller** negli attributi di controllo è selezionata per hello navigazione Controller.</span><span class="sxs-lookup"><span data-stu-id="f405a-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="f405a-140">Aggiungere un **View Controller** toostoryboard e aggiungere un **visualizzazione immagine**.</span><span class="sxs-lookup"><span data-stu-id="f405a-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="f405a-141">Si tratta hello pagina gli utenti vedranno una volta sceglieranno toolearn più facendo clic su notifiication hello.</span><span class="sxs-lookup"><span data-stu-id="f405a-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="f405a-142">L'aspetto dello storyboard dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f405a-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="f405a-143">Fare clic su hello **Home View Controller** nel storyboard e assicurarsi che sia **homeViewController** come relativo **classe personalizzata** e **Storyboard ID**sotto il controllo di identità hello.</span><span class="sxs-lookup"><span data-stu-id="f405a-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="f405a-144">Hello stesso per il Controller di visualizzazione immagine come **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="f405a-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="f405a-145">Quindi, creare una nuova classe di Controller di visualizzazione denominata **imageViewController** toohandle hello dell'interfaccia utente appena creato.</span><span class="sxs-lookup"><span data-stu-id="f405a-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="f405a-146">In **imageViewController.h**, aggiungere hello dopo le dichiarazioni di interfaccia toohello del controller.</span><span class="sxs-lookup"><span data-stu-id="f405a-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="f405a-147">Verificare che toocontrol e trascinate dalla hello storyboard immagine vista toothese proprietà toolink hello due:</span><span class="sxs-lookup"><span data-stu-id="f405a-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="f405a-148">In **imageViewController.m**, aggiungere hello segue alla fine di hello del **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="f405a-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="f405a-149">In **appdelegate. M**, controller di immagine hello importazione è stato creato:</span><span class="sxs-lookup"><span data-stu-id="f405a-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="f405a-150">Aggiungere una sezione dell'interfaccia con hello segue la dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="f405a-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="f405a-151">In **AppDelegate** assicurarsi che l'app esegua la registrazione per le notifiche automatiche in **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="f405a-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="f405a-152">Sostituire in seguito all'implementazione per hello **applicazione: didRegisterForRemoteNotificationsWithDeviceToken** storyboard hello tootake dell'interfaccia utente viene modificato in considerazione:</span><span class="sxs-lookup"><span data-stu-id="f405a-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="f405a-153">Aggiungere quindi hello troppo dei seguenti metodi**appdelegate. M** tooretrieve hello immagine dall'endpoint e inviare una notifica locale una volta completato il recupero.</span><span class="sxs-lookup"><span data-stu-id="f405a-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="f405a-154">Assicurarsi che segnaposto hello di toosubstitute `{backend endpoint}` con l'endpoint di back-end:</span><span class="sxs-lookup"><span data-stu-id="f405a-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="f405a-155">Gestire la notifica di locale hello sopra aprendo hello immagine Visualizza controller **appdelegate. M** con hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="f405a-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="f405a-156">Eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f405a-156">Run hello Application</span></span>
1. <span data-ttu-id="f405a-157">In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).</span><span class="sxs-lookup"><span data-stu-id="f405a-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="f405a-158">Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e una password di hello stesso valore per l'autenticazione e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="f405a-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="f405a-159">Fare clic su **Send push** (Invia push). Verrà visualizzato un avviso nell'app.</span><span class="sxs-lookup"><span data-stu-id="f405a-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="f405a-160">Se fa clic su **più**, sarà possibile portare toohello immagine scelto tooinclude nel back-end app.</span><span class="sxs-lookup"><span data-stu-id="f405a-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="f405a-161">È anche possibile fare clic su **inviare push** e premere immediatamente pulsante home di hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f405a-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="f405a-162">Dopo alcuni istanti si riceverà una notifica push.</span><span class="sxs-lookup"><span data-stu-id="f405a-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="f405a-163">Se si tocca su di esso o fare clic su altro, verranno portati contenuto dell'immagine rich tooyour app e hello.</span><span class="sxs-lookup"><span data-stu-id="f405a-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
