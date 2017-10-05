---
title: Push avanzato degli hub di notifica di Azure
description: Informazioni su come inviare notifiche push complesse a un'app per iOS da Azure. Gli esempi di codice sono scritti in Objective-C e C#.
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="81d5f-104">Push avanzato degli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="81d5f-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="81d5f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="81d5f-105">Overview</span></span>
<span data-ttu-id="81d5f-106">Per offrire agli utenti contenuti immediati avanzati, in un'applicazione potrebbe essere necessario effettuare il push non solo del testo normale.</span><span class="sxs-lookup"><span data-stu-id="81d5f-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="81d5f-107">Queste notifiche promuovono le interazioni con l'utente e presentano contenuti come URL, immagini/buoni e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="81d5f-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="81d5f-108">Questa esercitazione è basata sull'argomento [Usare Hub di notifica per inviare notifiche agli utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) e spiega come inviare notifiche push che incorporano payload (ad esempio, immagini).</span><span class="sxs-lookup"><span data-stu-id="81d5f-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="81d5f-109">Questa esercitazione è compatibile con iOS 7 e 8.</span><span class="sxs-lookup"><span data-stu-id="81d5f-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="81d5f-110">In generale:</span><span class="sxs-lookup"><span data-stu-id="81d5f-110">At a high level:</span></span>

1. <span data-ttu-id="81d5f-111">Il back-end dell'app:</span><span class="sxs-lookup"><span data-stu-id="81d5f-111">The app backend:</span></span>
   * <span data-ttu-id="81d5f-112">Archivia il payload avanzato (in questo caso, un'immagine) nell'archivio locale/database back-end</span><span class="sxs-lookup"><span data-stu-id="81d5f-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="81d5f-113">Invia l'ID di questa notifica avanzata al dispositivo</span><span class="sxs-lookup"><span data-stu-id="81d5f-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="81d5f-114">L'app sul dispositivo:</span><span class="sxs-lookup"><span data-stu-id="81d5f-114">App on the device:</span></span>
   * <span data-ttu-id="81d5f-115">Contatta il back-end che richiede il payload avanzato con l'ID ricevuto</span><span class="sxs-lookup"><span data-stu-id="81d5f-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="81d5f-116">Invia agli utenti notifiche sul dispositivo al termine del recupero dei dati e mostra immediatamente il payload quando gli utenti toccano per avere altre informazioni</span><span class="sxs-lookup"><span data-stu-id="81d5f-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="81d5f-117">Progetto WebAPI</span><span class="sxs-lookup"><span data-stu-id="81d5f-117">WebAPI Project</span></span>
1. <span data-ttu-id="81d5f-118">In Visual Studio aprire il progetto **AppBackend** creato nell'esercitazione sulla [creazione di notifiche per gli utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="81d5f-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="81d5f-119">Acquisire un'immagine con cui inviare una notifica agli utenti e inserirla in una cartella **img** nella directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="81d5f-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="81d5f-120">In Esplora soluzioni fare clic su **Mostra tutti i file**, quindi fare clic con il pulsante destro del mouse sulla cartella e selezionare **Includi nel progetto**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="81d5f-121">Con l'immagine selezionata, nella finestra Proprietà impostare Azione di compilazione su **Risorsa incorporata**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="81d5f-122">In **Notifications.cs**aggiungere la seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="81d5f-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="81d5f-123">Aggiornare l'intera classe **Notifications** con il seguente codice.</span><span class="sxs-lookup"><span data-stu-id="81d5f-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="81d5f-124">Assicurarsi di sostituire i segnaposto con le credenziali dell'hub di notifica e il nome file di immagine.</span><span class="sxs-lookup"><span data-stu-id="81d5f-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="81d5f-125">(facoltativo) Per altre informazioni su come aggiungere e ottenere le risorse del progetto, fare riferimento a [Come incorporare le risorse e accedervi usando Visual C#](http://support.microsoft.com/kb/319292).</span><span class="sxs-lookup"><span data-stu-id="81d5f-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="81d5f-126">In **NotificationsController.cs** ridefinire **NotificationsController** con i frammenti di codice riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="81d5f-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="81d5f-127">Questo codice invia un ID notifica avanzata automatica iniziale al dispositivo e consente il recupero lato client dell'immagine:</span><span class="sxs-lookup"><span data-stu-id="81d5f-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="81d5f-128">L'app verrà ora nuovamente distribuita in un sito Web di Azure in modo da renderla accessibile da tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="81d5f-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="81d5f-129">Fare clic con il pulsante destro del mouse sul progetto **AppBackend** e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="81d5f-130">Selezionare un sito Web Azure come destinazione di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="81d5f-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="81d5f-131">Accedere con l'account di Azure e selezionare un sito Web nuovo o esistente, quindi prendere nota della proprietà **URL di destinazione** nella scheda **Connessione**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="81d5f-132">Si farà riferimento a quest'URL come *endpoint back-end* più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81d5f-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="81d5f-133">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="81d5f-134">Modifica del progetto iOS</span><span class="sxs-lookup"><span data-stu-id="81d5f-134">Modify the iOS project</span></span>
<span data-ttu-id="81d5f-135">Dopo avere modificato il back-end del app per poter inviare solo l' *id* di una notifica, si modificherà l'app per iOS per poter gestire tale ID e recuperare il messaggio avanzato dal back-end.</span><span class="sxs-lookup"><span data-stu-id="81d5f-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="81d5f-136">Aprire il progetto iOS e abilitare le notifiche remote andando alla destinazione dell'app principale nella sezione **Targets** .</span><span class="sxs-lookup"><span data-stu-id="81d5f-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="81d5f-137">Fare clic su **Capabilities** (Funzionalità), attivare **Background Modes** (Modalità sfondo), e selezionare la casella di controllo **Remote Notifications** (Notifiche remote).</span><span class="sxs-lookup"><span data-stu-id="81d5f-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="81d5f-138">Passare a **Main.storyboard**e verificare che sia presente un elemento View Controller (in questa esercitazione, Home View Controller) creato nell'esercitazione relativa all’ [invio di notifiche per gli utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="81d5f-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="81d5f-139">Aggiungere un elemento **Navigation Controller** allo storyboard e trascinarlo tenendo premuto CTRL sull'elemento Home View Controller per impostarlo come **visualizzazione radice** della navigazione.</span><span class="sxs-lookup"><span data-stu-id="81d5f-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="81d5f-140">Assicurarsi che **Is Initial View Controller** in Attributes inspector sia selezionato solo per Navigation Controller.</span><span class="sxs-lookup"><span data-stu-id="81d5f-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="81d5f-141">Aggiungere un elemento **View Controller** allo storyboard e aggiungere un elemento **Image View**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="81d5f-142">Questa sarà la pagina visualizzata dagli utenti quando faranno clic sulla notifica per avere altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="81d5f-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="81d5f-143">L'aspetto dello storyboard dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="81d5f-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="81d5f-144">Fare clic sull'elemento **Home View Controller** nello storyboard e verificare che abbia **homeViewController** come **Custom Class** e **Storyboard ID** in Identity inspector.</span><span class="sxs-lookup"><span data-stu-id="81d5f-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="81d5f-145">Fare lo stesso per Image View Controller come **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="81d5f-146">Creare quindi una nuova classe View Controller denominata **imageViewController** per gestire l'interfaccia utente appena creata.</span><span class="sxs-lookup"><span data-stu-id="81d5f-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="81d5f-147">In **imageViewController.h**, aggiungere quanto segue alle dichiarazioni di interfaccia del controller.</span><span class="sxs-lookup"><span data-stu-id="81d5f-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="81d5f-148">Trascinare tenendo premuto CTRL dalla visualizzazione immagine dello storyboard a queste proprietà per collegarle:</span><span class="sxs-lookup"><span data-stu-id="81d5f-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="81d5f-149">In **imageViewController.m** aggiungere quanto segue alla fine di **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="81d5f-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="81d5f-150">In **AppDelegate.m**importare il controller immagine creato:</span><span class="sxs-lookup"><span data-stu-id="81d5f-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="81d5f-151">Aggiungere una sezione dell'interfaccia con la seguente dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="81d5f-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="81d5f-152">In **AppDelegate** assicurarsi che l'app esegua la registrazione per le notifiche automatiche in **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="81d5f-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="81d5f-153">Sostituire la seguente implementazione per **application:didRegisterForRemoteNotificationsWithDeviceToken** per tenere in considerazione le modifiche apportate all'interfaccia utente dello storyboard:</span><span class="sxs-lookup"><span data-stu-id="81d5f-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="81d5f-154">Aggiungere quindi i metodi seguenti ad **AppDelegate.m** per recuperare l'immagine dall'endpoint e inviare una notifica locale al termine del recupero.</span><span class="sxs-lookup"><span data-stu-id="81d5f-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="81d5f-155">Assicurarsi di sostituire il segnaposto `{backend endpoint}` con l'endpoint back-end:</span><span class="sxs-lookup"><span data-stu-id="81d5f-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="81d5f-156">Gestire la notifica locale precedente aprendo il controller di visualizzazione immagine in **AppDelegate.m** con i seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="81d5f-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="81d5f-157">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="81d5f-157">Run the Application</span></span>
1. <span data-ttu-id="81d5f-158">In XCode eseguire l'app su un dispositivo iOS fisico (le notifiche push non funzioneranno nel simulatore).</span><span class="sxs-lookup"><span data-stu-id="81d5f-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="81d5f-159">Nell'interfaccia utente dell'app per iOS immettere un nome utente e una password con lo stesso valore per l'autenticazione e fare clic su **Log In**.</span><span class="sxs-lookup"><span data-stu-id="81d5f-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="81d5f-160">Fare clic su **Send push** (Invia push). Verrà visualizzato un avviso nell'app.</span><span class="sxs-lookup"><span data-stu-id="81d5f-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="81d5f-161">Se si fa clic su **More** (Altro), si passerà all'immagine che si è scelto di includere nel back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="81d5f-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="81d5f-162">È anche possibile fare clic su **Send push** e premere subito il pulsante home del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="81d5f-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="81d5f-163">Dopo alcuni istanti si riceverà una notifica push.</span><span class="sxs-lookup"><span data-stu-id="81d5f-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="81d5f-164">Se la si tocca o si fa clic su More, si passerà all'app e al contenuto avanzato dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="81d5f-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
