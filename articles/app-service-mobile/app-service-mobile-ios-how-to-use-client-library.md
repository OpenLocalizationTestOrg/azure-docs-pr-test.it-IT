---
title: aaaHow tooUse iOS SDK per App mobili di Azure
description: Come tooUse iOS SDK per App mobili di Azure
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Come tooUse iOS libreria Client per App mobili di Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [iOS App mobili di Azure SDK][1]. Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end, creare una tabella e scaricare un progetto Xcode iOS preesistente. In questa Guida, l'attenzione su hello del client iOS SDK. toolearn ulteriori informazioni sugli hello SDK lato server per hello di back-end, vedere hello Server SDK oggetti.

## <a name="reference-documentation"></a>Documentazione di riferimento
Hello documentazione di riferimento per i client iOS hello SDK è disponibile in: [iOS App mobili di Azure Client riferimento][2].

## <a name="supported-platforms"></a>Piattaforme supportate
Hello iOS SDK supporta progetti Objective-C, progetti Swift 2.2 e 2.3 Swift progetti per iOS versione 8.0 o versioni successive.

l'autenticazione "server-flusso" Hello utilizza WebView per hello presentata l'interfaccia utente.  Se hello dispositivo non è in grado di toopresent una UI WebView, sarà necessario un altro metodo di autenticazione che è di fuori ambito hello del prodotto hello.  
Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.

## <a name="Setup"></a>Installazione e prerequisiti
In questa guida si presuppone che siano stati creati un backend e una tabella. Questa guida presuppone che la tabella hello con lo stesso schema come tabelle hello in tali esercitazioni. In questa guida si presuppone inoltre che nel codice, si faccia riferimento a `MicrosoftAzureMobile.framework` e si importi `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Procedura: creare Client
tooaccess un back-end di App mobili di Azure nel progetto, creare un `MSClient`. Sostituire `AppUrl` con URL app hello. È possibile lasciare `gatewayURLString` e `applicationKey` vuoti. Se si configura un gateway per l'autenticazione, popolare `gatewayURLString` con hello gateway URL.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Procedura: Creare un riferimento alla tabella
tooaccess o l'aggiornamento dati, creare una tabella di riferimento toohello back-end. Sostituire `TodoItem` con nome hello della tabella

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Procedura: Eseguire query sui dati
toocreate una query sul database, hello query `MSTable` oggetto. Hello query seguente vengono ottenuti tutti gli elementi di hello in `TodoItem` e registri di hello testo di ogni elemento.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Procedura: Filtrare i dati restituiti
risultati toofilter, sono disponibili numerose opzioni disponibili.

toofilter utilizzando un predicato, utilizzare un `NSPredicate` e `readWithPredicate`. esempio Hello Filtra elementi di dati restituiti toofind solo incompleti Todo.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Procedura: Usare MSQuery
creare una query complessa, incluso l'ordinamento e paging, tooperform un `MSQuery` dell'oggetto, direttamente o tramite un predicato:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` consente di controllare diversi comportamenti di query.

* Specificare l'ordine dei risultati
* Limite quali campi tooreturn
* Limitare il numero di record tooreturn
* Specificare il conteggio totale nella risposta
* Specificare i parametri della stringa di query personalizzata nella richiesta
* Applicare funzioni aggiuntive

Eseguire un `MSQuery` query chiamando `readWithCompletion` sull'oggetto hello.

## <a name="sorting"></a>Procedura: Ordinare i dati con MSQuery
risultati toosort, esaminiamo un esempio. richiamare toosort dal testo' campo' crescente e decrescente 'completato', `MSQuery` come illustrato di seguito:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Procedura: Limitare i campi ed espandere i parametri di query di tipo stringa con MSQuery
toolimit toobe di campi restituiti in una query, specificare nomi hello di campi di hello in hello **selectFields** proprietà. Questo esempio viene restituito solo il testo hello e campi completati:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**:

```
query.selectFields = ["text", "complete"]
```

parametri di stringa di query aggiuntive tooinclude in server hello richiedono (ad esempio, perché li utilizza uno script sul lato server personalizzato), popolare `query.parameters` come illustrato di seguito:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Procedura: Configurare la dimensione di pagina
Con App mobili di Azure, i controlli di dimensioni pagina hello hello numero di record che vengono estratti in un momento dalle tabelle di hello back-end. Mediante una chiamata troppo`pull` dati vengono quindi batch dei dati, in base alle dimensioni di questa pagina, fino a quando non esistono alcun ulteriori toopull record.

È possibile tooconfigure una dimensione di pagina utilizzando **MSPullSettings** come illustrato di seguito. dimensioni di pagina predefinite Hello sono 50 ed esempio hello seguente modifica too3.

È possibile configurare una dimensione di pagina diversa per finalità di prestazioni. Se si dispone di un numero elevato di record di dati di piccole dimensioni, dimensioni pagina elevata riducono il numero di hello di andata e ritorno di server.

Questa impostazione controlla solo hello dimensione di paging sul lato client hello. Se hello client richiede una dimensione di pagina maggiore rispetto a supportato dal back-end App per dispositivi mobili hello, dimensioni della pagina hello limitate a back-end hello massimo hello è toosupport configurato.

Questa impostazione è anche hello *numero* dei record di dati non hello *dimensioni in byte*.

Se si aumentano le dimensioni di pagina client hello, è anche necessario aumentare la dimensione di pagina hello sul server hello. Vedere ["procedura: ridimensionare la paginazione tabella hello"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per hello passaggi toodo questo.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Procedura: Inserire dati
creare una nuova riga di tabella, tooinsert un `NSDictionary` e richiamare `table insert`. Se [lo Schema dinamico] è abilitata, back-end per dispositivi mobili di Azure App Service hello generate automaticamente nuove colonne in base a hello `NSDictionary`.

Se `id` non viene fornito, back-end hello genera automaticamente un nuovo ID univoco. Fornire una propria `id` toouse indirizzi di posta elettronica, i nomi utente, valori personalizzati come ID. La specifica del proprio ID può semplificare l'esecuzione di join e la logica dei database aziendali.

Hello `result` contiene hello nuovo elemento è stato inserito. A seconda della logica di server, i dati modificati rispetto toowhat è stato passato toohello server o potrebbe disporre di ulteriori.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Procedura: Modificare dati
tooupdate una riga esistente, modificare un elemento e chiamare `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

In alternativa, fornire l'ID di riga hello e campo hello aggiornato:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Come minimo, hello `id` attributo deve essere impostato quando si eseguono aggiornamenti.

## <a name="deleting"></a>Procedura: Eliminare dati
toodelete un elemento, richiamare `delete` con elemento hello:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

In alternativa, eliminarlo specificando un ID di riga:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Come minimo, hello `id` attributo deve essere impostato quando si elimina apportato.

## <a name="customapi"></a>Procedura: Chiamare un'API personalizzata
Con un'API personalizzata è possibile esporre qualsiasi funzionalità di back-end. Non ha toomap tooa operazione di tabella. Non solo si ottengono maggiore controllo sulla messaggistica, è anche possibile lettura/set di intestazioni e cambiare formato del corpo della risposta hello. modalità di lettura toocreate un'API personalizzata nel back-end hello, toolearn [API personalizzate](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

chiamare un'API personalizzata, toocall `MSClient.invokeAPI`. richiesta di Hello e risposta contenuto vengono considerati come JSON. toouse altri tipi di supporti, [hello di utilizzare altri overload di `invokeAPI` ] [ 5].  toomake un `GET` richiesta invece di un `POST` richiesta, il parametro set `HTTPMethod` troppo`"GET"` e parametro `body` troppo`nil` (dal momento che le richieste GET non dispone dei corpi dei messaggi.) Se l'API personalizzata supporta altri verbi HTTP, modificare `HTTPMethod` in modo appropriato.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Procedura: registrazione delle notifiche multipiattaforma toosend push modelli
modelli tooregister, passare modelli con il **client.push registerDeviceToken** metodo nell'applicazione client.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

I modelli sono di tipo NSDictionary e possono contenere più modelli di hello seguente formato:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Tutti i tag vengono rimossi dalla richiesta di hello per la sicurezza.  i tag tooadd tooinstallations o modelli all'interno di installazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][4].  funzionamento delle notifiche toosend utilizzando questi modelli, registrati con [API degli hub di notifica][3].

## <a name="errors"></a>Procedura: Gestire gli errori
Quando si chiama un back-end mobile di servizio App di Azure, il blocco di completamento hello contiene un `NSError` parametro. Quando si verifica un errore, il parametro sarà diverso da Nil. Nel codice, si deve controllare questo parametro e gestire l'errore hello secondo le esigenze, come dimostrato nel precedente frammenti di codice hello.

file Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definisce le costanti hello `MSErrorResponseKey`, `MSErrorRequestKey`, e `MSErrorServerItemKey`. tooget toohello errore relativo a più dati:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Inoltre, il file hello definisce le costanti per ogni codice di errore:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Procedura: autenticare gli utenti con Active Directory Authentication Library hello
È possibile utilizzare gli utenti toosign di Active Directory Authentication Library (ADAL) hello in un'applicazione tramite Azure Active Directory. L'autenticazione di flusso client utilizzando un provider di identità SDK è preferibile toousing hello `loginWithProvider:completion:` metodo.  L'autenticazione del flusso client garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.

1. Configurare il back-end dell'app mobile per l'accesso AAD hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] [ 7] esercitazione. Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa. Per iOS, è consigliabile che hello URI di reindirizzamento del modulo hello `<app-scheme>://<bundle-id>`. Per ulteriori informazioni, vedere hello [delle Guide rapide iOS ADAL][8].
2. Installare ADAL usando Cocoapods. Modificare il hello tooinclude Podfile seguente definizione, la sostituzione **del progetto** con nome hello del progetto Xcode:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   e hello Pod:

        pod 'ADALiOS'
3. Utilizzando hello Terminal, eseguire `pod install` dalla directory hello contenente il progetto e quindi aprire l'area di lavoro Xcode hello generato (non il progetto hello).
4. Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso. In ogni esempio eseguire queste sostituzioni:

   * Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione. Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com. Questo valore può essere copiato da scheda dominio hello in Azure Active Directory in hello [portale di Azure classico].
   * Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili. È possibile ottenere l'ID client da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.
   * Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.
   * Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello. Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Procedura: autenticare gli utenti con hello SDK Facebook per iOS
È possibile utilizzare hello SDK Facebook per gli utenti di iOS toosign nell'applicazione con Facebook.  Mediante l'autenticazione di flusso un client è preferibile toousing hello `loginWithProvider:completion:` metodo.  l'autenticazione del client del flusso di Hello fornisce un'idea dell'esperienza utente più nativa e consente di personalizzare ulteriormente.

1. Configurare il back-end dell'app mobile per l'accesso Facebook seguendo il [come tooconfigure App del servizio per l'account di accesso Facebook] [ 9] esercitazione.
2. Installare hello SDK Facebook per iOS da hello seguente [SDK Facebook per iOS - Introduzione] [ 10] documentazione. Anziché creare un'app, è possibile aggiungere una registrazione esistente tooyour piattaforma iOS hello.
3. Documentazione di Facebook include codice Objective-C in hello App delegato. Se si utilizza **Swift**, è possibile utilizzare hello seguendo le traduzioni per appdelegate. SWIFT:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. In aggiunta tooadding `FBSDKCoreKit.framework` tooyour del progetto, aggiungere anche un riferimento troppo`FBSDKLoginKit.framework` in hello allo stesso modo.
5. Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Procedura: Autenticare gli utenti con Twitter Fabric for iOS
È possibile utilizzare l'infrastruttura per gli utenti di iOS toosign nell'applicazione in uso tramite Twitter. L'autenticazione del client del flusso è preferibile toousing hello `loginWithProvider:completion:` del metodo, fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.

1. Configurare il back-end dell'app mobile per l'accesso Twitter seguente hello [come tooconfigure App del servizio per l'account di accesso Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) esercitazione.
2. Per aggiungere il progetto di tooyour dell'infrastruttura di hello seguente [dell'infrastruttura per iOS - Introduzione] documentazione e l'impostazione TwitterKit.

   > [!NOTE]
   > Per impostazione predefinita, Fabric crea automaticamente un'applicazione Twitter. È possibile evitare la creazione di un'applicazione registrando hello chiave Consumer e segreto del cliente è stato creato in precedenza mediante hello frammenti di codice seguente.    In alternativa, è possibile sostituire la chiave Consumer hello e vedere la sezione valori segreto del cliente di fornire i valori da tooApp servizio con hello in hello [Dashboard infrastruttura]. Se si sceglie questa opzione, essere certi tooset hello callback URL tooa valore segnaposto, ad esempio `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Se si sceglie toouse segreti hello creato in precedenza, è possibile aggiungere hello tooyour codice delegato App seguenti:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Procedura: autenticare gli utenti con hello Google Accedi SDK per iOS
È possibile utilizzare hello Google Accedi SDK per gli utenti di iOS toosign nell'applicazione utilizzando un account di Google.  Google ha recentemente annunciato modifiche tootheir OAuth i criteri di sicurezza.  Modifiche apportate ai criteri richiederà utilizzare hello del SDK di Google in hello future.

1. Configurare il back-end dell'app mobile per l'accesso Google hello seguente [come tooconfigure App del servizio per l'account di accesso Google](app-service-mobile-how-to-configure-google-authentication.md) esercitazione.
2. Installare hello Google SDK per iOS da hello seguente [Sign-In Google per iOS - avviare l'integrazione di](https://developers.google.com/identity/sign-in/ios/start-integrating) documentazione. È possibile ignorare una sezione "Eseguire l'autenticazione con un Server back-end" hello.
3. Aggiungere hello seguenti del delegato tooyour `signIn:didSignInForUser:withError:` (metodo), in base toohello lingua in uso.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Assicurarsi di aggiungere anche hello seguente troppo`application:didFinishLaunchingWithOptions:` nell'app, delegato, sostituendo "SERVER_CLIENT_ID" con hello ID che è stato utilizzato tooconfigure servizio App nel passaggio 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Aggiungere hello seguito codice tooyour applicazione in un UIViewController che implementa hello `GIDSignInUIDelegate` protocollo, in base toohello lingua in uso.  È stato disconnesso prima da firmare nuovamente e anche se non è necessario tooenter le credenziali di nuovo, viene visualizzato una finestra di dialogo di consenso.  Chiamare questo metodo solo quando il token di sessione hello è scaduto.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[avvio rapido di Azure Mobile app]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[lo Schema dinamico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[Dashboard infrastruttura]: https://www.fabric.io/home
[dell'infrastruttura per iOS - Introduzione]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
