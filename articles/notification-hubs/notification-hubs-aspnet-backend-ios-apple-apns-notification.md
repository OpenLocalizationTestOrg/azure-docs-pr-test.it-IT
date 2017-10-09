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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Uso di Hub di notifica di Azure per inviare notifiche agli utenti per iOS con back-end .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Panoramica
Supporto di notifica push in Azure consente tooaccess un semplice utilizzo, multipiattaforma e infrastruttura push di scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme. Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push utente app specifica tooa di notifiche in un dispositivo specifico. Un back-end ASP.NET WebAPI è tooauthenticate utilizzati client e le notifiche di toogenerate, come illustrato nell'argomento Guida hello [registrazione dal back-end app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). In questa esercitazione è anche hello prerequisiti toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) esercitazione.
> Se si desidera toouse App per dispositivi mobili come il servizio back-end, vedere hello [Mobile App introduzione Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modificare l'app per iOS
1. Aprire hello singola pagina Visualizza app è stato creato in hello [Introduzione agli hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) esercitazione.
   
   > [!NOTE]
   > In questa sezione si presuppone che il progetto sia configurato con un nome di organizzazione vuoto. In caso contrario, sarà necessario tooprepend i nomi di classe tooall nome dell'organizzazione.
   > 
   > 
2. Nel Main aggiungere componenti hello illustrati nella schermata di hello seguito dalla libreria di oggetti hello.
   
    ![][1]
   
   * **Nome utente**: UITextField A con il testo segnaposto, *immettere nome utente*, immediatamente di sotto di hello inviare etichetta risultati e toohello vincolata a sinistra e i margini destro e di sotto di hello inviare etichetta risultati.
   * **Password**: UITextField A con il testo segnaposto, *immettere la Password*, immediatamente sotto hello campo di testo Nome utente e toohello vincolata a sinistra e a destra i margini e di sotto di campo di testo Nome utente hello. Controllare hello **Secure testo** opzione nel controllo di attributo, hello in *restituire chiave*.
   * **Accedi**: UIButton A con l'etichetta immediatamente sotto il campo di testo password hello e deselezionare hello **abilitato** opzione nel controllo gli attributi, hello in *contenuto del controllo*
   * **WNS**: etichetta e l'invio di commutatore tooenable hello notifica il servizio di notifica di Windows se sia stata impostata su hub hello. Vedere hello [Windows Introduzione](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) esercitazione.
   * **GCM**: etichetta e l'invio di commutatore tooenable hello tooGoogle notifica messaggistica Cloud se sia stata impostata su hub hello. Vedere l'esercitazione [Introduzione ad Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .
   * **APNS**: etichetta e l'invio di commutatore tooenable hello notifica toohello Apple piattaforma Notification Service.
   * **Recipent Username**: UITextField A con il testo segnaposto, *tag username destinatario*immediatamente di sotto di hello GCM etichetta e vincolata toohello sinistro e destro margini e di sotto di hello GCM assegnare un'etichetta.

    Alcuni componenti sono stati aggiunti in hello [Introduzione agli hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) esercitazione.

1. **CTRL** trascinare componenti hello tooViewController.h visualizzazione hello e aggiungere questi punti vendita di nuovo.
   
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
2. In ViewController.h, aggiungere hello seguente `#define` subito dopo le istruzioni di importazione. Hello Substitute *< immettere l'Endpoint di back-end\>*  segnaposto con URL di destinazione utilizzato toodeploy back-end app nella sezione precedente hello hello. Ad esempio, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. Nel progetto, creare un nuovo **Cocoa tocco classe** denominato **RegisterClient** toointerface con hello ASP.NET back-end è stato creato. Creare l'eredità dalla classe hello `NSObject`. Aggiungere quindi hello seguente di codice hello RegisterClient.h.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. In hello RegisterClient.m aggiornare hello `@interface` sezione:
   
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
5. Sostituire hello `@implementation` sezione hello RegisterClient.m con hello seguente codice.

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

    codice Hello precedente implementa la logica di hello descritto nell'articolo Guida hello [registrazione dal back-end app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) utilizzando NSURLSession tooperform REST chiama back-end app tooyour e NSUserDefaults toolocally archivio hello registrationId restituito dall'hub di notifica hello.

    Si noti che questa classe richiede la relativa proprietà **authorizationHeader** toobe set in ordine toowork correttamente. Questa proprietà è impostata tramite hello **ViewController** classe dopo l'accesso hello.

1. In ViewController.h aggiungere un'istruzione `#import` per RegisterClient.h. Quindi aggiungere una dichiarazione di token del dispositivo hello e fare riferimento a tooa `RegisterClient` istanza in hello `@interface` sezione:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. In ViewController.m, aggiungere una dichiarazione di metodo privato in hello `@interface` sezione:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Hello frammento seguente non è uno schema di autenticazione sicura, è necessario sostituire l'implementazione di hello di hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** con il meccanismo di autenticazione specifico viene generato un toobe token di autenticazione utilizzato da hello register classe client, ad esempio OAuth, Active Directory.
> 
> 

1. Quindi in hello `@implementation` sezione di ViewController.m aggiungere hello seguente di codice che aggiunge l'implementazione di hello per impostazione hello dispositivo token e l'autenticazione dell'intestazione.
   
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
   
    Si noti come token del dispositivo hello impostazione consenta hello pulsante Accedi. In questo modo come parte dell'azione di account di accesso hello, controller di visualizzazione hello registra le notifiche push con back-end app hello. Di conseguenza, non è desiderabile che accedi toobe azione accessibile fino a quando i token del dispositivo hello è stato impostato correttamente. È possibile separare hello Accedi dalla registrazione push hello come primo hello si verifica prima hello quest'ultimo.
2. In ViewController.m, utilizzare hello seguente metodo di azione hello tooimplement frammenti di codice per il **Accedi** pulsante e un metodo toosend hello messaggio di notifica tramite hello back-end ASP.NET.
   
       - (IBAction) LogInAction: mittente (id) {/ / crea l'intestazione di autenticazione e impostate nel registro client NSString * username = self. UsernameField.text;   Password NSString * = self. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tag: nil andCompletion:^(NSError* error) {Se (! errore) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correttamente!"];});}}];}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Passare i tag di hello pns e il nome utente come parametri con hello URL REST toohello back-end ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            Richiesta NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [richiesta setHTTPMethod:@"POST"];

            Ottenere hello fittizio authenticationheader dal client register hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [richiesta setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            Aggiungere il corpo di messaggio di notifica hello [richiesta setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [richiesta setHTTPBody: [messaggi dataUsingEncoding:NSUTF8StringEncoding]];

            Eseguire hello invia notifica API REST su hello ASP.NET back-end NSURLSessionDataTask * dataTask = [completionHandler:^(NSData *data, NSURLResponse *response, NSError  *di dataTaskWithRequest:request sessione Errore) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) risposta.        Se (errore | | HttpResponse. StatusCode! = 200) {NSString* stato = [NSString stringWithFormat:@"Error stato per % @: % d\nError: %@\n", pns, HttpResponse. StatusCode, errore];            dispatch_async(dispatch_get_main_queue(), ^ {/ / aggiungere testo, poiché tutte le chiamate PNS 3 possono anche avere informazioni tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Aggiornare l'azione di hello per hello **invia una notifica** pulsante back-end ASP.NET di hello toouse e inviare tooany PNS abilitato per un commutatore.

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



1. Nella funzione **ViewDidLoad**, aggiungere hello successivo tooinstantiate hello RegisterClient istanza e impostare hello delegato per i campi di testo.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Ora in **appdelegate. M**, rimuovere tutto il contenuto del metodo hello hello **applicazione: didRegisterForPushNotificationWithDeviceToken:** e sostituirlo con hello seguente toomake assicurarsi che hello vista controller contiene hello più recente token del dispositivo recuperati dal servizio APN:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Infine in **appdelegate. M**, assicurarsi di avere hello seguente metodo:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Hello test dell'applicazione
1. In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).
2. Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e password. Può trattarsi di qualsiasi stringa, ma devono essere entrambi hello stesso valore di stringa. Quindi fare clic su **Log In**.
   
    ![][2]
3. Verrà visualizzata una finestra popup che informa che la registrazione è stata completata. Fare clic su **OK**.
   
    ![][3]
4. In hello **tag username destinatario* testo immettere i tag del nome utente hello utilizzato con la registrazione di hello da un altro dispositivo.
5. Immettere un messaggio di notifica e fare clic su **Send Notification**.  Solo i dispositivi di hello che dispone di una registrazione con tag del nome utente destinatario hello ricevono il messaggio di notifica hello.  Viene inviato solo gli utenti toothose.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
