---
title: 'Configurazione guidata di app a singola pagina JavaScript con Azure AD v2: uso | Microsoft Docs'
description: Come le applicazioni SPA di Javascript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: f52157df298ddfc1c1b29a18dc9a54aae59b52a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-sign-in-the-user"></a><span data-ttu-id="b2612-103">Usare Microsoft Authentication Library (MSAL) per l'accesso degli utenti</span><span class="sxs-lookup"><span data-stu-id="b2612-103">Use the Microsoft Authentication Library (MSAL) to sign-in the user</span></span>

1.  <span data-ttu-id="b2612-104">Creare un file denominato `app.js`.</span><span class="sxs-lookup"><span data-stu-id="b2612-104">Create a file named `app.js`.</span></span> <span data-ttu-id="b2612-105">Se si usa Visual Studio, selezionare il progetto (ossia la cartella radice del progetto), fare clic con il pulsante destro del mouse e scegliere `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="b2612-105">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="b2612-106">Aggiungere il codice seguente al file `app.js`:</span><span class="sxs-lookup"><span data-stu-id="b2612-106">Add the following code to your `app.js` file:</span></span>

```javascript
// Graph API endpoint to show user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used to obtain the access token to read user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue to display user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call the Microsoft Graph API and display the results on the page. Sign the user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user to sign in via loginRedirect.
        // This will redirect user to the Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // The call to loginRedirect above frontloads the consent to query Graph API during the sign-in.
        // If you want to use dynamic consent, just remove the graphAPIScopes from loginRedirect call.
        // As such, user will be prompted to give consent when requested access to a resource that 
        // he/she hasn't consented before. In the case of this application - 
        // the first time the Graph API call to obtain user's profile is executed.
    } else {
        // If user is already signed in, display the user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API to show the user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order to call the Graph API, an access token needs to be acquired.
        // Try to acquire the token used to query Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After the access token is acquired, call the Web API, sending the acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If the acquireTokenSilent() method fails, then acquire the token interactively via acquireTokenRedirect().
                // In this case, the browser will redirect user back to the Azure Active Directory v2 Endpoint so the user 
                // can reenter the current username/ password and/ or give consent to new permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get the token silently, the Graph API call results will be made and results will be displayed in the page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() to show results.
 * @param {string} errorDesc - If error occur, the error message
 * @param {object} token - The token received from login
 * @param {object} error - The error string
 * @param {string} tokenType - the token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in the page
 * @param {string} endpoint - the endpoint used for the error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="b2612-107">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="b2612-107">More Information</span></span>

<span data-ttu-id="b2612-108">Quando un utente fa clic sul pulsante *Call Microsoft Graph API* (Chiama API Microsoft Graph) per la prima volta, il metodo `callGraphApi` chiama `loginRedirect` per l'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b2612-108">After a user clicks the *‘Call Microsoft Graph API’* button for the first time, `callGraphApi` method calls `loginRedirect` to sign in the user.</span></span> <span data-ttu-id="b2612-109">Questo metodo determina il reindirizzamento dell'utente all'*endpoint di Microsoft Azure Active Directory v2* per la richiesta e la convalida delle credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="b2612-109">This method results in redirecting the user to the *Microsoft Azure Active Directory v2 endpoint* to prompt and validate the user's credentials.</span></span> <span data-ttu-id="b2612-110">Dopo che è stato completato l'accesso, l'utente viene reindirizzato di nuovo alla pagina *index.html* originale e viene ricevuto un token, elaborato da `msal.js`, le cui informazioni vengono memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="b2612-110">As a result of a successful sign-in, the user is redirected back to the original *index.html* page, and a token is received, processed by `msal.js` and the information contained in the token is cached.</span></span> <span data-ttu-id="b2612-111">Questo token è noto come *token ID* e contiene informazioni di base sull'utente, ad esempio il nome visualizzato.</span><span class="sxs-lookup"><span data-stu-id="b2612-111">This token is known as the *ID token* and contains basic information about the user, such as the user display name.</span></span> <span data-ttu-id="b2612-112">Se si prevede di usare per qualsiasi scopo i dati forniti da questo token, è necessario verificare che il token venga convalidato dal server back-end per garantire che il token sia stato rilasciato a un utente valido per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2612-112">If you plan to use any data provided by this token for any purposes, you need to make sure this token is validated by your backend server to guarantee that the token was issued to a valid user for your application.</span></span>

<span data-ttu-id="b2612-113">L'app a singola pagina generata da questa guida non usa direttamente il token ID, ma chiama `acquireTokenSilent` e/o `acquireTokenRedirect` per acquisire un *token di accesso* usato per eseguire query sull'API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b2612-113">The SPA generated by this guide does not make use directly of the ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` to acquire an *access token* used to query the Microsoft Graph API.</span></span> <span data-ttu-id="b2612-114">Se è necessario un esempio che convalidi il token ID, vedere [questa](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Esempio active-directory-javascript-singlepageapp-dotnet-webapi-v2 in GitHub") applicazione di esempio in GitHub. L'esempio usa un'API Web ASP.NET per la convalida dei token.</span><span class="sxs-lookup"><span data-stu-id="b2612-114">If you need a sample that validates the ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – the sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="b2612-115">Acquisizione di un token utente in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="b2612-115">Getting a user token interactively</span></span>

<span data-ttu-id="b2612-116">Dopo l'accesso iniziale, per non chiedere agli utenti di ripetere l'autenticazione ogni volta che devono richiedere un token per accedere a una risorsa, si dovrà usare *acquireTokenSilent* per acquisire i token nella maggior parte dei casi.</span><span class="sxs-lookup"><span data-stu-id="b2612-116">After the initial sign-in, you do not want the ask users to reauthenticate every time they need to request a token to access a resource – so *acquireTokenSilent* should be used most of the time to acquire tokens.</span></span> <span data-ttu-id="b2612-117">In alcune situazioni, tuttavia, è necessario imporre agli utenti di interagire con l'endpoint di Azure Active Directory v2, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b2612-117">There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="b2612-118">Potrebbe essere necessario che gli utenti reimmettano le proprie credenziali perché la password è scaduta</span><span class="sxs-lookup"><span data-stu-id="b2612-118">Users may need to reenter their credentials because the password has expired</span></span>
-   <span data-ttu-id="b2612-119">L'applicazione richiede l'accesso a una risorsa per cui è necessario il consenso dell'utente</span><span class="sxs-lookup"><span data-stu-id="b2612-119">Your application is requesting access to a resource that the user needs to consent to</span></span>
-   <span data-ttu-id="b2612-120">È necessaria l'autenticazione a due fattori</span><span class="sxs-lookup"><span data-stu-id="b2612-120">Two factor authentication is required</span></span>

<span data-ttu-id="b2612-121">Chiamando *acquireTokenRedirect(scope)*, gli utenti vengono reindirizzati all'endpoint di Azure Active Directory v2 (mentre con *acquireTokenPopup(scope)* viene visualizzata una finestra popup) e gli utenti devono interagire confermando le proprie credenziali, dando il consenso per la risorsa necessaria o completando l'autenticazione a due fattori.</span><span class="sxs-lookup"><span data-stu-id="b2612-121">Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="b2612-122">Acquisizione di un token utente in modo invisibile</span><span class="sxs-lookup"><span data-stu-id="b2612-122">Getting a user token silently</span></span>
<span data-ttu-id="b2612-123">Il metodo ` acquireTokenSilent` gestisce le acquisizioni e i rinnovi dei token senza alcuna interazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b2612-123">The ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="b2612-124">Dopo l'esecuzione iniziale di `loginRedirect` o `loginPopup`, il metodo in genere usato per le chiamate successive per ottenere i token usati per l'accesso alle risorse protette è `acquireTokenSilent` e le chiamate per richiedere o rinnovare token vengono eseguite in modo invisibile all'utente.</span><span class="sxs-lookup"><span data-stu-id="b2612-124">After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="b2612-125">In alcuni casi, `acquireTokenSilent` può avere esito negativo, ad esempio se la password dell'utente è scaduta.</span><span class="sxs-lookup"><span data-stu-id="b2612-125">`acquireTokenSilent` may fail in some cases – for example, the user's password has expired.</span></span> <span data-ttu-id="b2612-126">L'applicazione può gestire questa eccezione in due modi:</span><span class="sxs-lookup"><span data-stu-id="b2612-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="b2612-127">Eseguire immediatamente una chiamata ad `acquireTokenRedirect` in modo da chiedere all'utente di eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b2612-127">Make a call to `acquireTokenRedirect` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="b2612-128">Questo modello viene in genere usato nelle applicazioni online in cui non è disponibile per l'utente contenuto non autenticato.</span><span class="sxs-lookup"><span data-stu-id="b2612-128">This pattern is commonly used in online applications where there is no unauthenticated content in the application available to the user.</span></span> <span data-ttu-id="b2612-129">L'esempio generato da questa configurazione guidata usa questo modello.</span><span class="sxs-lookup"><span data-stu-id="b2612-129">The sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="b2612-130">Le applicazioni possono anche generare un'indicazione visiva per informare l'utente che è necessario un accesso interattivo, in modo da consentire di scegliere il momento più opportuno per accedere. In alternativa, l'applicazione riproverà a eseguire `acquireTokenSilent` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b2612-130">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="b2612-131">Questo modello viene in genere usato quando l'utente può accedere ad altre funzionalità dell'applicazione senza interruzioni, ad esempio quando nell'applicazione è disponibile contenuto non autenticato.</span><span class="sxs-lookup"><span data-stu-id="b2612-131">This is commonly used when the user can use other functionality of the application without being disrupted - for example, there is unauthenticated content available in the application.</span></span> <span data-ttu-id="b2612-132">In questo caso, l'utente può decidere se vuole eseguire l'accesso per accedere alla risorsa protetta oppure aggiornare le informazioni obsolete.</span><span class="sxs-lookup"><span data-stu-id="b2612-132">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="b2612-133">Chiamare l'API Microsoft Graph usando il token appena ottenuto</span><span class="sxs-lookup"><span data-stu-id="b2612-133">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="b2612-134">Aggiungere il codice seguente al file `app.js`:</span><span class="sxs-lookup"><span data-stu-id="b2612-134">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used to display the results
 * @param {object} showTokenElement = HTML element used to display the RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in the page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in the page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="b2612-135">Altre informazioni sull'esecuzione di una chiamata REST a un'API protetta</span><span class="sxs-lookup"><span data-stu-id="b2612-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="b2612-136">Nell'applicazione di esempio creata da questa guida viene usato il metodo `callWebApiWithToken()` per eseguire una richiesta HTTP `GET` a una risorsa protetta che richiede un token e restituisce il contenuto al chiamante.</span><span class="sxs-lookup"><span data-stu-id="b2612-136">In the sample application created by this guide, the `callWebApiWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="b2612-137">Questo metodo aggiunge il token acquisito nell'*intestazione di autorizzazione HTTP*.</span><span class="sxs-lookup"><span data-stu-id="b2612-137">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="b2612-138">Per l'applicazione di esempio creata da questa guida, la risorsa è l'endpoint *me* dell'API Microsoft Graph, che consente di visualizzare informazioni sul profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b2612-138">For the sample application created by this guide, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="b2612-139">Aggiungere un metodo per disconnettere l'utente</span><span class="sxs-lookup"><span data-stu-id="b2612-139">Add a method to sign out the user</span></span>

<span data-ttu-id="b2612-140">Aggiungere il codice seguente al file `app.js`:</span><span class="sxs-lookup"><span data-stu-id="b2612-140">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Sign-out the user
 */
function signOut() {
    userAgentApplication.logout();
}
```
