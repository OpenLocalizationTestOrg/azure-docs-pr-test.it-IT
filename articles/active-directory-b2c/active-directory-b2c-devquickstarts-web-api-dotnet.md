---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'app Web .NET e chiamare una web api tramite i token di accesso OAuth 2.0 e di Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: Chiamare un'API Web .NET da un'app Web .NET

Tramite Azure Active Directory B2C, è possibile aggiungere identità potente Gestione funzionalità tooyour web App e API web. In questo articolo illustra il funzionamento di token di accesso e di effettuare chiamate da un "elenco".NET toorequest tooa app web .NET web api.

In questo articolo non viene illustrata la modalità tooimplement Accedi, sottoscrizione e il profilo di gestione con Azure Active Directory B2C. Si concentra sulle API web chiamante dopo hello è già autenticato. Se lo si è già fatto, è necessario fare:

* un'introduzione alle [app Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* un'introduzione alle [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Prerequisito

toobuild un'applicazione web che chiama una web api, è necessario:

1. [Creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md).
2. [Registrare un'API Web](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Registrare un'app Web](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Configurare i criteri](active-directory-b2c-reference-policies.md).
5. [GRANT prova web app autorizzazioni toouse prova web api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> un'applicazione client Hello e API web devono utilizzare directory B2C hello stesso Azure Active Directory.
>

## <a name="download-hello-code"></a>Scaricare codice hello

codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). È possibile clonare: esempio hello eseguendo:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio. file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`. `TaskWebApp`è un'applicazione web MVC hello utente interagisce con. `TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente. In questo articolo non viene illustrata la compilazione hello `TaskWebApp` app web o hello `TaskService` web api. toolearn come toobuild hello .NET web app usando Azure Active Directory B2C, vedere il nostro [esercitazione di app web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn come toobuild hello .NET web API protetta con Azure Active Directory B2C, vedere il nostro [esercitazione API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Aggiornare la configurazione di hello Azure Active Directory B2C

L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo. Se si desidera toouse il proprio tenant:

1. Aprire `web.config` in hello `TaskService` progetti e sostituire i valori hello per

    * `ida:Tenant` con il nome del tenant
    * `ida:ClientId` con l'ID dell'applicazione API Web
    * `ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"

2. Aprire `web.config` in hello `TaskWebApp` progetti e sostituire i valori hello per

    * `ida:Tenant` con il nome del tenant
    * `ida:ClientId` con l'ID dell'applicazione di tipo app Web
    * `ida:ClientSecret` con la chiave privata dell'app Web
    * `ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"
    * `ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"
    * `ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"



## <a name="requesting-and-saving-an-access-token"></a>Richiesta e salvataggio di un token di accesso

### <a name="specify-hello-permissions"></a>Specificare le autorizzazioni di hello

In ordine toomake hello chiamata toohello API web, è necessario utente hello tooauthenticate (tramite il criterio sign-configurazione/Accedi) e [ricevere un token di accesso](active-directory-b2c-access-tokens.md) da Azure Active Directory B2C. In ordine tooreceive un token di accesso, è necessario specificare le autorizzazioni di hello desideri toogrant token di accesso hello. le autorizzazioni di Hello sono specificate in hello `scope` parametro quando si apportata hello richiesta toohello `/authorize` endpoint. Ad esempio, un token di accesso con hello "Leggi" applicazione della risorsa autorizzazione toohello con tooacquire hello URI ID App del `https://contoso.onmicrosoft.com/tasks`, ambito hello sarebbe `https://contoso.onmicrosoft.com/tasks/read`.

ambito hello toospecify nel file di esempio, aprire hello `App_Start\Startup.Auth.cs` e definire hello `Scope` variabile OpenIdConnectAuthenticationOptions.

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Codice di autorizzazione hello per un token di accesso di Exchange

Al termine dell'esperienza di iscrizione o accesso hello un utente, l'applicazione riceverà un codice di autorizzazione da Azure Active Directory B2C. middleware OWIN OpenID Connect Hello archivierà il codice hello, ma non sarà un exchange per un token di accesso. È possibile utilizzare hello [libreria MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) exchange hello toomake. In questo esempio, è stato configurato un callback di notifica nel middleware di OpenID Connect hello ogni volta che viene ricevuto un codice di autorizzazione. Callback hello, è utilizzare codice hello MSAL tooexchange per un token e salvare il token di hello nella cache di hello.

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a>Chiamata all'API web hello

Questa sezione viene descritto come token hello toouse ricevute durante sign-configurazione/Accedi con Azure Active Directory B2C nell'ordine tooaccess hello API web.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Recuperare il token hello salvato nei controller di hello

Hello `TasksController` è responsabile per la comunicazione con l'API web hello e per l'invio di tooread toohello API di richieste HTTP, creare ed eliminare le attività. Poiché l'API di hello è protetto da Azure Active Directory B2C, il token di hello recuperare toofirst che è stato salvato in hello sopra passaggio è necessario.

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a>Lettura delle attività da API web hello

Quando si dispone di un token, è possibile collegarlo toohello HTTP `GET` richiesta in hello `Authorization` chiamata toosecurely intestazione `TaskService`:

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Creare ed eliminare le attività del sito Web API hello

Seguire hello stesso schema quando si invia `POST` e `DELETE` richiede toohello API web, utilizzando un token di accesso MSAL tooretrieve hello dalla cache di hello.

## <a name="run-hello-sample-app"></a>Eseguire app di esempio hello

Infine, compilare ed eseguire entrambe le app hello. Iscriversi e accedere e creare attività per l'utente connesso di hello. Disconnettersi ed eseguire l'accesso usando un account utente diverso. Creare le attività per l'utente. Si noti come attività hello vengono archiviate per utente su hello API, poiché hello API estrae l'identità dell'utente hello dal token hello che riceve. Provare anche a riprodurre con ambiti hello. Rimuovere l'autorizzazione di hello troppo "scrittura" e quindi provare ad aggiungere un'attività. È sufficiente Assicurarsi che toosign out ogni volta che si modifica l'ambito di hello.

