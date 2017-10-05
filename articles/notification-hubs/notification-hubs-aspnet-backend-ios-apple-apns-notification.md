---
title: Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET
description: Informazioni su come inviare notifiche push agli utenti in Azure. Gli esempi di codice sono scritti in Objective-C e nell'API .NET per il back-end.
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="c6371-104">Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET</span><span class="sxs-lookup"><span data-stu-id="c6371-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="c6371-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c6371-105">Overview</span></span>
<span data-ttu-id="c6371-106">Il supporto per le notifiche push in Azure consente di accedere a un'infrastruttura push facile da usare, multipiattaforma e con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="c6371-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="c6371-107">In questa esercitazione viene illustrato come usare Hub di notifica di Azure per inviare notifiche push a un utente specifico dell'app su un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="c6371-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="c6371-108">Per autenticare i client e generare le notifiche viene usato un back-end di API Web ASP.NET, come illustrato nell'argomento [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) (Registrazione dal back-end dell'app).</span><span class="sxs-lookup"><span data-stu-id="c6371-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="c6371-109">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6371-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="c6371-110">È inoltre propedeutica all'esercitazione [Push sicuro (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="c6371-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="c6371-111">Se si desidera usare le app per dispositivi mobili come servizio back-end, vedere [Introduzione alle app per dispositivi mobili con notifiche push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="c6371-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="c6371-112">Modificare l'app per iOS</span><span class="sxs-lookup"><span data-stu-id="c6371-112">Modify your iOS app</span></span>
1. <span data-ttu-id="c6371-113">Aprire l'app di visualizzazione Pagina singola creata nell'esercitazione [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c6371-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c6371-114">In questa sezione si presuppone che il progetto sia configurato con un nome di organizzazione vuoto.</span><span class="sxs-lookup"><span data-stu-id="c6371-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="c6371-115">In caso contrario, sarà necessario anteporre il nome dell'organizzazione a tutti i nomi di classi.</span><span class="sxs-lookup"><span data-stu-id="c6371-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="c6371-116">In Main.storyboard aggiungere i componenti illustrati nella schermata seguente dalla libreria di oggetti.</span><span class="sxs-lookup"><span data-stu-id="c6371-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="c6371-117">**Nome utente**: oggetto UITextField con testo segnaposto, *Enter Username*, immediatamente sotto l'etichetta per l'invio dei risultati e limitato dai margini sinistro e destro.</span><span class="sxs-lookup"><span data-stu-id="c6371-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="c6371-118">**Password**: oggetto UITextField con testo segnaposto, *Enter Password*, immediatamente sotto il campo di testo del nome utente e limitato dai margini sinistro e destro.</span><span class="sxs-lookup"><span data-stu-id="c6371-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="c6371-119">Selezionare l'opzione **Secure Text Entry** in Attribute Inspector sotto *Return Key*.</span><span class="sxs-lookup"><span data-stu-id="c6371-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="c6371-120">**Accesso**: oggetto UIButton con etichetta immediatamente sotto il campo di testo della password; deselezionare l'opzione **Abilitato** in Attributes Inspector sotto *Control-Content*.</span><span class="sxs-lookup"><span data-stu-id="c6371-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="c6371-121">**WNS**: etichetta e opzione per consentire l'invio della notifica al servizio di notifica Windows se è stato configurato nell'hub.</span><span class="sxs-lookup"><span data-stu-id="c6371-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="c6371-122">Vedere l'esercitazione [Introduzione a Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="c6371-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="c6371-123">**GCM**: etichetta e opzione per consentire l'invio della notifica a Google Cloud Messaging se è stato configurato nell'hub.</span><span class="sxs-lookup"><span data-stu-id="c6371-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="c6371-124">Vedere l'esercitazione [Introduzione ad Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c6371-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="c6371-125">**APNS**: etichetta e opzione per consentire l'invio della notifica al servizio di notifica della piattaforma di Apple.</span><span class="sxs-lookup"><span data-stu-id="c6371-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="c6371-126">**Nome utente del destinatario**: oggetto UITextField con testo segnaposto, *Recipient username tag*, immediatamente sotto l'etichetta GCM e limitato dai margini sinistro e destro.</span><span class="sxs-lookup"><span data-stu-id="c6371-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="c6371-127">Alcuni componenti sono stati aggiunti nell'esercitazione [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c6371-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="c6371-128">**CTRL** dai componenti nella visualizzazione a ViewController.h e aggiungere questi nuovi outlet.</span><span class="sxs-lookup"><span data-stu-id="c6371-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="c6371-129">In ViewController.h aggiungere l'elemento `#define` seguente sotto le istruzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="c6371-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="c6371-130">Sostituire il segnaposto *<Enter Your Backend Endpoint>\>* con l'URL di destinazione usato per distribuire il back-end dell'app nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="c6371-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="c6371-131">Ad esempio, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="c6371-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="c6371-132">Nel progetto creare una nuova **classe Cocoa Touch** denominata **RegisterClient** da usare come interfaccia con il back-end ASP.NET creato.</span><span class="sxs-lookup"><span data-stu-id="c6371-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="c6371-133">Creare la classe che eredita da `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="c6371-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="c6371-134">Aggiungere quindi il codice seguente in RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="c6371-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="c6371-135">In RegisterClient.m aggiornare la sezione `@interface` :</span><span class="sxs-lookup"><span data-stu-id="c6371-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="c6371-136">Sostituire la sezione `@implementation` in RegisterClient.m con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="c6371-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="c6371-137">Il codice riportato sopra implementa la logica illustrata nell'articolo di istruzioni [Registrazione dal back-end dell'app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) usando NSURLSession per eseguire chiamate REST al back-end dell'app e NSUserDefaults per archiviare in locale l'ID registrazione restituito dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c6371-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="c6371-138">Si noti che per il corretto funzionamento di questa classe è necessario che sia impostata la relativa proprietà **authorizationHeader** .</span><span class="sxs-lookup"><span data-stu-id="c6371-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="c6371-139">Questa proprietà viene impostata tramite la classe **ViewController** dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c6371-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="c6371-140">In ViewController.h aggiungere un'istruzione `#import` per RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="c6371-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="c6371-141">Aggiungere quindi una dichiarazione per il token del dispositivo e fare riferimento a un'istanza di `RegisterClient` nella sezione `@interface`:</span><span class="sxs-lookup"><span data-stu-id="c6371-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="c6371-142">In ViewController.m aggiungere una dichiarazione di metodo privato nella sezione `@interface` :</span><span class="sxs-lookup"><span data-stu-id="c6371-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="c6371-143">Il frammento seguente non è uno schema di autenticazione sicuro. È consigliabile sostituire l'implementazione di **createAndSetAuthenticationHeaderWithUsername:AndPassword:** con il meccanismo di autenticazione specifico che genera un token di autenticazione che deve essere usato dalla classe client di registrazione, ad esempio OAuth o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6371-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="c6371-144">Aggiungere quindi nella sezione `@implementation` di ViewController.m il codice seguente che aggiunge l'implementazione per l'impostazione del token del dispositivo e dell'intestazione di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c6371-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="c6371-145">Si noti come impostando il token del dispositivo viene abilitato il pulsante di accesso.</span><span class="sxs-lookup"><span data-stu-id="c6371-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="c6371-146">Questo dipende dal fatto che, nell'ambito dell'azione di accesso, il controller di visualizzazione esegue la registrazione per le notifiche push con il back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="c6371-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="c6371-147">L'azione di accesso deve quindi essere accessibile solo dopo che il token del dispositivo è stato correttamente configurato.</span><span class="sxs-lookup"><span data-stu-id="c6371-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="c6371-148">È possibile separare l'accesso dalla registrazione push, purché la prima azione avvenga prima della seconda.</span><span class="sxs-lookup"><span data-stu-id="c6371-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="c6371-149">In ViewController.m usare i frammenti di codice seguenti per implementare il metodo di azione per il pulsante **Log In** e un metodo per inviare il messaggio di notifica con il back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c6371-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="c6371-150">(IBAction) LogInAction: mittente (id) {/ / crea l'intestazione di autenticazione e impostate nel registro client NSString * username = self. UsernameField.text;   Password NSString * = self. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="c6371-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="c6371-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="c6371-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="c6371-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tag: nil andCompletion:^(NSError* error) {Se (! errore) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correttamente!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="c6371-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="c6371-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="c6371-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="c6371-154">Passare il tag pns e il nome utente come parametri con l'URL di REST per il back-end ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="c6371-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="c6371-155">Richiesta NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [richiesta setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="c6371-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="c6371-156">Ottenere la simulazione authenticationheader dal client register NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [richiesta setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="c6371-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="c6371-157">Aggiungere il corpo del messaggio di notifica [richiesta setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [richiesta setHTTPBody: [messaggi dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="c6371-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="c6371-158">Eseguire l'API REST di inviare una notifica su dataTask NSURLSessionDataTask back-end ASP.NET * = [completionHandler:^(NSData *data, NSURLResponse *response, NSError  *di dataTaskWithRequest:request sessione Errore) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) risposta.        Se (errore | | HttpResponse. StatusCode! = 200) {NSString* stato = [NSString stringWithFormat:@"Error stato per % @: % d\nError: %@\n", pns, HttpResponse. StatusCode, errore];            dispatch_async(dispatch_get_main_queue(), ^ {/ / aggiungere testo, in quanto tutte le chiamate PNS 3 potrebbero inoltre disporre delle informazioni alla visualizzazione [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="c6371-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="c6371-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="c6371-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="c6371-160">Aggiornare l'azione per il pulsante **Send Notification** per usare il back-end ASP.NET e inviare a qualsiasi PNS abilitato da un'opzione.</span><span class="sxs-lookup"><span data-stu-id="c6371-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="c6371-161">Nella funzione **ViewDidLoad**aggiungere quanto segue per creare l'istanza di RegisterClient e impostare il delegato per i campi di testo.</span><span class="sxs-lookup"><span data-stu-id="c6371-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="c6371-162">In **AppDelegate.m** rimuovere tutto il contenuto del metodo **application:didRegisterForPushNotificationWithDeviceToken:** e sostituirlo con il seguente per assicurarsi che il controller di visualizzazione contenga il token del dispositivo più recente recuperato dagli APN:</span><span class="sxs-lookup"><span data-stu-id="c6371-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="c6371-163">Infine in **AppDelegate.m**verificare che sia presente il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="c6371-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="c6371-164">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="c6371-164">Test the Application</span></span>
1. <span data-ttu-id="c6371-165">In XCode eseguire l'app su un dispositivo iOS fisico (le notifiche push non funzioneranno nel simulatore).</span><span class="sxs-lookup"><span data-stu-id="c6371-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="c6371-166">Nell'interfaccia utente dell'app per iOS immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="c6371-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="c6371-167">Può trattarsi di qualsiasi stringa, ma devono avere entrambi lo stesso valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="c6371-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="c6371-168">Quindi fare clic su **Log In**.</span><span class="sxs-lookup"><span data-stu-id="c6371-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="c6371-169">Verrà visualizzata una finestra popup che informa che la registrazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c6371-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="c6371-170">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6371-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="c6371-171">Nel campo di testo **Recipient username tag* (Tag nome utente destinatario) immettere il tag del nome utente usato con la registrazione da un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c6371-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="c6371-172">Immettere un messaggio di notifica e fare clic su **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="c6371-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="c6371-173">Solo i dispositivi che hanno una registrazione con il tag del nome utente del destinatario riceveranno il messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="c6371-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="c6371-174">Viene inviato solo a tali utenti.</span><span class="sxs-lookup"><span data-stu-id="c6371-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
