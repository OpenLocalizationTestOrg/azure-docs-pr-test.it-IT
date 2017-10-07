---
title: aaaAdd l'autenticazione in iOS con App mobili di Azure
description: "Informazioni su come utenti di tooauthenticate toouse App mobili di Azure di app iOS tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>Aggiungere app per iOS tooyour autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In questa esercitazione, si aggiunge l'autenticazione toohello [iOS quick start] progetto che utilizza un provider di identità supportati. In questa esercitazione si basa sull'hello [iOS quick start] esercitazione, è necessario completare prima.

## <a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app

L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.  App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.  In questa esercitazione si usa lo schema URL _appname_.  È tuttavia possibile usare QUALSIASI schema URL.  Deve essere univoco tooyour applicazioni per dispositivi mobili.  reindirizzamento di hello tooenable sul lato server th:

1. In hello [portale di Azure], selezionare il servizio App.

2. Fare clic su hello **autenticazione / autorizzazione** opzione di menu.

3. Fare clic su **Azure Active Directory** in hello **provider di autenticazione** sezione.

4. Set hello **modalità di gestione** troppo**avanzate**.

5. In hello **consentito URL di reindirizzamento esterno**, immettere `appname://easyauth.callback`.  Hello _appname_ in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.  Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.  È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.

6. Fare clic su **OK**.

7. Fare clic su **Salva**.

## <a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

In Xcode, premere **eseguire** toostart hello app. Poiché tenta di app hello tooaccess back-end come un utente non autenticato, viene generata un'eccezione, ma hello *TodoItem* tabella richiede ora l'autenticazione.

## <a name="add-authentication"></a>Aggiungere l'autenticazione tooapp
**Objective-C**:

1. Nel Mac, aprire *QSTodoListViewController.m* in Xcode e aggiungere al metodo hello:

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    Modifica *google* troppo*microsoftaccount*, *twitter*, *facebook*, o *windowsazureactivedirectory* se non si utilizza Google come provider di identità. Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.

    Sostituire hello **urlScheme** con un nome univoco per l'applicazione.  Hello urlScheme deve essere hello stesso come hello protocollo lo schema dell'URL specificato nel hello **consentito URL di reindirizzamento esterno** campo hello portale di Azure. Hello urlScheme viene utilizzata da un'applicazione hello autenticazione callback tooswitch tooyour back-dopo la richiesta di autenticazione è stata completata.

2. Sostituire `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* con hello seguente codice:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Aprire hello `QSAppDelegate.h` file e aggiungere hello seguente codice:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Aprire hello `QSAppDelegate.m` file e aggiungere hello seguente codice:

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   Aggiungere il codice direttamente prima della lettura riga hello `#pragma mark - Core Data stack`.  Sostituire il _appname_ oggi hello urlScheme che è stato utilizzato nel passaggio 1.

5. Aprire hello `AppName-Info.plist` file (sostituendo AppName con nome hello dell'app) e aggiungere hello seguente codice:

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Questo codice deve essere inserito all'interno di hello `<dict>` elemento.  Sostituire hello _appname_ stringa (all'interno della matrice per **CFBundleURLSchemes**) con il nome di app hello scelto nel passaggio 1.  È possibile inoltre apportare queste modifiche in hello plist editor, fare clic su hello `AppName-Info.plist` file nell'editor di XCode tooopen hello plist.

    Sostituire hello `com.microsoft.azure.zumo` stringa per **CFBundleURLName** con l'Apple identificatore di aggregazione.

6. Premere *eseguire* toostart hello app e quindi l'accesso. Quando si è connessi, si deve essere elenco di attività in grado di tooview hello e aggiornamenti.

**Swift**:

1. Nel Mac, aprire *ToDoTableViewController.swift* in Xcode e aggiungere al metodo hello:

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    Modifica *google* troppo*microsoftaccount*, *twitter*, *facebook*, o *windowsazureactivedirectory* se non si utilizza Google come provider di identità. Se si usa Facebook sarà necessario [consentire i domini Facebook][1] all'interno dell'app.

    Sostituire hello **urlScheme** con un nome univoco per l'applicazione.  Hello urlScheme deve essere hello stesso come hello protocollo lo schema dell'URL specificato nel hello **consentito URL di reindirizzamento esterno** campo hello portale di Azure. Hello urlScheme viene utilizzata da un'applicazione hello autenticazione callback tooswitch tooyour back-dopo la richiesta di autenticazione è stata completata.

2. Rimuovere le righe di hello `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` alla fine di `viewDidLoad()` in *ToDoTableViewController.swift*. Aggiungere una chiamata troppo`loginAndGetData()` al loro posto:

    ```swift
    loginAndGetData()
    ```

3. Aprire hello `AppDelegate.swift` file e aggiungere hello seguente riga toohello `AppDelegate` classe:

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    Sostituire hello _appname_ oggi hello urlScheme che è stato utilizzato nel passaggio 1.

4. Aprire hello `AppName-Info.plist` file (sostituendo AppName con nome hello dell'app) e aggiungere hello seguente codice:

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Questo codice deve essere inserito all'interno di hello `<dict>` elemento.  Sostituire hello _appname_ stringa (all'interno della matrice per **CFBundleURLSchemes**) con il nome di app hello scelto nel passaggio 1.  È possibile inoltre apportare queste modifiche in hello plist editor, fare clic su hello `AppName-Info.plist` file nell'editor di XCode tooopen hello plist.

    Sostituire hello `com.microsoft.azure.zumo` stringa per **CFBundleURLName** con l'Apple identificatore di aggregazione.

5. Premere *eseguire* toostart hello app e quindi l'accesso. Quando si è connessi, si deve essere elenco di attività in grado di tooview hello e aggiornamenti.

L'autenticazione del servizio app usa la comunicazione tra app di Apple.  Per ulteriori informazioni su questo argomento, vedere toohello [documentazione di Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portale di Azure]: https://portal.azure.com

[iOS quick start]: app-service-mobile-ios-get-started.md

