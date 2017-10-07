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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>Registrare l'utente corrente di hello per le notifiche push tramite ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
Questo argomento viene illustrato come toorequest push registrazione della notifica con gli hub di notifica di Azure quando la registrazione viene eseguita da ASP.NET Web API. In questo argomento estende esercitazione hello [notificare agli utenti con gli hub di notifica]. È necessario stati già completati i passaggi necessario hello nel servizio mobile toocreate esercitazione hello autenticato. Per ulteriori informazioni su hello notificare scenario gli utenti, vedere [notificare agli utenti con gli hub di notifica].

## <a name="update-your-app"></a>Aggiornamento dell'app
1. Nel MainStoryboard_iPhone.storyboard, aggiungere hello seguendo i componenti dalla libreria di oggetti hello:
   
   * **Etichetta**: "TooUser con gli hub di notifica Push"
   * **Etichetta**: "InstallationId"
   * **Etichetta**: "User"
   * **Campo di testo**: "User"
   * **Etichetta**: "Password"
   * **Campo di testo**: "Password"
   * **Pulsante**: "Login"
     
     A questo punto lo storyboard è simile hello seguenti:
     
      ![][0]
2. Nell'editor di Assistente hello, creare prese per tutti i controlli di hello commutato e chiamarli, collegare i campi di testo hello con hello View Controller (delegato) e creare un **azione** per hello **accesso** pulsante.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Creare una classe denominata **DeviceInfo**, e hello copia seguente codice nella sezione dell'interfaccia hello del file hello DeviceInfo.h:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Copiare hello seguente codice nella sezione di implementazione hello del file DeviceInfo.m hello:
   
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
5. In PushToUserAppDelegate.h, aggiungere hello singleton di proprietà seguenti:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. In hello **didFinishLaunchingWithOptions** metodo PushToUserAppDelegate.m, aggiungere hello seguente codice:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    prima riga Hello Inizializza hello **DeviceInfo** singleton. Hello seconda riga inizia hello per le notifiche push, che è già presente è registrazione sono stati già completati hello [iniziare con gli hub di notifica] esercitazione.
7. In PushToUserAppDelegate.m, implementare il metodo hello **didRegisterForRemoteNotificationsWithDeviceToken** nel AppDelegate e aggiungere hello seguente codice:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Consente di impostare token del dispositivo per la richiesta di hello hello.
   
   > [!NOTE]
   > A questo punto, il metodo non dovrebbe contenere altro codice. Se si dispone già di una chiamata toohello **registerNativeWithDeviceToken** metodo che è stato aggiunto al termine di hello [iniziare con gli hub di notifica](/manage/services/notification-hubs/get-started-notification-hubs-ios/) dell'esercitazione, è necessario commento o rimuovere chiamata.
   > 
   > 
8. Nel file hello PushToUserAppDelegate.m aggiungere hello seguente metodo del gestore:
   
   * applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * avviso = [[UIAlertView alloc] initWithTitle:@"Notification" messaggio: cancelButtonTitle delegato: nil [userInfo objectForKey:@"inAppMessage"]: @ otherButtonTitles:nil "OK", null];   [avviso Mostra]; }
   
   Questo metodo visualizza un avviso in hello dell'interfaccia utente quando l'applicazione riceve notifiche durante l'esecuzione.
9. Aprire file PushToUserViewController.m hello e tastiera restituito hello in seguito all'implementazione hello:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. In hello **viewDidLoad** metodo nel file hello PushToUserViewController.m inizializzare etichetta installationId hello come indicato di seguito:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Aggiungere le proprietà nell'interfaccia in PushToUserViewController.m seguenti hello:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Aggiungere quindi hello implementazione seguente:
    
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
13. Copia hello esempio di codice in hello **accesso** creato da XCode metodo del gestore:
    
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
    
    Questo metodo ottiene l'ID di installazione sia un canale per le notifiche push e lo invia, insieme a tipo di dispositivo hello, toohello autenticato metodo API Web che crea una registrazione di hub di notifica. Questa API Web è stata definita in [notificare agli utenti con gli hub di notifica].

Ora che hello client app è stata aggiornata, restituire toohello [notificare agli utenti con gli hub di notifica] e hello servizio mobile toosend notifiche di aggiornamento con gli hub di notifica.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificare agli utenti con gli hub di notifica]: /manage/services/notification-hubs/notify-users-aspnet

[iniziare con gli hub di notifica]: /manage/services/notification-hubs/get-started-notification-hubs-ios
