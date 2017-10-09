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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="4e5c4-103">Utilizzare hello libreria di autenticazione di Microsoft (MSAL) tooget un token per hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="4e5c4-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="4e5c4-104">Aprire `ViewController.swift` e sostituire il codice hello con:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-104">Open `ViewController.swift` and replace hello code with:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="4e5c4-105">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="4e5c4-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="4e5c4-106">Acquisizione di un token utente in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="4e5c4-106">Getting a user token interactively</span></span>
<span data-ttu-id="4e5c4-107">Chiamare il metodo hello `acquireToken` risultati del metodo in una finestra del browser richiesta hello toosign utente in.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="4e5c4-108">Le applicazioni in genere richiedono toosign un utente in modo interattivo hello devono tooaccess prima volta che una risorsa protetta o quando una tooacquire operazione invisibile all'utente un token ha esito negativo (ad esempio, la password dell'utente hello scaduto).</span><span class="sxs-lookup"><span data-stu-id="4e5c4-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="4e5c4-109">Acquisizione di un token utente in modo invisibile</span><span class="sxs-lookup"><span data-stu-id="4e5c4-109">Getting a user token silently</span></span>
<span data-ttu-id="4e5c4-110">Hello `acquireTokenSilent` metodo gestisce le acquisizioni di token e il rinnovo senza alcuna interazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="4e5c4-111">Dopo aver `acquireToken` per hello prima esecuzione, `acquireTokenSilent` è hello metodo comunemente utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="4e5c4-112">Infine, `acquireTokenSilent` avrà esito negativo, ad esempio hello utente è disconnesso o è stato modificato la password in un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="4e5c4-113">Quando MSAL rileva hello problema può essere risolto tramite la richiesta un'azione interattiva, viene generato un `MSALErrorCode.interactionRequired` eccezione.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="4e5c4-114">L'applicazione può gestire questa eccezione in due modi:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="4e5c4-115">Effettuare una chiamata su `acquireToken` immediatamente, in base alla quale conferma hello toosign utente in.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="4e5c4-116">Questo modello è in genere utilizzato nelle applicazioni in linea in cui è presente alcun contenuto offline in un'applicazione hello disponibile per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="4e5c4-117">applicazione di esempio Hello generata da questa installazione guidata utilizza questo modello: è possibile visualizzarlo in hello azione prima volta che si esegue l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="4e5c4-118">Poiché nessun utente è già utilizzata un'applicazione hello, `applicationContext.users().first` conterrà un valore null e un ` MSALErrorCode.interactionRequired ` verrà generata l'eccezione.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="4e5c4-119">Hello del codice nell'esempio hello quindi handle hello eccezione chiamando `acquireToken` risultante conferma toosign utente hello in.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="4e5c4-120">Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `acquireTokenSilent` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="4e5c4-121">Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non in linea contenuto disponibile in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="4e5c4-122">In questo caso, è possibile decidere utente hello quando desiderano toosign nella risorsa protetta hello tooaccess toorefresh hello informazioni non aggiornate o l'applicazione può decidere tooretry `acquireTokenSilent` quando rete viene ripristinata dopo essere stato temporaneamente non disponibile.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="4e5c4-123">Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta</span><span class="sxs-lookup"><span data-stu-id="4e5c4-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="4e5c4-124">Aggiungere hello nuovo metodo seguito troppo`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="4e5c4-125">Questo metodo è usato toomake un `GET` richiesta rispetto all'utilizzo di Microsoft Graph API hello un *intestazione autorizzazione HTTP*:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="4e5c4-126">Esecuzione di una chiamata REST a un'API protetta</span><span class="sxs-lookup"><span data-stu-id="4e5c4-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="4e5c4-127">In questa applicazione di esempio hello `getContentWithToken()` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="4e5c4-128">Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="4e5c4-129">Per questo esempio, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="4e5c4-130">Configurare la disconnessione</span><span class="sxs-lookup"><span data-stu-id="4e5c4-130">Set up sign-out</span></span>

<span data-ttu-id="4e5c4-131">Aggiungere hello seguente metodo troppo`ViewController.swift` toosign utente hello:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="4e5c4-132">Altre informazioni sulla disconnessione</span><span class="sxs-lookup"><span data-stu-id="4e5c4-132">More info on sign-out</span></span>

<span data-ttu-id="4e5c4-133">Hello `signoutButton` metodo hello cache utente MSAL: rimuove l'utente hello in modo efficace verrà utente corrente di MSAL tooforget hello in modo tooacquire una richiesta futura un token riuscirà solo se viene resa toobe interattiva.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="4e5c4-134">Anche se un'applicazione hello in questo esempio supporta un singolo utente, MSAL supporta scenari in cui può essere firmato in più account a hello contemporaneamente – un esempio è di un'applicazione di posta elettronica in cui un utente dispone di più account.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="4e5c4-135">Registrare callback hello</span><span class="sxs-lookup"><span data-stu-id="4e5c4-135">Register hello callback</span></span>

<span data-ttu-id="4e5c4-136">Dopo l'autenticazione utente hello, browser hello reindirizza un'applicazione hello utente toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="4e5c4-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="4e5c4-137">Seguire i passaggi di hello sotto tooregister questo callback:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="4e5c4-138">Aprire `AppDelegate.swift` e importare MSAL:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="4e5c4-139">Aggiungere hello seguente metodo tooyour <code>AppDelegate</code> classe toohandle callback:</span><span class="sxs-lookup"><span data-stu-id="4e5c4-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
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

