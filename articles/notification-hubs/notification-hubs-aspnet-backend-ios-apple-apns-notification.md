---
title: aaaAzure utenti notificare gli hub di notifica per iOS con back-end .NET
description: Informazioni su come toosend push toousers notifiche in Azure. Esempi di codice scritti in Objective-C e hello API .NET per hello di back-end.
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="b6ef2-104">Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET</span><span class="sxs-lookup"><span data-stu-id="b6ef2-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="b6ef2-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b6ef2-105">Overview</span></span>
<span data-ttu-id="b6ef2-106">Supporto di notifica push in Azure consente tooaccess un semplice utilizzo, multipiattaforma e infrastruttura push di scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="b6ef2-107">Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push utente app specifica tooa di notifiche in un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="b6ef2-108">Un back-end ASP.NET WebAPI è tooauthenticate utilizzati client e le notifiche di toogenerate, come illustrato nell'argomento Guida hello [registrazione dal back-end app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="b6ef2-109">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="b6ef2-110">In questa esercitazione è anche hello prerequisiti toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="b6ef2-111">Se si desidera toouse App per dispositivi mobili come il servizio back-end, vedere hello [Mobile App introduzione Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="b6ef2-112">Modificare l'app per iOS</span><span class="sxs-lookup"><span data-stu-id="b6ef2-112">Modify your iOS app</span></span>
1. <span data-ttu-id="b6ef2-113">Aprire hello singola pagina Visualizza app è stato creato in hello [Introduzione agli hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b6ef2-114">In questa sezione si presuppone che il progetto sia configurato con un nome di organizzazione vuoto.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="b6ef2-115">In caso contrario, sarà necessario tooprepend i nomi di classe tooall nome dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="b6ef2-116">Nel Main aggiungere componenti hello illustrati nella schermata di hello seguito dalla libreria di oggetti hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="b6ef2-117">**Nome utente**: UITextField A con il testo segnaposto, *immettere nome utente*, immediatamente di sotto di hello inviare etichetta risultati e toohello vincolata a sinistra e i margini destro e di sotto di hello inviare etichetta risultati.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="b6ef2-118">**Password**: UITextField A con il testo segnaposto, *immettere la Password*, immediatamente sotto hello campo di testo Nome utente e toohello vincolata a sinistra e a destra i margini e di sotto di campo di testo Nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="b6ef2-119">Controllare hello **Secure testo** opzione nel controllo di attributo, hello in *restituire chiave*.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="b6ef2-120">**Accedi**: UIButton A con l'etichetta immediatamente sotto il campo di testo password hello e deselezionare hello **abilitato** opzione nel controllo gli attributi, hello in *contenuto del controllo*</span><span class="sxs-lookup"><span data-stu-id="b6ef2-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="b6ef2-121">**WNS**: etichetta e l'invio di commutatore tooenable hello notifica il servizio di notifica di Windows se sia stata impostata su hub hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="b6ef2-122">Vedere hello [Windows Introduzione](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="b6ef2-123">**GCM**: etichetta e l'invio di commutatore tooenable hello tooGoogle notifica messaggistica Cloud se sia stata impostata su hub hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="b6ef2-124">Vedere l'esercitazione [Introduzione ad Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="b6ef2-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="b6ef2-125">**APNS**: etichetta e l'invio di commutatore tooenable hello notifica toohello Apple piattaforma Notification Service.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="b6ef2-126">**Recipent Username**: UITextField A con il testo segnaposto, *tag username destinatario*immediatamente di sotto di hello GCM etichetta e vincolata toohello sinistro e destro margini e di sotto di hello GCM assegnare un'etichetta.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="b6ef2-127">Alcuni componenti sono stati aggiunti in hello [Introduzione agli hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="b6ef2-128">**CTRL** trascinare componenti hello tooViewController.h visualizzazione hello e aggiungere questi punti vendita di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="b6ef2-129">In ViewController.h, aggiungere hello seguente `#define` subito dopo le istruzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="b6ef2-130">Hello Substitute *< immettere l'Endpoint di back-end\>*  segnaposto con URL di destinazione utilizzato toodeploy back-end app nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="b6ef2-131">Ad esempio, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="b6ef2-132">Nel progetto, creare un nuovo **Cocoa tocco classe** denominato **RegisterClient** toointerface con hello ASP.NET back-end è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="b6ef2-133">Creare l'eredità dalla classe hello `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="b6ef2-134">Aggiungere quindi hello seguente di codice hello RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="b6ef2-135">In hello RegisterClient.m aggiornare hello `@interface` sezione:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. <span data-ttu-id="b6ef2-136">Sostituire hello `@implementation` sezione hello RegisterClient.m con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    <span data-ttu-id="b6ef2-137">codice Hello precedente implementa la logica di hello descritto nell'articolo Guida hello [registrazione dal back-end app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) utilizzando NSURLSession tooperform REST chiama back-end app tooyour e NSUserDefaults toolocally archivio hello registrationId restituito dall'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="b6ef2-138">Si noti che questa classe richiede la relativa proprietà **authorizationHeader** toobe set in ordine toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="b6ef2-139">Questa proprietà è impostata tramite hello **ViewController** classe dopo l'accesso hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="b6ef2-140">In ViewController.h aggiungere un'istruzione `#import` per RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="b6ef2-141">Quindi aggiungere una dichiarazione di token del dispositivo hello e fare riferimento a tooa `RegisterClient` istanza in hello `@interface` sezione:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="b6ef2-142">In ViewController.m, aggiungere una dichiarazione di metodo privato in hello `@interface` sezione:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="b6ef2-143">Hello frammento seguente non è uno schema di autenticazione sicura, è necessario sostituire l'implementazione di hello di hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** con il meccanismo di autenticazione specifico viene generato un toobe token di autenticazione utilizzato da hello register classe client, ad esempio OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="b6ef2-144">Quindi in hello `@implementation` sezione di ViewController.m aggiungere hello seguente di codice che aggiunge l'implementazione di hello per impostazione hello dispositivo token e l'autenticazione dell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    <span data-ttu-id="b6ef2-145">Si noti come token del dispositivo hello impostazione consenta hello pulsante Accedi.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="b6ef2-146">In questo modo come parte dell'azione di account di accesso hello, controller di visualizzazione hello registra le notifiche push con back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="b6ef2-147">Di conseguenza, non è desiderabile che accedi toobe azione accessibile fino a quando i token del dispositivo hello è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="b6ef2-148">È possibile separare hello Accedi dalla registrazione push hello come primo hello si verifica prima hello quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="b6ef2-149">In ViewController.m, utilizzare hello seguente metodo di azione hello tooimplement frammenti di codice per il **Accedi** pulsante e un metodo toosend hello messaggio di notifica tramite hello back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="b6ef2-150">(IBAction) LogInAction: mittente (id) {/ / crea l'intestazione di autenticazione e impostate nel registro client NSString * username = self. UsernameField.text;   Password NSString * = self. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="b6ef2-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="b6ef2-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="b6ef2-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tag: nil andCompletion:^(NSError* error) {Se (! errore) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correttamente!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="b6ef2-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="b6ef2-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="b6ef2-154">Passare i tag di hello pns e il nome utente come parametri con hello URL REST toohello back-end ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="b6ef2-155">Richiesta NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [richiesta setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="b6ef2-156">Ottenere hello fittizio authenticationheader dal client register hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [richiesta setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="b6ef2-157">Aggiungere il corpo di messaggio di notifica hello [richiesta setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [richiesta setHTTPBody: [messaggi dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="b6ef2-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="b6ef2-158">Eseguire hello invia notifica API REST su hello ASP.NET back-end NSURLSessionDataTask * dataTask = [completionHandler:^(NSData *data, NSURLResponse *response, NSError  *di dataTaskWithRequest:request sessione Errore) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) risposta.        Se (errore | | HttpResponse. StatusCode! = 200) {NSString* stato = [NSString stringWithFormat:@"Error stato per % @: % d\nError: %@\n", pns, HttpResponse. StatusCode, errore];            dispatch_async(dispatch_get_main_queue(), ^ {/ / aggiungere testo, poiché tutte le chiamate PNS 3 possono anche avere informazioni tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="b6ef2-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="b6ef2-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="b6ef2-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="b6ef2-160">Aggiornare l'azione di hello per hello **invia una notifica** pulsante back-end ASP.NET di hello toouse e inviare tooany PNS abilitato per un commutatore.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. <span data-ttu-id="b6ef2-161">Nella funzione **ViewDidLoad**, aggiungere hello successivo tooinstantiate hello RegisterClient istanza e impostare hello delegato per i campi di testo.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="b6ef2-162">Ora in **appdelegate. M**, rimuovere tutto il contenuto del metodo hello hello **applicazione: didRegisterForPushNotificationWithDeviceToken:** e sostituirlo con hello seguente toomake assicurarsi che hello vista controller contiene hello più recente token del dispositivo recuperati dal servizio APN:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="b6ef2-163">Infine in **appdelegate. M**, assicurarsi di avere hello seguente metodo:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="b6ef2-164">Hello test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b6ef2-164">Test hello Application</span></span>
1. <span data-ttu-id="b6ef2-165">In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="b6ef2-166">Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="b6ef2-167">Può trattarsi di qualsiasi stringa, ma devono essere entrambi hello stesso valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="b6ef2-168">Quindi fare clic su **Log In**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="b6ef2-169">Verrà visualizzata una finestra popup che informa che la registrazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="b6ef2-170">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="b6ef2-171">In hello **tag username destinatario* testo immettere i tag del nome utente hello utilizzato con la registrazione di hello da un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="b6ef2-172">Immettere un messaggio di notifica e fare clic su **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="b6ef2-173">Solo i dispositivi di hello che dispone di una registrazione con tag del nome utente destinatario hello ricevono il messaggio di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="b6ef2-174">Viene inviato solo gli utenti toothose.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
