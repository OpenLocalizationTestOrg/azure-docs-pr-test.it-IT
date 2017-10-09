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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Usare user hello toosign-in hello libreria di autenticazione di Microsoft (MSAL)

1.  Creare un file denominato `app.js`. Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), fare clic e selezionare: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Aggiungere i seguenti tooyour codice hello `app.js` file:

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
### <a name="more-information"></a>Altre informazioni

Dopo che un utente fa clic hello *'Chiamare l'API di Microsoft Graph'* pulsante per la prima volta, hello `callGraphApi` chiamate al metodo `loginRedirect` toosign utente hello. Questo metodo comporta il reindirizzamento hello utente toohello *endpoint v2 di Microsoft Azure Active Directory* tooprompt e convalidare le credenziali dell'utente hello. Come risultato un esito positivo Accedi, hello è reindirizzato toohello indietro originale *index.html* pagina e un token viene ricevuto, elaborato da `msal.js` e informazioni di hello contenute nel token di hello sono memorizzato nella cache. Questo token è noto come hello *token ID* e contiene le informazioni di base utente hello, ad esempio nome utente di hello. Se si prevede di toouse tutti i dati forniti da questo token per qualsiasi scopo, è necessario che questo token viene convalidato dal tooguarantee server back-end che hello token toomake è stato emesso tooa utente valido per l'applicazione.

Hello SPA generato da questa Guida non rende usare direttamente di token ID hello: chiama invece `acquireTokenSilent` e/o `acquireTokenRedirect` tooacquire un *token di accesso* utilizzato tooquery hello Microsoft Graph API. Se è necessario un esempio che convalida il token di ID hello, dare un'occhiata [questo](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "esempio active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") applicazione di esempio in GitHub: esempio hello utilizza un'API Web ASP.NET per la convalida del token.

#### <a name="getting-a-user-token-interactively"></a>Acquisizione di un token utente in modo interattivo

Dopo hello iniziale Accedi, hello non si desidera chiedere tooreauthenticate utenti ogni volta che è necessario toorequest un token tooaccess una risorsa, pertanto *acquireTokenSilent* devono essere utilizzati nella maggior parte dei token di tooacquire ora hello. Vi sono tuttavia situazioni che è necessario che gli utenti interagiscono con endpoint di Azure Active Directory v2 – tooforce sono riportati alcuni esempi:
-   Gli utenti potrebbe essere necessario tooreenter le proprie credenziali perché hello password è scaduta
-   L'applicazione richiede risorse tooa di accesso che hello tooconsent esigenze utente per
-   È necessaria l'autenticazione a due fattori

Chiamare il metodo hello *acquireTokenRedirect(scope)* comportare reindirizzamento endpoint toohello v2 Azure Active Directory gli utenti (o *acquireTokenPopup(scope)* risultato in una finestra popup) in cui gli utenti devono toointeract con confermando entrambi le proprie credenziali, dando hello consenso toohello necessarie risorse o completamento dell'autenticazione a due fattori di hello.

#### <a name="getting-a-user-token-silently"></a>Acquisizione di un token utente in modo invisibile
Hello ` acquireTokenSilent` metodo gestisce le acquisizioni di token e il rinnovo senza alcuna interazione dell'utente. Dopo aver `loginRedirect` (o `loginPopup`) viene eseguito per hello prima volta, `acquireTokenSilent` è hello metodo comunemente utilizzato tooobtain token utilizzati tooaccess risorse per le chiamate successive - protette come chiamate toorequest o rinnovare token vengono apportate automaticamente.
`acquireTokenSilent`potrebbe hanno esito negativo in alcuni casi, ad esempio, la password dell'utente hello è scaduto. L'applicazione può gestire questa eccezione in due modi:

1.  Effettuare una chiamata troppo`acquireTokenRedirect` immediatamente, in base alla quale conferma hello toosign utente in. Questo modello viene usato comunemente nelle applicazioni in linea in cui non è presente contenuto non autenticato in toohello disponibili utente dell'applicazione hello. esempio Hello generato da questa installazione guidata utilizza questo modello.

2. Le applicazioni possono rendere un utente un'indicazione visiva toohello interactive sign-in è necessario e pertanto l'utente hello è possibile selezionare toosign momento hello in o possibile riprovare a eseguire un'applicazione hello `acquireTokenSilent` in un secondo momento. Viene in genere utilizzato quando l'utente hello è possibile utilizzare altre funzionalità dell'applicazione hello senza viene interrotto, ad esempio, c'è non autenticato contenuto disponibile in un'applicazione hello. In questo caso, l'utente di hello può decidere quando desiderano toosign nella risorsa protetta hello tooaccess o toorefresh hello informazioni non aggiornate.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chiamare l'API Microsoft Graph hello tramite token hello che è stata ottenuta

Aggiungere i seguenti tooyour codice hello `app.js` file:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Altre informazioni sull'esecuzione di una chiamata REST a un'API protetta

Nell'applicazione di esempio hello creata in questa Guida, hello `callWebApiWithToken()` metodo è usato toomake HTTP `GET` richiesta in una risorsa protetta che richiede un chiamante toohello contenuto hello token e quindi restituito. Questo metodo aggiunge token hello acquisito hello *intestazione autorizzazione HTTP*. Per l'applicazione di esempio hello creata da questa Guida, la risorsa hello è hello Microsoft Graph API *me* endpoint che consente di visualizzare informazioni sul profilo dell'utente hello.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Aggiungere un metodo toosign utente hello

Aggiungere i seguenti tooyour codice hello `app.js` file:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
