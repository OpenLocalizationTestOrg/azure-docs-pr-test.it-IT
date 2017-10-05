---
title: Introduzione alla chiamata di API da un'App Web Azure AD v2.0 .NET| Documentazione Microsoft
description: Come creare un'app Web .NET MVC che chiama servizi Web usando account Microsoft personali, aziendali e dell'istituto di istruzione per l'accesso.
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="5bea9-103">Chiamare un'API Web da un'applicazione Web .NET</span><span class="sxs-lookup"><span data-stu-id="5bea9-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="5bea9-104">Con l'endpoint v2.0 è possibile aggiungere rapidamente l'autenticazione alle app Web e alle API Web con supporto per account Microsoft personali, aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="5bea9-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="5bea9-105">Di seguito viene creata un'app Web MVC che consente agli utenti di accedere tramite OpenID Connect e con l'aiuto del middleware OWIN di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5bea9-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="5bea9-106">L'applicazione Web otterrà i token di accesso OAuth 2.0 per un'api Web protetta da OAuth 2.0 che consente di creare, leggere ed eliminare le voci dell'elenco attività di un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="5bea9-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="5bea9-107">Questa esercitazione è incentrata principalmente sull'uso di MSAL per l'acquisizione e l'uso di token di accesso in un'app Web, la cui descrizione dettagliata è disponibile [qui](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="5bea9-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="5bea9-108">Come prerequisiti, è consigliabile apprendere come [aggiungere l'accesso base a un'app Web](active-directory-v2-devquickstarts-dotnet-web.md) o come [proteggere correttamente un'API Web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="5bea9-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5bea9-109">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="5bea9-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="5bea9-110">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5bea9-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="5bea9-111">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="5bea9-111">Download sample code</span></span>
<span data-ttu-id="5bea9-112">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="5bea9-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="5bea9-113">Per seguire la procedura è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="5bea9-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="5bea9-114">In alternativa, è possibile [scaricare l'app completata come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) oppure clonare l'app completata:</span><span class="sxs-lookup"><span data-stu-id="5bea9-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="5bea9-115">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="5bea9-115">Register an app</span></span>
<span data-ttu-id="5bea9-116">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5bea9-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="5bea9-117">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="5bea9-117">Make sure to:</span></span>

* <span data-ttu-id="5bea9-118">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="5bea9-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="5bea9-119">Creare una **Chiave privata app** di tipo **Password** e copiare il relativo valore per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="5bea9-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="5bea9-120">Aggiungere la piattaforma **Web** per l'app.</span><span class="sxs-lookup"><span data-stu-id="5bea9-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="5bea9-121">Immettere l' **URI di reindirizzamento**corretto.</span><span class="sxs-lookup"><span data-stu-id="5bea9-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="5bea9-122">L'URI di reindirizzamento indica ad Azure AD dove indirizzare le risposte di autenticazione. Il valore predefinito per questa esercitazione è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="5bea9-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="5bea9-123">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="5bea9-123">Install OWIN</span></span>
<span data-ttu-id="5bea9-124">Aggiungere i pacchetti NuGet del middleware OWIN al progetto `TodoList-WebApp` tramite la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5bea9-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="5bea9-125">Il middleware OWIN verrà usato, tra le altre cose, per inviare le richieste di accesso e disconnessione, gestire la sessione dell'utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="5bea9-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="5bea9-126">Connettere l'utente all'app</span><span class="sxs-lookup"><span data-stu-id="5bea9-126">Sign the user in</span></span>
<span data-ttu-id="5bea9-127">Configurare il middleware OWIN per l'uso del [protocollo di autenticazione OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="5bea9-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="5bea9-128">Aprire il file `web.config` nella radice del progetto `TodoList-WebApp` e immettere i valori di configurazione dell'app nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="5bea9-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="5bea9-129">`ida:ClientId` rappresenta l' **ID applicazione** assegnato all'app nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="5bea9-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="5bea9-130">`ida:ClientSecret` rappresenta la **chiave privata app** creata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="5bea9-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="5bea9-131">`ida:RedirectUri` rappresenta l' **URI di reindirizzamento** immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="5bea9-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="5bea9-132">Aprire il file `web.config` nella radice del progetto `TodoList-Service` e sostituire `ida:Audience` con lo stesso **ID applicazione** di cui sopra.</span><span class="sxs-lookup"><span data-stu-id="5bea9-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="5bea9-133">Aprire il file `App_Start\Startup.Auth.cs` e aggiungere istruzioni `using` per le librerie indicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5bea9-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="5bea9-134">Nello stesso file, implementare il metodo `ConfigureAuth(...)` .</span><span class="sxs-lookup"><span data-stu-id="5bea9-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="5bea9-135">I parametri forniti in `OpenIDConnectAuthenticationOptions` fungeranno da coordinate per consentire all'app di comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bea9-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="5bea9-136">Usare MSAL per ottenere i token di accesso</span><span class="sxs-lookup"><span data-stu-id="5bea9-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="5bea9-137">Nella notifica `AuthorizationCodeReceived` si desidera usare [OAuth 2.0 in parallelo con OpenID Connect](active-directory-v2-protocols.md) per riscattare l'authorization_code per un token di accesso al servizio To Do List.</span><span class="sxs-lookup"><span data-stu-id="5bea9-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="5bea9-138">MSAL può semplificare questo processo.</span><span class="sxs-lookup"><span data-stu-id="5bea9-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="5bea9-139">Per prima cosa installare la versione di anteprima di MSAL:</span><span class="sxs-lookup"><span data-stu-id="5bea9-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="5bea9-140">Aggiungere quindi un'altra istruzione `using`al file `App_Start\Startup.Auth.cs` per MSAL.</span><span class="sxs-lookup"><span data-stu-id="5bea9-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="5bea9-141">Aggiungere ora un nuovo metodo, il gestore eventi `OnAuthorizationCodeReceived`.</span><span class="sxs-lookup"><span data-stu-id="5bea9-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="5bea9-142">Questo gestore userà MSAL per acquisire un token di accesso per l'API To Do List e archivierà il token nella cache dei token di MSAL per usi successivi:</span><span class="sxs-lookup"><span data-stu-id="5bea9-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="5bea9-143">Nelle app Web, MSAL ha una cache di token estendibile che può essere usata per archiviare i token.</span><span class="sxs-lookup"><span data-stu-id="5bea9-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="5bea9-144">Questo esempio implementa `NaiveSessionCache` che usa lo spazio di archiviazione della sessione HTTP per la memorizzazione dei token nella cache.</span><span class="sxs-lookup"><span data-stu-id="5bea9-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="5bea9-145">Chiamare l'API Web</span><span class="sxs-lookup"><span data-stu-id="5bea9-145">Call the Web API</span></span>
<span data-ttu-id="5bea9-146">È ora possibile usare il token di accesso acquisito al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="5bea9-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="5bea9-147">Aprire il file `Controllers\TodoListController.cs` dell'app Web, che esegue tutte le richieste CRUD all'API To Do List.</span><span class="sxs-lookup"><span data-stu-id="5bea9-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="5bea9-148">È possibile usare nuovamente MSAL per recuperare i token di accesso dalla cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="5bea9-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="5bea9-149">Per prima cosa aggiungere un'istruzione `using` per MSAL a questo file.</span><span class="sxs-lookup"><span data-stu-id="5bea9-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="5bea9-150">Nell'azione `Index` usare il metodo `AcquireTokenSilentAsync` di MSAL per ottenere un token di accesso da usare per leggere i dati dal servizio To Do List:</span><span class="sxs-lookup"><span data-stu-id="5bea9-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="5bea9-151">L'esempio aggiunge quindi il token risultante alla richiesta HTTP GET come intestazione `Authorization`, usata dal servizio To Do List per autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="5bea9-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="5bea9-152">Se il servizio To Do List restituisce una risposta `401 Unauthorized`, significa che i token di accesso in MSAL per qualche motivo non sono più validi.</span><span class="sxs-lookup"><span data-stu-id="5bea9-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="5bea9-153">In questo caso, è consigliabile eliminare tutti i token di accesso dalla cache MSAL e visualizzare all'utente un messaggio che comunica che potrebbe essere necessario eseguire un nuovo accesso. In questo modo verrà riavviato il flusso di acquisizione dei token.</span><span class="sxs-lookup"><span data-stu-id="5bea9-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="5bea9-154">Analogamente, se per qualsiasi motivo MSAL non riesce a restituire un token di accesso, è consigliabile chiedere all'utente di eseguire di nuovo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="5bea9-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="5bea9-155">Questo è semplice quanto individuare eventuali `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="5bea9-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="5bea9-156">La stessa identica chiamata `AcquireTokenSilentAsync` viene implementata nelle azioni `Create` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="5bea9-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="5bea9-157">Nelle app Web è possibile usare questo metodo MSAL per ottenere i token di accesso ogni volta che sono necessari nell'app.</span><span class="sxs-lookup"><span data-stu-id="5bea9-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="5bea9-158">L'acquisizione, la memorizzazione nella cache e l'aggiornamento dei token vengono gestiti da MSAL.</span><span class="sxs-lookup"><span data-stu-id="5bea9-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="5bea9-159">Infine compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="5bea9-159">Finally, build and run your app!</span></span>  <span data-ttu-id="5bea9-160">Accedere con un account Microsoft o con un account Azure AD e osservare che l'identità dell'utente sia visibile nella barra di spostamento superiore.</span><span class="sxs-lookup"><span data-stu-id="5bea9-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="5bea9-161">Aggiungere ed eliminare alcuni elementi dall'elenco di attività dell'utente per vedere le chiamate API protette OAuth 2.0 in azione.</span><span class="sxs-lookup"><span data-stu-id="5bea9-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="5bea9-162">Sono ora disponibili un'app e un'API Web protette che usano protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="5bea9-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="5bea9-163">Come riferimento, viene fornito l'esempio completato (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5bea9-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5bea9-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5bea9-164">Next Steps</span></span>
<span data-ttu-id="5bea9-165">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="5bea9-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="5bea9-166">Guida per sviluppatori v2.0 >></span><span class="sxs-lookup"><span data-stu-id="5bea9-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="5bea9-167">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="5bea9-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="5bea9-168">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="5bea9-168">Get security updates for our products</span></span>
<span data-ttu-id="5bea9-169">È consigliabile ricevere notifiche in caso di problemi di sicurezza. A tale scopo, visitare [questa pagina](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5bea9-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

