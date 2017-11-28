---
title: utente corrente di aaaRegister hello per le notifiche push tramite l'API Web | Documenti Microsoft
description: Informazioni su come toorequest registrazione della notifica push in un'app iOS con gli hub di notifica di Azure quando la registrazione viene eseguita tramite l'API Web ASP.NET.
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="a26fe-103">Registrare l'utente corrente di hello per le notifiche push tramite ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a26fe-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a26fe-104">iOS</span><span class="sxs-lookup"><span data-stu-id="a26fe-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a26fe-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a26fe-105">Overview</span></span>
<span data-ttu-id="a26fe-106">Questo argomento viene illustrato come toorequest push registrazione della notifica con gli hub di notifica di Azure quando la registrazione viene eseguita da ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="a26fe-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="a26fe-107">In questo argomento estende esercitazione hello [notificare agli utenti con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="a26fe-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="a26fe-108">È necessario stati già completati i passaggi necessario hello nel servizio mobile toocreate esercitazione hello autenticato.</span><span class="sxs-lookup"><span data-stu-id="a26fe-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="a26fe-109">Per ulteriori informazioni su hello notificare scenario gli utenti, vedere [notificare agli utenti con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="a26fe-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="a26fe-110">Aggiornamento dell'app</span><span class="sxs-lookup"><span data-stu-id="a26fe-110">Update your app</span></span>
1. <span data-ttu-id="a26fe-111">Nel MainStoryboard_iPhone.storyboard, aggiungere hello seguendo i componenti dalla libreria di oggetti hello:</span><span class="sxs-lookup"><span data-stu-id="a26fe-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="a26fe-112">**Etichetta**: "TooUser con gli hub di notifica Push"</span><span class="sxs-lookup"><span data-stu-id="a26fe-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="a26fe-113">**Etichetta**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="a26fe-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="a26fe-114">**Etichetta**: "User"</span><span class="sxs-lookup"><span data-stu-id="a26fe-114">**Label**: "User"</span></span>
   * <span data-ttu-id="a26fe-115">**Campo di testo**: "User"</span><span class="sxs-lookup"><span data-stu-id="a26fe-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="a26fe-116">**Etichetta**: "Password"</span><span class="sxs-lookup"><span data-stu-id="a26fe-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="a26fe-117">**Campo di testo**: "Password"</span><span class="sxs-lookup"><span data-stu-id="a26fe-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="a26fe-118">**Pulsante**: "Login"</span><span class="sxs-lookup"><span data-stu-id="a26fe-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="a26fe-119">A questo punto lo storyboard è simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a26fe-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="a26fe-120">Nell'editor di Assistente hello, creare prese per tutti i controlli di hello commutato e chiamarli, collegare i campi di testo hello con hello View Controller (delegato) e creare un **azione** per hello **accesso** pulsante.</span><span class="sxs-lookup"><span data-stu-id="a26fe-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="a26fe-121">Creare una classe denominata **DeviceInfo**, e hello copia seguente codice nella sezione dell'interfaccia hello del file hello DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="a26fe-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="a26fe-122">Copiare hello seguente codice nella sezione di implementazione hello del file DeviceInfo.m hello:</span><span class="sxs-lookup"><span data-stu-id="a26fe-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="a26fe-123">In PushToUserAppDelegate.h, aggiungere hello singleton di proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a26fe-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="a26fe-124">In hello **didFinishLaunchingWithOptions** metodo PushToUserAppDelegate.m, aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a26fe-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="a26fe-125">prima riga Hello Inizializza hello **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="a26fe-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="a26fe-126">Hello seconda riga inizia hello per le notifiche push, che è già presente è registrazione sono stati già completati hello [iniziare con gli hub di notifica] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a26fe-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="a26fe-127">In PushToUserAppDelegate.m, implementare il metodo hello **didRegisterForRemoteNotificationsWithDeviceToken** nel AppDelegate e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a26fe-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="a26fe-128">Consente di impostare token del dispositivo per la richiesta di hello hello.</span><span class="sxs-lookup"><span data-stu-id="a26fe-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a26fe-129">A questo punto, il metodo non dovrebbe contenere altro codice.</span><span class="sxs-lookup"><span data-stu-id="a26fe-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="a26fe-130">Se si dispone già di una chiamata toohello **registerNativeWithDeviceToken** metodo che è stato aggiunto al termine di hello [iniziare con gli hub di notifica](/manage/services/notification-hubs/get-started-notification-hubs-ios/) dell'esercitazione, è necessario commento o rimuovere chiamata.</span><span class="sxs-lookup"><span data-stu-id="a26fe-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="a26fe-131">Nel file hello PushToUserAppDelegate.m aggiungere hello seguente metodo del gestore:</span><span class="sxs-lookup"><span data-stu-id="a26fe-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="a26fe-132">applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * avviso = [[UIAlertView alloc] initWithTitle:@"Notification" messaggio: cancelButtonTitle delegato: nil [userInfo objectForKey:@"inAppMessage"]: @ otherButtonTitles:nil "OK", null];   [avviso Mostra]; }</span><span class="sxs-lookup"><span data-stu-id="a26fe-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="a26fe-133">Questo metodo visualizza un avviso in hello dell'interfaccia utente quando l'applicazione riceve notifiche durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a26fe-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="a26fe-134">Aprire file PushToUserViewController.m hello e tastiera restituito hello in seguito all'implementazione hello:</span><span class="sxs-lookup"><span data-stu-id="a26fe-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="a26fe-135">In hello **viewDidLoad** metodo nel file hello PushToUserViewController.m inizializzare etichetta installationId hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a26fe-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="a26fe-136">Aggiungere le proprietà nell'interfaccia in PushToUserViewController.m seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a26fe-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="a26fe-137">Aggiungere quindi hello implementazione seguente:</span><span class="sxs-lookup"><span data-stu-id="a26fe-137">Then, add hello following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="a26fe-138">Copia hello esempio di codice in hello **accesso** creato da XCode metodo del gestore:</span><span class="sxs-lookup"><span data-stu-id="a26fe-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="a26fe-139">Questo metodo ottiene l'ID di installazione sia un canale per le notifiche push e lo invia, insieme a tipo di dispositivo hello, toohello autenticato metodo API Web che crea una registrazione di hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="a26fe-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="a26fe-140">Questa API Web è stata definita in [notificare agli utenti con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="a26fe-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="a26fe-141">Ora che hello client app è stata aggiornata, restituire toohello [notificare agli utenti con gli hub di notifica] e hello servizio mobile toosend notifiche di aggiornamento con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="a26fe-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificare agli utenti con gli hub di notifica]: /manage/services/notification-hubs/notify-users-aspnet

[iniziare con gli hub di notifica]: /manage/services/notification-hubs/get-started-notification-hubs-ios
