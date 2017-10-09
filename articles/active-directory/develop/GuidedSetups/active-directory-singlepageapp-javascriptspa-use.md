---
title: aaaAzure AD v2 JS SPA impostazione guidata - utilizzo | Documenti Microsoft
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
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="5409c-103">Usare user hello toosign-in hello libreria di autenticazione di Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="5409c-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="5409c-104">Creare un file denominato `app.js`.</span><span class="sxs-lookup"><span data-stu-id="5409c-104">Create a file named `app.js`.</span></span> <span data-ttu-id="5409c-105">Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), fare clic e selezionare: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="5409c-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="5409c-106">Aggiungere i seguenti tooyour codice hello `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="5409c-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
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
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
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
### <a name="more-information"></a><span data-ttu-id="5409c-107">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="5409c-107">More Information</span></span>

<span data-ttu-id="5409c-108">Dopo che un utente fa clic hello *'Chiamare l'API di Microsoft Graph'* pulsante per la prima volta, hello `callGraphApi` chiamate al metodo `loginRedirect` toosign utente hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="5409c-109">Questo metodo comporta il reindirizzamento hello utente toohello *endpoint v2 di Microsoft Azure Active Directory* tooprompt e convalidare le credenziali dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="5409c-110">Come risultato un esito positivo Accedi, hello è reindirizzato toohello indietro originale *index.html* pagina e un token viene ricevuto, elaborato da `msal.js` e informazioni di hello contenute nel token di hello sono memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="5409c-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="5409c-111">Questo token è noto come hello *token ID* e contiene le informazioni di base utente hello, ad esempio nome utente di hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="5409c-112">Se si prevede di toouse tutti i dati forniti da questo token per qualsiasi scopo, è necessario che questo token viene convalidato dal tooguarantee server back-end che hello token toomake è stato emesso tooa utente valido per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5409c-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="5409c-113">Hello SPA generato da questa Guida non rende usare direttamente di token ID hello: chiama invece `acquireTokenSilent` e/o `acquireTokenRedirect` tooacquire un *token di accesso* utilizzato tooquery hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="5409c-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="5409c-114">Se è necessario un esempio che convalida il token di ID hello, dare un'occhiata [questo](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "esempio active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") applicazione di esempio in GitHub: esempio hello utilizza un'API Web ASP.NET per la convalida del token.</span><span class="sxs-lookup"><span data-stu-id="5409c-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="5409c-115">Acquisizione di un token utente in modo interattivo</span><span class="sxs-lookup"><span data-stu-id="5409c-115">Getting a user token interactively</span></span>

<span data-ttu-id="5409c-116">Dopo hello iniziale Accedi, hello non si desidera chiedere tooreauthenticate utenti ogni volta che è necessario toorequest un token tooaccess una risorsa, pertanto *acquireTokenSilent* devono essere utilizzati nella maggior parte dei token di tooacquire ora hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="5409c-117">Vi sono tuttavia situazioni che è necessario che gli utenti interagiscono con endpoint di Azure Active Directory v2 – tooforce sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="5409c-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="5409c-118">Gli utenti potrebbe essere necessario tooreenter le proprie credenziali perché hello password è scaduta</span><span class="sxs-lookup"><span data-stu-id="5409c-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="5409c-119">L'applicazione richiede risorse tooa di accesso che hello tooconsent esigenze utente per</span><span class="sxs-lookup"><span data-stu-id="5409c-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="5409c-120">È necessaria l'autenticazione a due fattori</span><span class="sxs-lookup"><span data-stu-id="5409c-120">Two factor authentication is required</span></span>

<span data-ttu-id="5409c-121">Chiamare il metodo hello *acquireTokenRedirect(scope)* comportare reindirizzamento endpoint toohello v2 Azure Active Directory gli utenti (o *acquireTokenPopup(scope)* risultato in una finestra popup) in cui gli utenti devono toointeract con confermando entrambi le proprie credenziali, dando hello consenso toohello necessarie risorse o completamento dell'autenticazione a due fattori di hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="5409c-122">Acquisizione di un token utente in modo invisibile</span><span class="sxs-lookup"><span data-stu-id="5409c-122">Getting a user token silently</span></span>
<span data-ttu-id="5409c-123">Hello ` acquireTokenSilent` metodo gestisce le acquisizioni di token e il rinnovo senza alcuna interazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5409c-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="5409c-124">Dopo aver `loginRedirect` (o `loginPopup`) viene eseguito per hello prima volta, `acquireTokenSilent` è hello metodo comunemente utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5409c-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="5409c-125">`acquireTokenSilent`potrebbe hanno esito negativo in alcuni casi, ad esempio, la password dell'utente hello è scaduto.</span><span class="sxs-lookup"><span data-stu-id="5409c-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="5409c-126">L'applicazione può gestire questa eccezione in due modi:</span><span class="sxs-lookup"><span data-stu-id="5409c-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="5409c-127">Effettuare una chiamata troppo`acquireTokenRedirect` immediatamente, in base alla quale conferma hello toosign utente in.</span><span class="sxs-lookup"><span data-stu-id="5409c-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="5409c-128">Questo modello viene usato comunemente nelle applicazioni in linea in cui non è presente contenuto non autenticato in toohello disponibili utente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="5409c-129">esempio Hello generato da questa installazione guidata utilizza questo modello.</span><span class="sxs-lookup"><span data-stu-id="5409c-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="5409c-130">Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `acquireTokenSilent` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5409c-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="5409c-131">Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non autenticato contenuto disponibile in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="5409c-132">In questo caso, l'utente di hello può decidere quando desiderano toosign nella risorsa protetta hello tooaccess o toorefresh hello informazioni non aggiornate.</span><span class="sxs-lookup"><span data-stu-id="5409c-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="5409c-133">Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta</span><span class="sxs-lookup"><span data-stu-id="5409c-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="5409c-134">Aggiungere i seguenti tooyour codice hello `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="5409c-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
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
                        // Display response in hello page
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
                        // Display response as error in hello page
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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="5409c-135">Altre informazioni sull'esecuzione di una chiamata REST a un'API protetta</span><span class="sxs-lookup"><span data-stu-id="5409c-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="5409c-136">Nell'applicazione di esempio hello creata in questa Guida, hello `callWebApiWithToken()` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito.</span><span class="sxs-lookup"><span data-stu-id="5409c-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="5409c-137">Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*.</span><span class="sxs-lookup"><span data-stu-id="5409c-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="5409c-138">Per l'applicazione di esempio hello creata da questa Guida, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="5409c-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="5409c-139">Aggiungere un metodo toosign utente hello</span><span class="sxs-lookup"><span data-stu-id="5409c-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="5409c-140">Aggiungere i seguenti tooyour codice hello `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="5409c-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
