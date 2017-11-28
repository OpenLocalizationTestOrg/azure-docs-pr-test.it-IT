
<span data-ttu-id="1bfa8-101">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-101">**Objective-C**:</span></span>

1. <span data-ttu-id="1bfa8-102">In **QSAppDelegate.m** importare iOS SDK e **QSTodoService.h**:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-102">In **QSAppDelegate.m**, import the iOS SDK and **QSTodoService.h**:</span></span>
   
        #import <MicrosoftAzureMobile/MicrosoftAzureMobile.h>
        #import "QSTodoService.h"
2. <span data-ttu-id="1bfa8-103">In `didFinishLaunchingWithOptions` in **QSAppDelegate.m** inserire le righe seguenti prima di `return YES;`:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-103">In `didFinishLaunchingWithOptions` in **QSAppDelegate.m**, insert the following lines right before `return YES;`:</span></span>
   
        UIUserNotificationSettings* notificationSettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:notificationSettings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
3. <span data-ttu-id="1bfa8-104">In **QSAppDelegate.m**aggiungere i metodi del gestore seguenti.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-104">In **QSAppDelegate.m**, add the following handler methods.</span></span> <span data-ttu-id="1bfa8-105">L'app è ora aggiornata per il supporto delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-105">Your app is now updated to support push notifications.</span></span> 
   
        // Registration with APNs is successful
        - (void)application:(UIApplication *)application
        didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
   
            QSTodoService *todoService = [QSTodoService defaultService];
            MSClient *client = todoService.client;
   
            [client.push registerDeviceToken:deviceToken completion:^(NSError *error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
            }];
        }
   
        // Handle any failure to register
        - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:
        (NSError *)error {
            NSLog(@"Failed to register for remote notifications: %@", error);
        }
   
        // Use userInfo in the payload to display an alert.
        - (void)application:(UIApplication *)application
              didReceiveRemoteNotification:(NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
   
            NSDictionary *apsPayload = userInfo[@"aps"];
            NSString *alertString = apsPayload[@"alert"];
   
            // Create alert with notification content.
            UIAlertController *alertController = [UIAlertController
                                          alertControllerWithTitle:@"Notification"
                                          message:alertString
                                          preferredStyle:UIAlertControllerStyleAlert];
   
            UIAlertAction *cancelAction = [UIAlertAction
                                           actionWithTitle:NSLocalizedString(@"Cancel", @"Cancel")
                                           style:UIAlertActionStyleCancel
                                           handler:^(UIAlertAction *action)
                                           {
                                               NSLog(@"Cancel");
                                           }];
   
            UIAlertAction *okAction = [UIAlertAction
                                       actionWithTitle:NSLocalizedString(@"OK", @"OK")
                                       style:UIAlertActionStyleDefault
                                       handler:^(UIAlertAction *action)
                                       {
                                           NSLog(@"OK");
                                       }];
   
            [alertController addAction:cancelAction];
            [alertController addAction:okAction];
   
            // Get current view controller.
            UIViewController *currentViewController = [[[[UIApplication sharedApplication] delegate] window] rootViewController];
            while (currentViewController.presentedViewController)
            {
                currentViewController = currentViewController.presentedViewController;
            }
   
            // Display alert.
            [currentViewController presentViewController:alertController animated:YES completion:nil];
   
        }

<span data-ttu-id="1bfa8-106">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-106">**Swift**:</span></span>

1. <span data-ttu-id="1bfa8-107">Aggiungere il file **ClientManager.swift** con i seguenti contenuti.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-107">Add file **ClientManager.swift** with the following contents.</span></span> <span data-ttu-id="1bfa8-108">Sostituire *%AppUrl%* con l'URL del back-end di app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-108">Replace *%AppUrl%* with the URL of the Azure Mobile App backend.</span></span>
   
        class ClientManager {
            static let sharedClient = MSClient(applicationURLString: "%AppUrl%")
        }
2. <span data-ttu-id="1bfa8-109">In **ToDoTableViewController.swift** sostituire la riga `let client` che inizializza un `MSClient` con la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-109">In **ToDoTableViewController.swift**, replace the `let client` line that initializes an `MSClient` with this line:</span></span>
   
        let client = ClientManager.sharedClient
3. <span data-ttu-id="1bfa8-110">In **AppDelegate.swift** sostituire il corpo di `func application` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1bfa8-110">In **AppDelegate.swift**, replace the body of `func application` as follows:</span></span>
   
        func application(application: UIApplication,
          didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
           application.registerUserNotificationSettings(
               UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound],
                   categories: nil))
           application.registerForRemoteNotifications()
           return true
        }
4. <span data-ttu-id="1bfa8-111">In **AppDelegate.swift**, aggiungere i metodi del gestore seguenti.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-111">In **AppDelegate.swift**, add the following handler methods.</span></span> <span data-ttu-id="1bfa8-112">L'app è ora aggiornata per il supporto delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="1bfa8-112">Your app is now updated to support push notifications.</span></span>
   
        func application(application: UIApplication,
           didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
            ClientManager.sharedClient.push?.registerDeviceToken(deviceToken) { error in
                print("Error registering for notifications: ", error?.description)
            }
        }
   
        func application(application: UIApplication,
           didFailToRegisterForRemoteNotificationsWithError error: NSError) {
            print("Failed to register for remote notifications: ", error.description)
        }
   
        func application(application: UIApplication,
           didReceiveRemoteNotification userInfo: [NSObject: AnyObject]) {
   
            print(userInfo)
   
            let apsNotification = userInfo["aps"] as? NSDictionary
            let apsString       = apsNotification?["alert"] as? String
   
            let alert = UIAlertController(title: "Alert", message: apsString, preferredStyle: .Alert)
            let okAction = UIAlertAction(title: "OK", style: .Default) { _ in
                print("OK")
            }
            let cancelAction = UIAlertAction(title: "Cancel", style: .Default) { _ in
                print("Cancel")
            }
   
            alert.addAction(okAction)
            alert.addAction(cancelAction)
   
            var currentViewController = self.window?.rootViewController
            while currentViewController?.presentedViewController != nil {
                currentViewController = currentViewController?.presentedViewController
            }
   
            currentViewController?.presentViewController(alert, animated: true) {}
   
        }

