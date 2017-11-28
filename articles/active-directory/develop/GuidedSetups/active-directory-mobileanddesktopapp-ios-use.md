---
title: Introduzione a iOS per Azure AD v2 - Uso | Microsoft Docs
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="48878-103">Usare Microsoft Authentication Library (MSAL) per ottenere un token per l'API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="48878-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="48878-104">Aprire `ViewController.swift` e sostituire il codice con:</span><span class="sxs-lookup"><span data-stu-id="48878-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="48878-105">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="48878-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="48878-106">Acquisizione di un token utente in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="48878-106">Getting a user token interactively</span></span>
<span data-ttu-id="48878-107">Se si chiama il metodo `acquireToken`, viene visualizzata una finestra del browser in cui si chiede all'utente di eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="48878-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="48878-108">In genere, le applicazioni chiedono agli utenti di accedere in modo interattivo la prima volta che devono accedere a una risorsa protetta o quando un'operazione invisibile di acquisizione di un token ha esito negativo (ad esempio, perché la password dell'utente è scaduta).</span><span class="sxs-lookup"><span data-stu-id="48878-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="48878-109">Acquisizione di un token utente in modo invisibile</span><span class="sxs-lookup"><span data-stu-id="48878-109">Getting a user token silently</span></span>
<span data-ttu-id="48878-110">Il metodo `acquireTokenSilent` gestisce le acquisizioni e i rinnovi dei token senza alcuna interazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="48878-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="48878-111">Dopo aver eseguito `acquireToken` la prima volta, per le chiamate successive il metodo comunemente usato per ottenere i token usati per accedere a risorse protette è `acquireTokenSilent`: le chiamate per richiedere o rinnovare token vengono eseguite in modo invisibile per l'utente.</span><span class="sxs-lookup"><span data-stu-id="48878-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="48878-112">Alla fine, tuttavia, `acquireTokenSilent` avrà esito negativo perché, ad esempio, l'utente si sarà disconnesso o avrà modificato la password in un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="48878-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="48878-113">Se MSAL rileva che il problema può essere risolto richiedendo un'azione interattiva, viene attivata un'eccezione `MSALErrorCode.interactionRequired`.</span><span class="sxs-lookup"><span data-stu-id="48878-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="48878-114">L'applicazione può gestire questa eccezione in due modi:</span><span class="sxs-lookup"><span data-stu-id="48878-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="48878-115">Eseguire subito una chiamata a `acquireToken`, in modo da chiedere all'utente di eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="48878-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="48878-116">Questo criterio viene usato in genere nelle applicazioni online in cui non sono disponibili contenuti offline per l'utente.</span><span class="sxs-lookup"><span data-stu-id="48878-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="48878-117">L'applicazione di esempio generata tramite questa installazione guidata usa questo criterio: è possibile vederlo in azione la prima volta che viene eseguita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48878-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="48878-118">Poiché nessun utente ha mai usato l'applicazione, `applicationContext.users().first` conterrà un valore null e verrà generata un'eccezione ` MSALErrorCode.interactionRequired `.</span><span class="sxs-lookup"><span data-stu-id="48878-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="48878-119">Il codice dell'esempio gestirà quindi l'eccezione chiamando `acquireToken`, ovvero chiedendo all'utente di eseguire l'eccesso.</span><span class="sxs-lookup"><span data-stu-id="48878-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="48878-120">Le applicazioni possono anche generare un'indicazione visiva per informare l'utente che è necessario un accesso interattivo, in modo da consentire di scegliere il momento più opportuno per accedere. In alternativa, l'applicazione riproverà a eseguire `acquireTokenSilent` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="48878-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="48878-121">Questo metodo viene usato in genere quando l'utente può accedere ad altre funzionalità dell'applicazione senza essere interrotto, ad esempio quando nell'applicazione sono disponibili contenuti offline.</span><span class="sxs-lookup"><span data-stu-id="48878-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="48878-122">In questo caso, l'utente può decidere quando eseguire l'accesso per accedere alla risorsa protetta o per aggiornare informazioni obsolete. In alternativa, l'applicazione può decidere di riprovare a eseguire `acquireTokenSilent` se la rete viene ripristinata dopo essere stata temporaneamente non disponibile.</span><span class="sxs-lookup"><span data-stu-id="48878-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="48878-123">Chiamare l'API Microsoft Graph usando il token appena ottenuto</span><span class="sxs-lookup"><span data-stu-id="48878-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="48878-124">Aggiungere il nuovo metodo seguente a `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="48878-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="48878-125">Questo metodo consente di eseguire una richiesta `GET` all'API Graph di Microsoft tramite un'*intestazione dell'autorizzazione HTTP*:</span><span class="sxs-lookup"><span data-stu-id="48878-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="48878-126">Esecuzione di una chiamata REST a un'API protetta</span><span class="sxs-lookup"><span data-stu-id="48878-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="48878-127">In questa applicazione di esempio, viene usato il metodo `getContentWithToken()` per eseguire una richiesta HTTP `GET` a una risorsa protetta che richiede un token e restituisce il contenuto al chiamante.</span><span class="sxs-lookup"><span data-stu-id="48878-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="48878-128">Questo metodo aggiunge il token acquisito nell'*intestazione di autorizzazione HTTP*.</span><span class="sxs-lookup"><span data-stu-id="48878-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="48878-129">Per questo esempio, la risorsa è l'endpoint *me* dell'API Microsoft Graph, che consente di visualizzare informazioni sul profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="48878-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="48878-130">Configurare la disconnessione</span><span class="sxs-lookup"><span data-stu-id="48878-130">Set up sign-out</span></span>

<span data-ttu-id="48878-131">Aggiungere il metodo seguente al file `ViewController.swift` per disconnettere l'utente:</span><span class="sxs-lookup"><span data-stu-id="48878-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="48878-132">Altre informazioni sulla disconnessione</span><span class="sxs-lookup"><span data-stu-id="48878-132">More info on sign-out</span></span>

<span data-ttu-id="48878-133">Il metodo `signoutButton` sopra riportato rimuove l'utente dalla cache utente di MSAL: in questo modo, MSAL dimenticherà l'utente corrente e un'eventuale richiesta futura di acquisizione di un token riuscirà solo se eseguita in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="48878-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="48878-134">Anche se l'applicazione in questo esempio supporta un unico utente, MSAL supporta anche scenari in cui è possibile eseguire contemporaneamente l'accesso di più account, come nel caso di un'applicazione di posta elettronica in cui un utente dispone di più account.</span><span class="sxs-lookup"><span data-stu-id="48878-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="48878-135">Registrare il callback</span><span class="sxs-lookup"><span data-stu-id="48878-135">Register the callback</span></span>

<span data-ttu-id="48878-136">Dopo l'autenticazione dell'utente, il browser reindirizza di nuovo l'utente all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48878-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="48878-137">Eseguire la procedura descritta di seguito per registrare questo callback:</span><span class="sxs-lookup"><span data-stu-id="48878-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="48878-138">Aprire `AppDelegate.swift` e importare MSAL:</span><span class="sxs-lookup"><span data-stu-id="48878-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="48878-139">Aggiungere il metodo seguente alla classe <code>AppDelegate</code> per gestire i callback:</span><span class="sxs-lookup"><span data-stu-id="48878-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

