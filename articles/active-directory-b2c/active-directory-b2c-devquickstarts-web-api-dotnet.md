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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="92648-103">Azure AD B2C: Chiamare un'API Web .NET da un'app Web .NET</span><span class="sxs-lookup"><span data-stu-id="92648-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="92648-104">Tramite Azure Active Directory B2C, è possibile aggiungere identità potente Gestione funzionalità tooyour web App e API web.</span><span class="sxs-lookup"><span data-stu-id="92648-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="92648-105">In questo articolo illustra il funzionamento di token di accesso e di effettuare chiamate da un "elenco".NET toorequest tooa app web .NET web api.</span><span class="sxs-lookup"><span data-stu-id="92648-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="92648-106">In questo articolo non viene illustrata la modalità tooimplement Accedi, sottoscrizione e il profilo di gestione con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="92648-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="92648-107">Si concentra sulle API web chiamante dopo hello è già autenticato.</span><span class="sxs-lookup"><span data-stu-id="92648-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="92648-108">Se lo si è già fatto, è necessario fare:</span><span class="sxs-lookup"><span data-stu-id="92648-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="92648-109">un'introduzione alle [app Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="92648-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="92648-110">un'introduzione alle [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="92648-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="92648-111">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="92648-111">Prerequisite</span></span>

<span data-ttu-id="92648-112">toobuild un'applicazione web che chiama una web api, è necessario:</span><span class="sxs-lookup"><span data-stu-id="92648-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="92648-113">[Creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="92648-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="92648-114">[Registrare un'API Web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="92648-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="92648-115">[Registrare un'app Web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="92648-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="92648-116">[Configurare i criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="92648-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="92648-117">[GRANT prova web app autorizzazioni toouse prova web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="92648-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92648-118">un'applicazione client Hello e API web devono utilizzare directory B2C hello stesso Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92648-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="92648-119">Scaricare codice hello</span><span class="sxs-lookup"><span data-stu-id="92648-119">Download hello code</span></span>

<span data-ttu-id="92648-120">codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="92648-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="92648-121">È possibile clonare: esempio hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="92648-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="92648-122">Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92648-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="92648-123">file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="92648-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="92648-124">`TaskWebApp`è un'applicazione web MVC hello utente interagisce con.</span><span class="sxs-lookup"><span data-stu-id="92648-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="92648-125">`TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="92648-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="92648-126">In questo articolo non viene illustrata la compilazione hello `TaskWebApp` app web o hello `TaskService` web api.</span><span class="sxs-lookup"><span data-stu-id="92648-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="92648-127">toolearn come toobuild hello .NET web app usando Azure Active Directory B2C, vedere il nostro [esercitazione di app web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="92648-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="92648-128">toolearn come toobuild hello .NET web API protetta con Azure Active Directory B2C, vedere il nostro [esercitazione API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92648-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="92648-129">Aggiornare la configurazione di hello Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="92648-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="92648-130">L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="92648-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="92648-131">Se si desidera toouse il proprio tenant:</span><span class="sxs-lookup"><span data-stu-id="92648-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="92648-132">Aprire `web.config` in hello `TaskService` progetti e sostituire i valori hello per</span><span class="sxs-lookup"><span data-stu-id="92648-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="92648-133">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="92648-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="92648-134">`ida:ClientId` con l'ID dell'applicazione API Web</span><span class="sxs-lookup"><span data-stu-id="92648-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="92648-135">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="92648-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="92648-136">Aprire `web.config` in hello `TaskWebApp` progetti e sostituire i valori hello per</span><span class="sxs-lookup"><span data-stu-id="92648-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="92648-137">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="92648-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="92648-138">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="92648-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="92648-139">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="92648-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="92648-140">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="92648-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="92648-141">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="92648-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="92648-142">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="92648-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="92648-143">Richiesta e salvataggio di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="92648-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="92648-144">Specificare le autorizzazioni di hello</span><span class="sxs-lookup"><span data-stu-id="92648-144">Specify hello permissions</span></span>

<span data-ttu-id="92648-145">In ordine toomake hello chiamata toohello API web, è necessario utente hello tooauthenticate (tramite il criterio sign-configurazione/Accedi) e [ricevere un token di accesso](active-directory-b2c-access-tokens.md) da Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="92648-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="92648-146">In ordine tooreceive un token di accesso, è necessario specificare le autorizzazioni di hello desideri toogrant token di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="92648-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="92648-147">le autorizzazioni di Hello sono specificate in hello `scope` parametro quando si apportata hello richiesta toohello `/authorize` endpoint.</span><span class="sxs-lookup"><span data-stu-id="92648-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="92648-148">Ad esempio, un token di accesso con hello "Leggi" applicazione della risorsa autorizzazione toohello con tooacquire hello URI ID App del `https://contoso.onmicrosoft.com/tasks`, ambito hello sarebbe `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="92648-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="92648-149">ambito hello toospecify nel file di esempio, aprire hello `App_Start\Startup.Auth.cs` e definire hello `Scope` variabile OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="92648-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="92648-150">Codice di autorizzazione hello per un token di accesso di Exchange</span><span class="sxs-lookup"><span data-stu-id="92648-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="92648-151">Al termine dell'esperienza di iscrizione o accesso hello un utente, l'applicazione riceverà un codice di autorizzazione da Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="92648-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="92648-152">middleware OWIN OpenID Connect Hello archivierà il codice hello, ma non sarà un exchange per un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="92648-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="92648-153">È possibile utilizzare hello [libreria MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) exchange hello toomake.</span><span class="sxs-lookup"><span data-stu-id="92648-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="92648-154">In questo esempio, è stato configurato un callback di notifica nel middleware di OpenID Connect hello ogni volta che viene ricevuto un codice di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="92648-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="92648-155">Callback hello, è utilizzare codice hello MSAL tooexchange per un token e salvare il token di hello nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="92648-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

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

## <a name="calling-hello-web-api"></a><span data-ttu-id="92648-156">Chiamata all'API web hello</span><span class="sxs-lookup"><span data-stu-id="92648-156">Calling hello web API</span></span>

<span data-ttu-id="92648-157">Questa sezione viene descritto come token hello toouse ricevute durante sign-configurazione/Accedi con Azure Active Directory B2C nell'ordine tooaccess hello API web.</span><span class="sxs-lookup"><span data-stu-id="92648-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="92648-158">Recuperare il token hello salvato nei controller di hello</span><span class="sxs-lookup"><span data-stu-id="92648-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="92648-159">Hello `TasksController` è responsabile per la comunicazione con l'API web hello e per l'invio di tooread toohello API di richieste HTTP, creare ed eliminare le attività.</span><span class="sxs-lookup"><span data-stu-id="92648-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="92648-160">Poiché l'API di hello è protetto da Azure Active Directory B2C, il token di hello recuperare toofirst che è stato salvato in hello sopra passaggio è necessario.</span><span class="sxs-lookup"><span data-stu-id="92648-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

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

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="92648-161">Lettura delle attività da API web hello</span><span class="sxs-lookup"><span data-stu-id="92648-161">Read tasks from hello web API</span></span>

<span data-ttu-id="92648-162">Quando si dispone di un token, è possibile collegarlo toohello HTTP `GET` richiesta in hello `Authorization` chiamata toosecurely intestazione `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="92648-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="92648-163">Creare ed eliminare le attività del sito Web API hello</span><span class="sxs-lookup"><span data-stu-id="92648-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="92648-164">Seguire hello stesso schema quando si invia `POST` e `DELETE` richiede toohello API web, utilizzando un token di accesso MSAL tooretrieve hello dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="92648-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="92648-165">Eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="92648-165">Run hello sample app</span></span>

<span data-ttu-id="92648-166">Infine, compilare ed eseguire entrambe le app hello.</span><span class="sxs-lookup"><span data-stu-id="92648-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="92648-167">Iscriversi e accedere e creare attività per l'utente connesso di hello.</span><span class="sxs-lookup"><span data-stu-id="92648-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="92648-168">Disconnettersi ed eseguire l'accesso usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="92648-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="92648-169">Creare le attività per l'utente.</span><span class="sxs-lookup"><span data-stu-id="92648-169">Create tasks for that user.</span></span> <span data-ttu-id="92648-170">Si noti come attività hello vengono archiviate per utente su hello API, poiché hello API estrae l'identità dell'utente hello dal token hello che riceve.</span><span class="sxs-lookup"><span data-stu-id="92648-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="92648-171">Provare anche a riprodurre con ambiti hello.</span><span class="sxs-lookup"><span data-stu-id="92648-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="92648-172">Rimuovere l'autorizzazione di hello troppo "scrittura" e quindi provare ad aggiungere un'attività.</span><span class="sxs-lookup"><span data-stu-id="92648-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="92648-173">È sufficiente Assicurarsi che toosign out ogni volta che si modifica l'ambito di hello.</span><span class="sxs-lookup"><span data-stu-id="92648-173">Just make sure toosign out each time you change hello scope.</span></span>

