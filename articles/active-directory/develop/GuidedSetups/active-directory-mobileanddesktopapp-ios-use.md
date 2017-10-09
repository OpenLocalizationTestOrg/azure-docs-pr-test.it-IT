---
title: 'iOS v2 aaaAzure AD Guida introduttiva: uso | Documenti Microsoft'
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilizzare hello libreria di autenticazione di Microsoft (MSAL) tooget un token per hello Microsoft Graph API

Aprire `ViewController.swift` e sostituire il codice hello con:

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Altre informazioni
#### <a name="getting-a-user-token-interactively"></a>Acquisizione di un token utente in modo interattivo
Chiamare il metodo hello `acquireToken` risultati del metodo in una finestra del browser richiesta hello toosign utente in. Le applicazioni in genere richiedono toosign un utente in modo interattivo hello devono tooaccess prima volta che una risorsa protetta o quando una tooacquire operazione invisibile all'utente un token ha esito negativo (ad esempio, la password dell'utente hello scaduto).

#### <a name="getting-a-user-token-silently"></a>Acquisizione di un token utente in modo invisibile
Hello `acquireTokenSilent` metodo gestisce le acquisizioni di token e il rinnovo senza alcuna interazione dell'utente. Dopo aver `acquireToken` per hello prima esecuzione, `acquireTokenSilent` è hello metodo comunemente utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.

Infine, `acquireTokenSilent` avrà esito negativo, ad esempio hello utente è disconnesso o è stato modificato la password in un altro dispositivo. Quando MSAL rileva hello problema può essere risolto tramite la richiesta un'azione interattiva, viene generato un `MSALErrorCode.interactionRequired` eccezione. L'applicazione può gestire questa eccezione in due modi:

1.  Effettuare una chiamata su `acquireToken` immediatamente, in base alla quale conferma hello toosign utente in. Questo modello è in genere utilizzato nelle applicazioni in linea in cui è presente alcun contenuto offline in un'applicazione hello disponibile per l'utente hello. applicazione di esempio Hello generata da questa installazione guidata utilizza questo modello: è possibile visualizzarlo in hello azione prima volta che si esegue l'applicazione hello. Poiché nessun utente è già utilizzata un'applicazione hello, `applicationContext.users().first` conterrà un valore null e un ` MSALErrorCode.interactionRequired ` verrà generata l'eccezione. Hello del codice nell'esempio hello quindi handle hello eccezione chiamando `acquireToken` risultante conferma toosign utente hello in.

2.  Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `acquireTokenSilent` in un secondo momento. Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non in linea contenuto disponibile in un'applicazione hello. In questo caso, è possibile decidere utente hello quando desiderano toosign nella risorsa protetta hello tooaccess toorefresh hello informazioni non aggiornate o l'applicazione può decidere tooretry `acquireTokenSilent` quando rete viene ripristinata dopo essere stato temporaneamente non disponibile.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta

Aggiungere hello nuovo metodo seguito troppo`ViewController.swift`. Questo metodo è usato toomake un `GET` richiesta rispetto all'utilizzo di Microsoft Graph API hello un *intestazione autorizzazione HTTP*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a>Esecuzione di una chiamata REST a un'API protetta

In questa applicazione di esempio hello `getContentWithToken()` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito. Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*. Per questo esempio, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configurare la disconnessione

Aggiungere hello seguente metodo troppo`ViewController.swift` toosign utente hello:

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Altre informazioni sulla disconnessione

Hello `signoutButton` metodo hello cache utente MSAL: rimuove l'utente hello in modo efficace verrà utente corrente di MSAL tooforget hello in modo tooacquire una richiesta futura un token riuscirà solo se viene resa toobe interattiva.

Anche se un'applicazione hello in questo esempio supporta un singolo utente, MSAL supporta scenari in cui può essere firmato in più account a hello contemporaneamente – un esempio è di un'applicazione di posta elettronica in cui un utente dispone di più account.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Registrare callback hello

Dopo l'autenticazione utente hello, browser hello reindirizza un'applicazione hello utente toohello indietro. Seguire i passaggi di hello sotto tooregister questo callback:

1.  Aprire `AppDelegate.swift` e importare MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Aggiungere hello seguente metodo tooyour <code>AppDelegate</code> classe toohandle callback:
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

