---
title: tooiOS di notifiche push aaaSending con gli hub di notifica di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure.
services: notification-hubs
documentationcenter: ios
keywords: notifica push,notifiche push,notifiche push ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>TooiOS l'invio di notifiche push con hub di notifica di Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Panoramica
> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Questa esercitazione illustra applicazione iOS tooan di notifiche push toouse toosend di hub di notifica di Azure. Creerai un'app iOS vuota che riceve le notifiche push tramite hello [servizio Apple Push Notification (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Al termine, sarà in grado di toouse il toobroadcast di hub di notifica push notifiche tooall hello che eseguono l'app.

## <a name="before-you-begin"></a>Prima di iniziare
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

codice Hello completata per questa esercitazione è disponibile [su GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* [iOS Mobile Services SDK versione 1.2.4]
* Ultima versione di [Xcode]
* Un dispositivo con iOS 8 o versione successiva.
* [Apple Developer Program](https://developer.apple.com/programs/) .
  
  > [!NOTE]
  > A causa dei requisiti di configurazione per le notifiche push, è necessario distribuire e testare le notifiche push in un dispositivo fisico iOS (iPhone o iPad) anziché simulatore iOS hello.
  > 
  > 

Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni di Hub di notifica relative ad app per iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Configurare l'hub di notifica per l'invio di notifiche push di iOS
In questa sezione viene illustrata la creazione di un nuovo hub di notifica e la configurazione dell'autenticazione con il servizio APN utilizzando hello **. p12** certificato push creato. Se si desidera toouse un hub di notifica che è già stato creato, è possibile ignorare toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Fare clic su hello <b>Notification Services</b> pulsante hello <b>impostazioni</b> pannello, quindi selezionare <b>Apple (APNS)</b>. Fare clic su <b>carica certificato</b> e seleziona hello <b>. p12</b> file esportato in precedenza. Assicurarsi di specificare anche la password corretta hello.</p>

<p>Verificare che tooselect <b>Sandbox</b> modalità poiché si tratta per lo sviluppo. Utilizzare solo hello <b>produzione</b> se si desidera toousers di notifiche push toosend che hanno acquistato l'app dall'archivio hello.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Configurare APNS nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Configurare il certificato APN nel portale di Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Hub di notifica è ora configurato toowork con il servizio APN e aver tooregister stringhe di connessione hello app e inviare notifiche push.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Connettere il tooNotification app iOS hub
1. In Xcode, creare un nuovo progetto di iOS e selezionare hello **singola visualizzazione applicazione** modello.
   
    ![Xcode - Single View Application][8]
    
2. Quando si impostano opzioni hello per il nuovo progetto, verificare che toouse hello stesso **Product Name** e **identificatore organizzazione** utilizzato quando si imposta in precedenza ID bundle hello in hello Apple Developer portale.
   
    ![Xcode - Opzioni di progetto][11]
    
3. In **destinazioni**, fare clic sul nome del progetto, fare clic su hello **Build Settings** scheda ed espandere **identità di firma codice**, quindi in **Debug**, impostare l'identità di firma codice. Attiva/disattiva **livelli** da **base** troppo**tutti**e impostare **profilo di Provisioning** toohello profilo creato in precedenza di provisioning .
   
    Se non viene visualizzato hello provisioning nuovo profilo creato in Xcode, provare ad aggiornare i profili di hello per le identità di firma. Fare clic su **Xcode** sulla barra dei menu hello, fare clic su **preferenze**, fare clic su hello **Account** scheda, fare clic su hello **Visualizza dettagli** fare clic sui identità di firma e quindi scegliere il pulsante di aggiornamento hello nell'angolo inferiore destro hello.
   
    ![Xcode - Profilo di provisioning][9]
4. Scaricare hello [iOS Mobile Services SDK versione 1.2.4] e decomprimere file hello. In Xcode, mouse sul progetto e fare clic su hello **aggiungere file alla** hello tooadd opzione **WindowsAzureMessaging.framework** progetto Xcode tooyour di cartella. Selezionare **Copy items if needed** (Copia elementi se necessario) e fare clic su **Add** (Aggiungi).
   
   > [!NOTE]
   > hub di notifica Hello SDK non supporta attualmente bitcode in Xcode 7.  È necessario impostare **abilitare Bitcode** troppo**n** in hello **le opzioni di compilazione** per il progetto.
   > 
   > 
   
    ![Decomprimere Azure SDK][10]
5. Aggiungere un nuovo progetto tooyour file di intestazione denominato `HubInfo.h`. Questo file contiene costanti hello per l'hub di notifica.  Aggiungere hello seguenti definizioni e sostituire i segnaposto di valore letterale stringa hello con il *nome hub* hello e *DefaultListenSharedAccessSignature* annotato in precedenza.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Aprire il `AppDelegate.h` file aggiungere hello seguenti direttive di importazione:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. Nel `AppDelegate.m file`, aggiungere hello seguente di codice hello `didFinishLaunchingWithOptions` metodo in base alla versione di iOS. Questo codice registra l'handle di dispositivo nel servizio APNS:
   
    Per iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Per too8 precedenti versioni di iOS:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. In hello stesso file, aggiungere hello dei seguenti metodi. Questo codice si connette l'hub di notifica toohello utilizzando hello informazioni di connessione specificato nel HubInfo.h. Fornisce quindi hub di notifica toohello token dispositivo hello in modo che hello hub di notifica è possibile inviare notifiche:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. In hello stesso file, aggiungere hello seguente metodo toodisplay un **UIAlert** se viene ricevuta notifica di hello mentre è attiva app hello:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Compilare ed eseguire l'applicazione hello in tooverify il dispositivo che non si verificano errori.

## <a name="send-test-push-notifications"></a>Inviare notifiche push di prova
È possibile verificare la ricezione di notifiche nell'app mediante l'invio di notifiche push in hello [portale Azure] tramite hello **Troubleshooting** sezione nel Pannello di hub hello (utilizzare hello *inviodiTest* opzione).

![Portale di Azure - Invio di prova][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Facoltativo) Inviare notifiche push da app hello
> [!IMPORTANT]
> Questo esempio l'invio di notifiche da app client hello viene fornito solo a scopo illustrativo. Poiché questo richiederà hello `DefaultFullSharedAccessSignature` toobe presente sull'app client hello, che espone il rischio di toohello hub di notifica che un utente può ottenere le notifiche di accesso non autorizzato toosend tooyour client.
> 
> 

Se si desidera toosend le notifiche push all'interno di un'app, in questa sezione viene fornito un esempio di come toodo questo utilizzando hello interfaccia REST.

1. In Xcode aprire `Main.storyboard` e aggiungere i seguenti componenti dell'interfaccia utente dagli hello oggetto libreria tooallow hello utente toosend notifiche push in app hello hello:
   
   * Etichetta senza testo. Sarà errori tooreport utilizzato per l'invio di notifiche. Hello **righe** proprietà deve essere impostata troppo**0** in modo che verrà ridimensionato automaticamente toohello vincolata destra e i margini sinistro e parte superiore di hello della visualizzazione hello.
   * Un campo di testo con **segnaposto** testo impostato troppo**messaggio di notifica immettere**. Vincolare campo hello immediatamente sotto l'etichetta di hello, come illustrato di seguito. Visualizzazione Controller hello come delegato presa hello.
   * Un pulsante denominato **invia una notifica** vincolata sotto il campo di testo hello e in centro orizzontale hello.
     
     visualizzazione di Hello dovrebbe apparire come segue:
     
     ![Finestra di progettazione Xcode][32]
2. [Aggiungere le prese](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) per il campo di testo ed etichetta hello connessi, la visualizzazione e aggiornare il `interface` definizione toosupport `UITextFieldDelegate` e `NSXMLParserDelegate`. Aggiungere hello tre dichiarazioni di proprietà indicate di seguito toohelp supporto chiamando hello API REST e l'analisi di risposta hello.
   
    Il file ViewController.h dovrebbe apparire come segue:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Aprire `HubInfo.h` e aggiungere i seguenti costanti che verranno utilizzate per l'invio di hub di notifiche tooyour hello. Sostituire l'effettivo valore letterale stringa segnaposto hello *DefaultFullSharedAccessSignature* stringa di connessione.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Aggiungere il seguente hello `#import` tooyour istruzioni `ViewController.h` file.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. In `ViewController.m` aggiungere hello implementazione dell'interfaccia toohello di codice seguente. Questo codice analizzerà la stringa di connessione *DefaultFullSharedAccessSignature* . Come accennato in hello [riferimento all'API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), queste informazioni analizzate saranno toogenerate usato un token di firma di accesso condiviso per hello **autorizzazione** intestazione della richiesta.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. In `ViewController.m`, hello aggiornamento `viewDidLoad` metodo tooparse hello stringa di connessione quando viene caricato vista hello. Aggiungere anche i metodi di utilità hello, illustrati di seguito, l'implementazione dell'interfaccia toohello.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. In `ViewController.m`, aggiungere hello seguente codice toohello interfaccia implementazione toogenerate hello SaS token di autenticazione che verrà fornito in hello **autorizzazione** intestazione, come indicato in hello [API REST Riferimento](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + trascinare da hello **invia una notifica di** pulsante troppo`ViewController.m` tooadd un'azione denominata **SendNotificationMessage** per hello **tocco premuto** evento. Metodo di aggiornamento con hello dopo la notifica di hello codice toosend mediante hello API REST.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. In `ViewController.m`, aggiungere hello seguente toosupport metodo delegato tastiera hello per il campo di testo hello di chiusura. CTRL + trascinare dalla hello testo campo toohello View Controller icona hello tooset della finestra di progettazione dell'interfaccia di hello Visualizza controller come delegato presa hello.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. In `ViewController.m`, aggiungere seguente hello delegare la risposta metodi toosupport analisi hello tramite `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Compilare il progetto hello e verificare che non siano presenti errori.

> [!NOTE]
> Se si verifica un errore di compilazione in Xcode7 sul supporto di bitcode, è necessario modificare hello **Build Settings** > **abilitare Bitcode (ENABLE_BITCODE)** troppo**n** in Xcode. Hello SDK hub di notifica non supporta attualmente bitcode. 
> 
> 

È possibile trovare tutti i payload di notifica possibili hello in hello Apple [locali e Guida per programmatori notifica Push].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Verifica della ricezione di notifiche push nell'app
le notifiche push tootest in iOS, è necessario distribuire dispositivi dei / o fisici tooa app hello. È possibile inviare notifiche push di Apple usando simulatore iOS hello.

1. Eseguire app hello e verificare che la registrazione ha esito positivo e quindi premere **OK**.
   
    ![Test di registrazione notifica push per app iOS][33]
2. È possibile inviare una notifica push di test da hello [portale Azure], come descritto in precedenza. Se è stato aggiunto il codice per l'invio di notifiche push in hello app, toccare tooenter campo di testo hello all'interno di un messaggio di notifica. Premere quindi hello **inviare** pulsante sulla tastiera di hello o hello **invia una notifica di** pulsante nel messaggio di notifica di hello vista toosend hello.
   
    ![Test di invio notifica push per app iOS][34]
3. Hello push notifica viene inviata tooall i dispositivi registrati tooreceive notifiche hello da hello determinato Hub di notifica.
   
    ![Test di ricezione notifica push per app iOS][35]

## <a name="next-steps"></a>Passaggi successivi
In questo semplice esempio, si trasmessa tooall le notifiche push con i dispositivi iOS registrati. Si consiglia di un passaggio successivo del learning procedere toohello [notifica hub di notifica gli utenti di Azure per iOS con back-end .NET] esercitazione che assiste nella creazione di un push toosend back-end le notifiche tramite tag. 

Se si desidera che gli utenti dai gruppi di interesse toosegment, è inoltre possibile spostare in toohello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione. 

Per informazioni generali su Hub di notifica, vedere [Panoramica dell'Hub di notifica].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[iOS Mobile Services SDK versione 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Panoramica dell'Hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[notifica hub di notifica gli utenti di Azure per iOS con back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[locali e Guida per programmatori notifica Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[portale Azure]: https://portal.azure.com
