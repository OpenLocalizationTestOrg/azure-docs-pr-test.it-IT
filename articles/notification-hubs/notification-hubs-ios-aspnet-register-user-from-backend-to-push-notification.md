---
title: Registrare l'utente corrente per le notifiche push mediante l'API Web | Documentazione Microsoft
description: Informazioni su come chiedere la registrazione per le notifiche push in un'app per iOS con Hub di notifica di Azure quando la registrazione viene eseguita mediante l'API Web ASP.NET.
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
ms.openlocfilehash: fd56bb2dd627b31f00363851a4e76484aa382988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a>Registrazione dell'utente corrente per le notifiche push mediante ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
Questo argomento illustra come richiedere la registrazione per le notifiche push con Hub di notifica di Azure quando la registrazione viene eseguita mediante l'API Web ASP.NET. In questo argomento viene estesa l'esercitazione [Utilizzo di Hub di notifica per inviare notifiche agli utenti]. Per creare il servizio mobile autenticato è necessario aver già completato i passaggi richiesti in tale esercitazione. Per ulteriori informazioni sullo scenario di notifica agli utenti, vedere [Utilizzo di Hub di notifica per inviare notifiche agli utenti].

## <a name="update-your-app"></a>Aggiornamento dell'app
1. Nel file MainStoryboard_iPhone.storyboard aggiungere i componenti seguenti dalla libreria di oggetti:
   
   * **Etichetta**: "Push to User with Notification Hubs"
   * **Etichetta**: "InstallationId"
   * **Etichetta**: "User"
   * **Campo di testo**: "User"
   * **Etichetta**: "Password"
   * **Campo di testo**: "Password"
   * **Pulsante**: "Login"
     
     A questo punto lo storyboard avrà un aspetto simile al seguente:
     
      ![][0]
2. Nell'assistente dell'editor creare outlet per tutti i controlli con opzioni e chiamarli, collegare i campi di testo per mezzo dell'elemento View Controller (delegato), quindi creare una connessione di tipo **Action** per il pulsante **login**.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Creare una classe denominata **DeviceInfo**e copiare il codice seguente nella sezione dell'interfaccia del file DeviceInfo.h:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Copiare il codice seguente nella sezione di implementazione del file DeviceInfo.m:
   
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
   
                    //store the install ID so we don't generate a new one next time
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
5. In PushToUserAppDelegate.h aggiungere il singleton della proprietà seguente:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Nel metodo **didFinishLaunchingWithOptions** di PushToUserAppDelegate.m aggiungere il codice seguente:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    La prima riga inizializza il singleton **DeviceInfo** . La seconda riga avvia la registrazione per le notifiche push, che è già presente se si è completata l'esercitazione [Introduzione ad Hub di notifica] .
7. In PushToUserAppDelegate.m implementare il metodo **didRegisterForRemoteNotificationsWithDeviceToken** nel delegato dell'app e aggiungere il codice seguente:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Questo codice consente di impostare il token di dispositivo per la richiesta.
   
   > [!NOTE]
   > A questo punto, il metodo non dovrebbe contenere altro codice. Se è già presente una chiamata al metodo **registerNativeWithDeviceToken** aggiunto durante l'esercitazione [Introduzione ad Hub di notifica](/manage/services/notification-hubs/get-started-notification-hubs-ios/) , è necessario impostare la chiamata come commento oppure rimuoverla.
   > 
   > 
8. Nel file PushToUserAppDelegate.m aggiungere il metodo del seguente gestore:
   
   * applicazione (void):(UIApplication *) applicazione didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", userInfo);   UIAlertView * avviso = [[UIAlertView alloc] initWithTitle:@"Notification" messaggio: cancelButtonTitle delegato: nil [userInfo objectForKey:@"inAppMessage"]: @ otherButtonTitles:nil "OK", null];   [avviso Mostra]; }
   
   Questo metodo visualizza un avviso nell'interfaccia utente quando l'app riceve notifiche mentre è in esecuzione.
9. Aprire il file PushToUserViewController.m e restituire la tastiera nell'implementazione seguente:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Nel metodo **viewDidLoad** di PushToUserViewController.m inizializzare l'etichetta installationId come segue:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. In PushToUserViewController.m aggiungere le proprietà seguenti nell'interfaccia:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Aggiungere quindi l'implementazione seguente:
    
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
13. Copiare il codice seguente nel metodo del gestore **login** creato da XCode:
    
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
    
    Questo metodo ottiene un ID di installazione e un canale per le notifiche push e li invia, insieme al tipo di dispositivo, al metodo API Web di autenticazione che crea una registrazione in Hub di notifica. Questa API Web è stata definita in [Utilizzo di Hub di notifica per inviare notifiche agli utenti].

Ora che l'app client è stata aggiornata, tornare a [Utilizzo di Hub di notifica per inviare notifiche agli utenti] e aggiornare il servizio mobile per l'invio di notifiche con Hub di notifica.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[Utilizzo di Hub di notifica per inviare notifiche agli utenti]: /manage/services/notification-hubs/notify-users-aspnet

[Introduzione ad Hub di notifica]: /manage/services/notification-hubs/get-started-notification-hubs-ios
