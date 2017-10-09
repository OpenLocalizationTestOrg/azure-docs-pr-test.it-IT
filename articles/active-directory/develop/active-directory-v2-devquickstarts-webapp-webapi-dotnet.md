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
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="ca92a-103">Chiamare un'API Web da un'applicazione Web .NET</span><span class="sxs-lookup"><span data-stu-id="ca92a-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="ca92a-104">Con l'endpoint di hello v 2.0, è possibile aggiungere applicazioni web per l'autenticazione tooyour rapidamente e le API web con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="ca92a-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="ca92a-105">Di seguito viene creata un'app Web MVC che consente agli utenti di accedere tramite OpenID Connect e con l'aiuto del middleware OWIN di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ca92a-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="ca92a-106">app web Hello consente di ottenere i token di accesso OAuth 2.0 per una web api protetta da OAuth 2.0 che consente di creare, leggere e delete su un determinato utente "elenco di attività".</span><span class="sxs-lookup"><span data-stu-id="ca92a-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="ca92a-107">In questa esercitazione verrà concentra principalmente sulle utilizzando MSAL tooacquire e utilizzare i token di accesso in un'app web, descritta in modo completo [qui](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="ca92a-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="ca92a-108">Come prerequisito, è opportuno toofirst informazioni su come troppo[aggiungere app web di base Accedi tooa](active-directory-v2-devquickstarts-dotnet-web.md) o come troppo[proteggere correttamente un'API web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="ca92a-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ca92a-109">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="ca92a-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="ca92a-110">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ca92a-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="ca92a-111">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="ca92a-111">Download sample code</span></span>
<span data-ttu-id="ca92a-112">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="ca92a-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="ca92a-113">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="ca92a-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="ca92a-114">In alternativa, è possibile [scaricare app hello completata come un file zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) o clone hello completato app:</span><span class="sxs-lookup"><span data-stu-id="ca92a-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="ca92a-115">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="ca92a-115">Register an app</span></span>
<span data-ttu-id="ca92a-116">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ca92a-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="ca92a-117">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="ca92a-117">Make sure to:</span></span>

* <span data-ttu-id="ca92a-118">Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="ca92a-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="ca92a-119">Creare un **segreto dell'App** di hello **Password** , tipo e copia verso il basso il valore per un momento successivo</span><span class="sxs-lookup"><span data-stu-id="ca92a-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="ca92a-120">Aggiungere hello **Web** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="ca92a-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="ca92a-121">Immettere hello corretto **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="ca92a-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="ca92a-122">uri di reindirizzamento Hello indica tooAzure Active Directory in cui devono essere indirizzate le risposte di autenticazione: hello valore predefinito per questa esercitazione è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="ca92a-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="ca92a-123">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="ca92a-123">Install OWIN</span></span>
<span data-ttu-id="ca92a-124">Aggiungere hello OWIN middleware NuGet pacchetti toohello `TodoList-WebApp` progetto utilizzando hello Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ca92a-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="ca92a-125">middleware OWIN Hello verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="ca92a-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="ca92a-126">Utente hello Sign in</span><span class="sxs-lookup"><span data-stu-id="ca92a-126">Sign hello user in</span></span>
<span data-ttu-id="ca92a-127">Configurare ora hello toouse middleware OWIN di hello [protocollo di autenticazione OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ca92a-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="ca92a-128">Aprire hello `web.config` file nella radice di hello di hello `TodoList-WebApp` del progetto, quindi immettere i valori di configurazione dell'applicazione nella hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="ca92a-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="ca92a-129">Hello `ida:ClientId` è hello **Id applicazione** assegnato tooyour app nel portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="ca92a-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="ca92a-130">Hello `ida:ClientSecret` è hello **segreto dell'App** creato nel portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="ca92a-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="ca92a-131">Hello `ida:RedirectUri` è hello **Uri di reindirizzamento** immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="ca92a-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="ca92a-132">Aprire hello `web.config` file nella radice di hello di hello `TodoList-Service` progetti e sostituire hello `ida:Audience` con hello stesso **Id applicazione** come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ca92a-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="ca92a-133">File aperti hello `App_Start\Startup.Auth.cs` e aggiungere `using` istruzioni per le librerie di hello dall'alto.</span><span class="sxs-lookup"><span data-stu-id="ca92a-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="ca92a-134">Nel file stesso hello, implementare hello `ConfigureAuth(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="ca92a-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="ca92a-135">parametri che vengono forniti in Hello `OpenIDConnectAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca92a-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="ca92a-136">Utilizzare i token di accesso tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="ca92a-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="ca92a-137">In hello `AuthorizationCodeReceived` notifica desideriamo toouse [OAuth 2.0 in combinazione con OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code per un toohello token di accesso servizio elenco attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="ca92a-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="ca92a-138">MSAL può semplificare questo processo.</span><span class="sxs-lookup"><span data-stu-id="ca92a-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="ca92a-139">In primo luogo, installare la versione di anteprima hello di MSAL:</span><span class="sxs-lookup"><span data-stu-id="ca92a-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="ca92a-140">E aggiungere un altro `using` toohello istruzione `App_Start\Startup.Auth.cs` file per MSAL.</span><span class="sxs-lookup"><span data-stu-id="ca92a-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="ca92a-141">Aggiungere un nuovo metodo hello `OnAuthorizationCodeReceived` gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ca92a-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="ca92a-142">Questo gestore utilizzerà MSAL tooacquire un toohello token di accesso API elenco attività da eseguire e archivierà token hello nella cache dei token del MSAL per un momento successivo:</span><span class="sxs-lookup"><span data-stu-id="ca92a-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

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

* <span data-ttu-id="ca92a-143">Nelle App web, MSAL ha una cache dei token estendibile che può essere utilizzati toostore token.</span><span class="sxs-lookup"><span data-stu-id="ca92a-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="ca92a-144">In questo esempio implementa hello `NaiveSessionCache` che utilizza i token toocache di archiviazione della sessione http.</span><span class="sxs-lookup"><span data-stu-id="ca92a-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="ca92a-145">Chiamare l'API Web hello</span><span class="sxs-lookup"><span data-stu-id="ca92a-145">Call hello Web API</span></span>
<span data-ttu-id="ca92a-146">Ora è tooactually utilizzare access_token hello acquisite nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="ca92a-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="ca92a-147">Aprire hello web app `Controllers\TodoListController.cs` file, rendendo tutti hello CRUD richiede toohello API elenco attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="ca92a-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="ca92a-148">È possibile utilizzare MSAL nuovamente qui access_tokens toofetch da hello cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="ca92a-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="ca92a-149">Aggiungere innanzitutto un `using` istruzione per MSAL toothis file.</span><span class="sxs-lookup"><span data-stu-id="ca92a-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="ca92a-150">In hello `Index` , utilizzare MSAL dell'azione `AcquireTokenSilentAsync` tooget metodo access_token che possono essere dati tooread utilizzato dal servizio elenco attività hello:</span><span class="sxs-lookup"><span data-stu-id="ca92a-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

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

* <span data-ttu-id="ca92a-151">Hello viene quindi aggiunto hello risultante toohello token richiesta HTTP GET come hello `Authorization` intestazione, il servizio elenco attività hello utilizza richiesta hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="ca92a-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="ca92a-152">Se il servizio elenco attività hello restituisce un `401 Unauthorized` risposta, access_tokens hello in MSAL diventate non valide per qualche motivo.</span><span class="sxs-lookup"><span data-stu-id="ca92a-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="ca92a-153">In questo caso, si deve eliminare qualsiasi access_tokens dalla cache MSAL hello e viene visualizzato il messaggio che può essere necessario toosign in nuovamente, che verrà riavviato il flusso di acquisizione del token hello utente hello.</span><span class="sxs-lookup"><span data-stu-id="ca92a-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

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

* <span data-ttu-id="ca92a-154">Analogamente, se MSAL è Impossibile tooreturn access_token per qualsiasi motivo, è necessario indicare toosign utente hello in nuovamente.</span><span class="sxs-lookup"><span data-stu-id="ca92a-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="ca92a-155">Questo è semplice quanto individuare eventuali `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="ca92a-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="ca92a-156">Hello esatta stesso `AcquireTokenSilentAsync` implementd in hello è chiamata `Create` e `Delete` azioni.</span><span class="sxs-lookup"><span data-stu-id="ca92a-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="ca92a-157">Nelle App web, è possibile utilizzare questo access_tokens di tooget metodo MSAL tutte le volte necessarie nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca92a-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="ca92a-158">L'acquisizione, la memorizzazione nella cache e l'aggiornamento dei token vengono gestiti da MSAL.</span><span class="sxs-lookup"><span data-stu-id="ca92a-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="ca92a-159">Infine compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="ca92a-159">Finally, build and run your app!</span></span>  <span data-ttu-id="ca92a-160">Accedere con un Account Microsoft o un Account di Azure AD e notare come identità dell'utente hello si riflette nella barra di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="ca92a-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="ca92a-161">Aggiungere ed eliminare alcuni elementi dall'elenco di attività dell'utente hello chiama hello toosee che OAuth 2.0 protetto API in azione.</span><span class="sxs-lookup"><span data-stu-id="ca92a-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="ca92a-162">Sono ora disponibili un'app e un'API Web protette che usano protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="ca92a-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="ca92a-163">Per riferimento, hello completata esempio (senza i valori di configurazione) [sono disponibili](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ca92a-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ca92a-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca92a-164">Next Steps</span></span>
<span data-ttu-id="ca92a-165">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="ca92a-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="ca92a-166">Guida per sviluppatori v 2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="ca92a-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="ca92a-167">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="ca92a-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="ca92a-168">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="ca92a-168">Get security updates for our products</span></span>
<span data-ttu-id="ca92a-169">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="ca92a-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

