---
title: v 2.0 aaaAzure AD .NET web API chiamata di app introduzione | Documenti Microsoft
description: Come toobuild un'App Web di MVC .NET che chiama servizi web mediante Microsoft personale degli account e di lavoro o scuola account per l'accesso.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a>Chiamare un'API Web da un'applicazione Web .NET
Con l'endpoint di hello v 2.0, è possibile aggiungere applicazioni web per l'autenticazione tooyour rapidamente e le API web con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.  Di seguito viene creata un'app Web MVC che consente agli utenti di accedere tramite OpenID Connect e con l'aiuto del middleware OWIN di Microsoft.  app web Hello consente di ottenere i token di accesso OAuth 2.0 per una web api protetta da OAuth 2.0 che consente di creare, leggere e delete su un determinato utente "elenco di attività".

In questa esercitazione verrà concentra principalmente sulle utilizzando MSAL tooacquire e utilizzare i token di accesso in un'app web, descritta in modo completo [qui](active-directory-v2-flows.md#web-apps).  Come prerequisito, è opportuno toofirst informazioni su come troppo[aggiungere app web di base Accedi tooa](active-directory-v2-devquickstarts-dotnet-web.md) o come troppo[proteggere correttamente un'API web](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Scaricare il codice di esempio
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o scheletro hello clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

In alternativa, è possibile [scaricare app hello completata come un file zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) o clone hello completato app:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).  Verificare di:

* Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.
* Creare un **segreto dell'App** di hello **Password** , tipo e copia verso il basso il valore per un momento successivo
* Aggiungere hello **Web** piattaforma per l'app.
* Immettere hello corretto **URI di reindirizzamento**. uri di reindirizzamento Hello indica tooAzure Active Directory in cui devono essere indirizzate le risposte di autenticazione: hello valore predefinito per questa esercitazione è `https://localhost:44326/`.

## <a name="install-owin"></a>Installare OWIN
Aggiungere hello OWIN middleware NuGet pacchetti toohello `TodoList-WebApp` progetto utilizzando hello Console di gestione pacchetti.  middleware OWIN Hello verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Utente hello Sign in
Configurare ora hello toouse middleware OWIN di hello [protocollo di autenticazione OpenID Connect](active-directory-v2-protocols.md).  

* Aprire hello `web.config` file nella radice di hello di hello `TodoList-WebApp` del progetto, quindi immettere i valori di configurazione dell'applicazione nella hello `<appSettings>` sezione.
  * Hello `ida:ClientId` è hello **Id applicazione** assegnato tooyour app nel portale di registrazione hello.
  * Hello `ida:ClientSecret` è hello **segreto dell'App** creato nel portale di registrazione hello.
  * Hello `ida:RedirectUri` è hello **Uri di reindirizzamento** immesso nel portale di hello.
* Aprire hello `web.config` file nella radice di hello di hello `TodoList-Service` progetti e sostituire hello `ida:Audience` con hello stesso **Id applicazione** come indicato in precedenza.
* File aperti hello `App_Start\Startup.Auth.cs` e aggiungere `using` istruzioni per le librerie di hello dall'alto.
* Nel file stesso hello, implementare hello `ConfigureAuth(...)` metodo.  parametri che vengono forniti in Hello `OpenIDConnectAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a>Utilizzare i token di accesso tooget MSAL
In hello `AuthorizationCodeReceived` notifica desideriamo toouse [OAuth 2.0 in combinazione con OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code per un toohello token di accesso servizio elenco attività da eseguire.  MSAL può semplificare questo processo.

* In primo luogo, installare la versione di anteprima hello di MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* E aggiungere un altro `using` toohello istruzione `App_Start\Startup.Auth.cs` file per MSAL.
* Aggiungere un nuovo metodo hello `OnAuthorizationCodeReceived` gestore dell'evento.  Questo gestore utilizzerà MSAL tooacquire un toohello token di accesso API elenco attività da eseguire e archivierà token hello nella cache dei token del MSAL per un momento successivo:

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* Nelle App web, MSAL ha una cache dei token estendibile che può essere utilizzati toostore token.  In questo esempio implementa hello `NaiveSessionCache` che utilizza i token toocache di archiviazione della sessione http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Chiamare l'API Web hello
Ora è tooactually utilizzare access_token hello acquisite nel passaggio 3.  Aprire hello web app `Controllers\TodoListController.cs` file, rendendo tutti hello CRUD richiede toohello API elenco attività da eseguire.

* È possibile utilizzare MSAL nuovamente qui access_tokens toofetch da hello cache MSAL.  Aggiungere innanzitutto un `using` istruzione per MSAL toothis file.
  
    `using Microsoft.Identity.Client;`
* In hello `Index` , utilizzare MSAL dell'azione `AcquireTokenSilentAsync` tooget metodo access_token che possono essere dati tooread utilizzato dal servizio elenco attività hello:

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* Hello viene quindi aggiunto hello risultante toohello token richiesta HTTP GET come hello `Authorization` intestazione, il servizio elenco attività hello utilizza richiesta hello tooauthenticate.
* Se il servizio elenco attività hello restituisce un `401 Unauthorized` risposta, access_tokens hello in MSAL diventate non valide per qualche motivo.  In questo caso, si deve eliminare qualsiasi access_tokens dalla cache MSAL hello e viene visualizzato il messaggio che può essere necessario toosign in nuovamente, che verrà riavviato il flusso di acquisizione del token hello utente hello.

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* Analogamente, se MSAL è Impossibile tooreturn access_token per qualsiasi motivo, è necessario indicare toosign utente hello in nuovamente.  Questo è semplice quanto individuare eventuali `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Hello esatta stesso `AcquireTokenSilentAsync` implementd in hello è chiamata `Create` e `Delete` azioni.  Nelle App web, è possibile utilizzare questo access_tokens di tooget metodo MSAL tutte le volte necessarie nell'applicazione.  L'acquisizione, la memorizzazione nella cache e l'aggiornamento dei token vengono gestiti da MSAL.

Infine compilare ed eseguire l'app.  Accedere con un Account Microsoft o un Account di Azure AD e notare come identità dell'utente hello si riflette nella barra di spostamento superiore hello.  Aggiungere ed eliminare alcuni elementi dall'elenco di attività dell'utente hello chiama hello toosee che OAuth 2.0 protetto API in azione.  Sono ora disponibili un'app e un'API Web protette che usano protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.

Per riferimento, hello completata esempio (senza i valori di configurazione) [sono disponibili](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Passaggi successivi
Per altre risorse, vedere:

* [Guida per sviluppatori v 2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

