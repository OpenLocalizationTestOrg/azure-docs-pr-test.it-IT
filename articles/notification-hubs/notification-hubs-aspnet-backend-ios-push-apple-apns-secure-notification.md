---
title: aaaAzure notifica hub Secure Push
description: Informazioni su come toosend sicura push notifiche tooan iOS app di Azure. Gli esempi di codice sono scritti in Objective-C e C#.
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Push sicuro degli hub di notifica di Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura push di semplice utilizzo, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.

A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello. In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra il dispositivo di client hello e back-end app hello.

In generale, il flusso di hello è il seguente:

1. Hello app back-end:
   * Archivia il payload sicuro nel database back-end.
   * Invia ID hello del dispositivo notifica toohello (viene inviata alcuna informazione protetta).
2. Hello app sul dispositivo hello, quando si riceve notifica hello:
   * dispositivo di Hello contatta hello back-end richiedente hello sicura payload.
   * app Hello possono mostrare payload hello come una notifica sul dispositivo hello.

È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso. In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token. Se l'applicazione non archivia i token di autenticazione nel dispositivo hello, o se i token possono essere scaduti, hello app del dispositivo, al momento della ricezione di notifiche di hello deve essere visualizzato una generica notifica conferma hello utente toolaunch hello app. app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.

Questa esercitazione Secure Push viene illustrato come toosend una notifica push in modo sicuro. Hello esercitazione si basa sulle hello [notifica utenti](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima.

> [!NOTE]
> In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Modificare il progetto di iOS hello
Ora che è stato modificato il hello solo toosend back-end di app *id* di una notifica, aver toochange il toohandle app iOS di notifica e chiamare nuovamente il hello tooretrieve back-end protetta toobe messaggio visualizzato.

tooachieve questo obiettivo, abbiamo toowrite hello logica tooretrieve hello contenuto protetto da hello app back-end.

1. In **appdelegate. M**, verificare che i registri applicazione hello per le notifiche invisibile all'utente in modo elabora l'id di notifica hello inviato dal back-end hello. Aggiungere hello **UIRemoteNotificationTypeNewsstandContentAvailability** opzione didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. Nel **appdelegate. M** aggiungere una sezione di implementazione nella parte superiore di hello con hello segue la dichiarazione:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Successivamente, aggiungere in hello di sezione implementazione hello codice seguente, sostituendo i segnaposto hello `{back-end endpoint}` con endpoint hello per il back-end ottenuto in precedenza:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. È ora dispongono di una notifica in ingresso toohandle hello e utilizzare il metodo hello sopra tooretrieve hello contenuto toodisplay. In primo luogo, abbiamo tooenable il toorun app iOS in background hello quando si riceve una notifica push. In **XCode**, selezionare il progetto di app nel riquadro di sinistra hello, quindi scegliere la destinazione dell'applicazione principale in hello **destinazioni** sezione dal riquadro centrale hello.
2. Quindi fare clic sui **funzionalità** scheda nella parte superiore di hello del riquadro centrale e verificare hello **notifiche remoto** casella di controllo.
   
    ![][IOS1]
3. In **appdelegate. M** aggiungere hello seguendo le notifiche push toohandle metodo:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    Si noti che è preferibile toohandle casi di hello di proprietà di intestazione di autenticazione mancante o il rifiuto da hello back-end. gestione di specifica Hello di questi casi dipendono principalmente l'esperienza utente di destinazione. È una notifica con un messaggio generico per notifica effettivo di hello utente tooauthenticate tooretrieve hello toodisplay.

## <a name="run-hello-application"></a>Eseguire l'applicazione hello
toorun applicazione hello, hello seguenti:

1. In XCode, eseguire l'applicazione hello in un dispositivo dei / o fisici (push delle notifiche non funzionerà nel simulatore hello).
2. Nell'app iOS hello dell'interfaccia utente, immettere un nome utente e password. Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.
3. Nell'app iOS hello dell'interfaccia utente, fare clic su **Accedi**. Fare clic su **Send push**. Dovrebbe essere hello protetto delle notifiche visualizzato nell'elenco il centro notifiche.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
