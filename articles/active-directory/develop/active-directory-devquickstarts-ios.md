---
title: aaaIntegrate AD Azure in un'app iOS | Documenti Microsoft
description: Come un'applicazione iOS che si integra con Azure AD per l'accesso e le chiamate AD Azure toobuild protetto API tramite OAuth.
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Integrare Azure AD in un'app iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consente di ottenere in esecuzione con Azure Active Directory in pochi minuti.  portale per sviluppatori Hello in modo semplificato il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice.  Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida. 
> 
> 

Azure Active Directory (Azure AD) offre hello Active Directory Authentication Library o ADAL, per i client iOS necessarie tooaccess risorse protette. ADAL semplifica il processo di hello che l'app Usa i token di accesso tooobtain. toodemonstrate facilmente, in questo articolo è compilare un'applicazione elenco attività di Objective C:

* Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Cerca in una directory gli utenti con un determinato alias.

toobuild hello completo lavoro dell'applicazione, è necessario:

1. Registrare l'applicazione con Azure AD.
2. Installare e configurare ADAL.
3. Usare i token ADAL tooget da Azure AD.

tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione. Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).


> [!TIP]
> Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consentono di ottenere in esecuzione in Azure AD in pochi minuti. portale per sviluppatori Hello in modo semplificato il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice. Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Determinare qual è l'URI di reindirizzamento per iOS
toosecurely avviare le applicazioni in determinati scenari SSO, è necessario creare un *URI di reindirizzamento* in un formato specifico. Un reindirizzamento URI viene usato tooensure che hello token restituito toohello corretta applicazione che ha richiesto la loro.


formato iOS Hello per un reindirizzamento dell'URI è:

```
<app-scheme>://<bundle-id>
```

* **app-scheme**: è registrato nel progetto XCode ed è il modo in cui altre applicazioni possono eseguire la chiamata. È possibile trovarlo in Info.plist -> URL types -> URL Identifier. È consigliabile crearne uno se non sono stati configurati uno o più URI.
* **id bundle** -questo è l'identificatore Bundle trovato in "identity" hello annullare le impostazioni del progetto in XCode.

Per un esempio di questo codice di QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Registrare un'applicazione hello DirectorySearcher
tooset dei token tooget app, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Seguire hello richiede toocreate un nuovo **applicazione Client nativa**.
  * Hello **nome** di hello applicazione descrive tooend utenti applicazione.
  * Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte.  Immettere un valore specifico tooyour applicazione e si basa sulle informazioni di URI di reindirizzamento precedente hello.
6. Dopo aver completato la registrazione di hello, Azure AD le assegna l'app un ID applicazione univoco.  È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.
7. Da hello **impostazioni** selezionare **autorizzazioni obbligatorie** e quindi selezionare **Aggiungi**. Selezionare **Microsoft Graph** come hello API, quindi aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.  Questo imposta hello di tooquery l'applicazione Azure AD Graph API per gli utenti.

## <a name="3-install-and-configure-adal"></a>3. Installare e configurare ADAL
Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.  Per toocommunicate ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.

1. Inizia ad aggiungere toohello ADAL progetto DirectorySearcher utilizzando CocoaPods.

    ```
    $ vi Podfile
    ```
2. Aggiungere hello toothis podfile seguenti:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Ora è possibile caricare hello podfile utilizzando CocoaPods. Verrà creata una nuova area di lavoro XCode che sarà caricata.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. Nel progetto di avvio rapido hello, aprire il file plist hello `settings.plist`.  Sostituire i valori hello elementi hello in hello sezione tooreflect hello valori immessi in hello portale di Azure. Il codice fa riferimento a questi valori ogni volta che usa ADAL.
  * Hello `tenant` dominio hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.
  * Hello `clientId` hello client ID dell'applicazione copiata dal portale hello.
  * Hello `redirectUri` è l'URL di reindirizzamento hello è registrato nel portale di hello.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Utilizzare i token ADAL tooget da Azure AD
Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente un completionBlock `+(void) getToken : `, e ADAL hello rest.  

1. In hello `QuickStart` progetto, aprire `GraphAPICaller.m` e individuare hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` commento superiore hello.  Questo è possibile passare attraverso un CompletionBlock, toocommunicate con Azure AD, ADAL hello e indicare come token toocache.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. A questo punto è necessario toouse toosearch questo token per gli utenti nel grafico hello. Trovare hello `// TODO: implement SearchUsersList` commento. Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.  tooquery hello Azure AD Graph API, è necessario tooinclude access_token in hello `Authorization` intestazione della richiesta di hello. È qui che entra in gioco ADAL.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. Quando l'app richiede un token chiamando `getToken(...)`, ADAL tenta tooreturn un token senza chiedere utente hello per le credenziali.  Se ADAL rileva che l'utente hello toosign in tooget un token, verrà visualizzato una finestra di dialogo per l'accesso, raccogliere le credenziali dell'utente hello e restituisce quindi un token dopo l'autenticazione.  Se la libreria ADAL non è in grado di tooreturn un token per qualsiasi motivo, viene generata una `AdalException`.

> [!Note] 
> Hello `AuthenticationResult` oggetto contiene un `tokenCacheStoreItem` oggetto che può essere informazioni hello toocollect utilizzati che potrebbe essere necessario l'app. Nella Guida introduttiva, hello `tokenCacheStoreItem` è toodetermine usato se l'autenticazione è già stata eseguita.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Compilare ed eseguire un'applicazione hello
Congratulazioni. Ora è un'applicazione iOS che è possibile autenticare gli utenti, in modo sicuro chiamare l'API Web tramite OAuth 2.0 e ottenere le informazioni di base utente hello.  Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.  Avviare l'applicazione QuickStart e accedere come uno di questi utenti.  Cercare altri utenti in base al relativo UPN.  Chiudere l'applicazione hello e avviarla nuovamente.  Si noti che la sessione dell'utente hello rimane invariata.

ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.  Si occupa di tutto il lavoro dirty hello, ad esempio la gestione della cache, supporto del protocollo OAuth, presentate utente hello con un toosign dell'interfaccia utente in e l'aggiornamento i token scaduti.  Ciò che occorre tooknow è una singola chiamata API, `getToken`.

Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) su [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Passaggi successivi
È possibile procedere con tooadditional scenari.  È opportuno tootry:

* [Proteggere un'API Web Node.js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md)
* Informazioni su [come tooenable SSO tra app in iOS usando ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

