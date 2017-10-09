---
title: aaaAdd Accedi tooan iOS applicazione usando hello endpoint v 2.0 di Azure AD | Documenti Microsoft
description: Come toobuild un'app iOS che accede agli utenti con entrambi account Microsoft personale e gli account aziendali o dell'istituto di istruzione tramite le librerie di terze parti.
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Aggiungere app per iOS tooan Accedi con l'API Graph utilizzando hello v 2.0 endpoint di una libreria di terze parti
piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect. Gli sviluppatori possono utilizzare qualsiasi libreria desiderano toointegrate grazie ai servizi. gli sviluppatori di toohelp utilizzano la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come piattaforma delle identità Microsoft tooconnect toohello tooconfigure librerie di terze parti. La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) possono connettersi toohello piattaforma delle identità Microsoft.

Con un'applicazione hello creati in questa procedura dettagliata, gli utenti possono accedere tootheir organizzazione e quindi cercare altri utenti nell'organizzazione utilizzando hello API Graph.

Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questa configurazione di esempio può non avere senso tooyou. Per informazioni, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

> [!NOTE]
> Alcune funzionalità di piattaforma che dispone di un'espressione in hello OAuth2 o OpenID Connect standard, ad esempio l'accesso condizionale e gestione di criteri di Intune, richiedono si toouse l'open source di librerie di identità di Microsoft Azure.
> 
> 

endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità.

> [!NOTE]
> toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Scaricare il codice da GitHub
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o scheletro hello clone:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

È possibile anche scaricare l'esempio di hello e iniziare subito:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire hello i passaggi dettagliati in [come un'app con endpoint v 2.0 hello tooregister](active-directory-v2-app-registration.md).  Verificare di:

* Hello copia **Id applicazione** che è assegnato tooyour app perché è necessario prima.
* Aggiungere hello **Mobile** piattaforma per l'app.
* Hello copia **URI di reindirizzamento** dal portale hello. È necessario utilizzare il valore predefinito hello di `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Scaricare libreria NXOAuth2 di terze parti hello e creare un'area di lavoro
Questa procedura dettagliata, si utilizzerà hello OAuth2Client da GitHub, che è una libreria OAuth2 per Mac OS X e iOS (Cocoa e Cocoa touch). Questa libreria è basata sulla bozza 10 della specifica OAuth2 hello. Implementa il profilo di applicazione nativa hello e supporta l'endpoint di autorizzazione hello dell'utente hello. Questi sono tutti aspetti di hello, occorre toointegrate con la piattaforma di identità Microsoft hello.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Aggiungi progetto di libreria di tooyour hello utilizzando CocoaPods
CocoaPods è un gestore delle dipendenze per i progetti Xcode. Gestisce automaticamente i passaggi di installazione precedente hello.

```
$ vi Podfile
```
1. Aggiungere hello toothis podfile seguenti:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Caricare hello podfile mediante CocoaPods. Verrà creata una nuova area di lavoro Xcode da caricare.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Esplorare la struttura del progetto hello hello
Hello seguente struttura è impostato per il progetto nella struttura hello:

* Una visualizzazione master con una ricerca UPN
* Una vista di dettaglio per i dati di hello sull'utente selezionato hello
* Una vista di account di accesso in cui un utente possa accedere nel grafico di hello toohello app tooquery

File toovarious nell'autenticazione di base tooadd hello verrà spostato. Altre parti di codice hello, ad esempio di codice visual hello, non pertinenti tooidentity ma vengono forniti per l'utente.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Impostare il file settings.plst hello nella libreria hello
* Nel progetto di avvio rapido hello, aprire hello `settings.plist` file. Sostituire i valori hello elementi hello in hello sezione tooreflect hello valori utilizzati in hello portale di Azure. Il codice farà riferimento a questi valori ogni volta che viene utilizzato Active Directory Authentication Library hello.
  * Hello `clientId` hello client ID dell'applicazione copiata dal portale hello.
  * Hello `redirectUri` è l'URL di reindirizzamento hello tale portale hello fornito.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Impostare la libreria NXOAuth2Client hello nel LoginViewController
libreria NXOAuth2Client Hello richiede tooget alcuni valori impostato. Dopo avere completato questa attività, è possibile utilizzare hello toocall token acquisito hello API Graph. Poiché `LoginView` verrà chiamato ogni volta che è necessario tooauthenticate, avrebbe senso tooput i valori di configurazione nel file toothat.

* Aggiungere alcuni valori toohello `LoginViewController.m` contesto hello tooset di file per l'autenticazione e autorizzazione. Dettagli sui valori hello seguono codice hello.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Esaminare i dettagli sul codice hello.

prima stringa Hello è per `scopes`.  Hello `User.Read` valore consente di profilo di base hello tooread di hello effettuato l'accesso utente.

Maggiori informazioni su tutti gli ambiti disponibili hello in [gli ambiti di autorizzazione di Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Per `authURL`, `loginURL`, `bhh`, e `tokenURL`, è consigliabile utilizzare valori hello forniti in precedenza. Se si usa l'open source di hello librerie di identità di Microsoft Azure, è abbassare questi dati per l'utente tramite l'endpoint dei metadati. Che abbiamo realizzato operazioni di estrazione di questi valori si hello.

Hello `keychain` valore è contenitore hello hello NXOAuth2Client libreria utilizzerà toocreate toostore un portachiavi dei token. Se si desidera tooget single sign-on (SSO) in numerose applicazioni, è possibile specificare hello stesso portachiavi in ognuna delle applicazioni e richiedere l'uso hello di tale portachiavi in Xcode diritti. Ciò è illustrato nella documentazione di Apple hello.

rest Hello di questi valori sono libreria hello toouse necessarie e creare posizioni di contesto di toohello toocarry valori.

### <a name="create-a-url-cache"></a>Creare una cache di URL
All'interno di `(void)viewDidLoad()`, che viene sempre chiamato dopo il caricamento della visualizzazione hello, codice hello primes una cache per l'utilizzo.

Aggiungere hello seguente codice:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Creare una visualizzazione Web per l'accesso
WebView può richiedere all'utente di hello di altri fattori come messaggio SMS (se configurata) o dall'utente toohello i messaggi di errore. Qui verranno configuri hello WebView e successivamente hello scrittura i callback di hello toohandle codice che verranno eseguito in hello WebView dai servizi di identità hello.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Eseguire l'override di autenticazione di hello WebView metodi toohandle
hello tootell WebView cosa accade quando un utente deve toosign in come descritto in precedenza, è possibile incollare hello seguente codice.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Scrivere codice toohandle hello risultato della richiesta OAuth2 hello
Hello codice riportato di seguito gestirà redirectURL hello restituiti da hello WebView. Se l'autenticazione non è riuscita, codice hello tenterà di nuovo. Nel frattempo, la libreria hello fornirà errore hello che è possibile vedere nella console di hello o gestire in modo asincrono.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Impostare hello contesto OAuth (denominata archivio account)
Qui è possibile chiamare `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` nell'archivio di hello account condiviso per ogni servizio che si desidera hello applicazione toobe in grado di tooaccess. tipo di account Hello è una stringa che viene utilizzata come identificatore per un determinato servizio. Poiché si accede hello API Graph, codice hello fa riferimento tooit come `"myGraphService"`. Impostare quindi un osservatore che indica quando nulla cambia con token hello. Dopo avere ottenuto il token hello, viene restituito hello utente indietro toohello `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Consente di impostare hello toosearch visualizzazione Master e visualizzare gli utenti di hello da hello API Graph
Un'applicazione Master-View-Controller (MVC) che visualizza i dati restituito nella griglia hello hello esula dall'ambito hello di questa procedura dettagliata e molte esercitazioni online spiegano come toobuild uno. Tutto questo codice è in file scheletro hello. Tuttavia, è necessario toodeal con poche operazioni nell'applicazione MVC:

* Intercept quando un utente digita un valore nel campo di ricerca hello
* Fornire un oggetto di dati back-toohello MasterView, pertanto può visualizzare i risultati di hello nella griglia hello

Queste operazioni verranno eseguite sotto.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Aggiungere un toosee di controllo se si è connessi
un'applicazione Hello non offre se hello utente non è connesso, pertanto se è già presente un token nella cache di hello è toocheck smart. Se non si reindirizza toohello LoginView per toosign utente hello in. Se si ricorderà, hello migliore modo toodo azioni quando si carica una visualizzazione è hello toouse `viewDidLoad()` metodo che fornisce Apple.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Aggiornare hello tabella vista quando vengono ricevuti dati
Quando si hello API Graph restituisce dati, è necessario dati hello toodisplay. Per semplicità, ecco tutte hello codice tooupdate hello alla tabella. Nel codice boilerplate MVC, è possibile incollare solo i valori corretti di hello.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Fornire un hello toocall modo API Graph, quando l'utente immette nel campo di ricerca hello
Quando un utente digita una ricerca nella casella hello, è necessario tooshove che su toohello API Graph. Hello `GraphAPICaller` classe, si compilerà nel seguente codice hello, separa le funzionalità di ricerca hello dalla presentazione hello. Per il momento opportuno scrivere codice hello feed qualsiasi toohello caratteri ricerca API Graph. A tale scopo occorre fornire un metodo denominato `lookupInGraph`, che accetta una stringa hello da toosearch per.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Scrivere un hello tooaccess di classe Helper API Graph
Si tratta di core hello dell'applicazione. Mentre rest hello inserimento di codice nel modello MVC predefinito di hello da Apple, qui scrivere grafico hello tooquery del codice come utente hello tipi e restituire quindi i dati. Ecco il codice hello e segue una spiegazione dettagliata.

### <a name="create-a-new-objective-c-header-file"></a>Creare un nuovo file di intestazione Objective C
File con nome hello `GraphAPICaller.h`e aggiungere hello seguente codice.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Qui è possibile osservare che si sta specificando un metodo che accetta una stringa e restituisce completionBlock. Questo completionBlock, come si può immaginare, aggiornerà hello tabella fornendo un oggetto con i dati inseriti in tempo reale come hello ricerche degli utenti.

### <a name="create-a-new-objective-c-file"></a>Creare un nuovo file Objective C
File con nome hello `GraphAPICaller.m`e aggiungere al metodo hello.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

Ora questo metodo verrà analizzato in dettaglio.

core Hello di questo codice è in hello `NXOAuth2Request`, metodo che accetta i parametri di hello che è già stato definito nel file settings.plist hello.

primo passaggio Hello è chiamata all'API Graph tooconstruct hello destra. Poiché si sta chiamando `/users`, si specifica che mediante l'aggiunta di risorse di API Graph toohello con versione di hello. Rende senso tooput in un file di impostazioni esterno perché questi può essere modificato con hello API evoluzione.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Successivamente, è necessario toospecify parametri che si fornirà anche toohello chiamata all'API Graph. È *molto importante* non inserire parametri hello nell'endpoint di risorse hello perché che viene eseguita la pulitura per tutti i caratteri conforme non URI in fase di esecuzione. Tutto il codice query debba essere fornito nei parametri hello.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Come si può notare, viene chiamato un metodo `convertParamsToDictionary` che non è ancora stato scritto. Di seguito farlo ora alla fine di hello del file hello:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Successivamente, è possibile utilizzare hello `NXOAuth2Request` nuovamente i dati di tooget metodo dall'API di hello in formato JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Infine, si esaminerà modalità di restituzione di dati di hello toohello MasterViewController. dati Hello restituisce come serializzato e deve toobe deserializzato e caricato in un oggetto che hello MainViewController può utilizzare. A tale scopo, è scheletro hello un `User.m/h` file che crea un oggetto utente. Inserire l'oggetto utente con le informazioni dal grafico hello.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Eseguire l'esempio hello
Se è stato utilizzato scheletro hello o seguito insieme a questa procedura dettagliata hello che dovrebbe essere in esecuzione l'applicazione. Avviare il simulatore hello e fare clic su **Accedi** toouse un'applicazione hello.

## <a name="get-security-updates-for-our-product"></a>Ottenere aggiornamenti della sicurezza per il prodotto
Si consiglia di notifiche quando gli eventi imprevisti di protezione si verificano visitando hello tooget [Security TechCenter](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

