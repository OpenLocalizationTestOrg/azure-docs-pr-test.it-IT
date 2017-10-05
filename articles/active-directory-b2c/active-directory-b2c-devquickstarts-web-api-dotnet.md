---
title: Azure Active Directory B2C | Documentazione Microsoft
description: Come compilare un'app Web .NET e chiamare un API Web usando Azure Active Directory B2C i token di accesso OAuth 2.0.
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
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="c8d4b-103">Azure AD B2C: Chiamare un'API Web .NET da un'app Web .NET</span><span class="sxs-lookup"><span data-stu-id="c8d4b-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="c8d4b-104">Tramite Azure AD B2C, è possibile aggiungere potenti funzionalità di gestione di identità per l'app Web e le API.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="c8d4b-105">In questo articolo viene illustrato come richiedere i token di accesso ed effettuare chiamate da un'app Web "elenco attività" .NET per API Web .NET.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="c8d4b-106">Questo articolo non descrive come implementare le esperienze di accesso, iscrizione e gestione del profilo con Azure AD B2C,</span><span class="sxs-lookup"><span data-stu-id="c8d4b-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="c8d4b-107">ma illustra la chiamata delle API Web dopo che l'utente ha già effettuato l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="c8d4b-108">Se lo si è già fatto, è necessario fare:</span><span class="sxs-lookup"><span data-stu-id="c8d4b-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="c8d4b-109">un'introduzione alle [app Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="c8d4b-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="c8d4b-110">un'introduzione alle [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="c8d4b-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="c8d4b-111">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="c8d4b-111">Prerequisite</span></span>

<span data-ttu-id="c8d4b-112">Per compilare un'app Web che chiama un'API Web è necessario:</span><span class="sxs-lookup"><span data-stu-id="c8d4b-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="c8d4b-113">[Creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="c8d4b-114">[Registrare un'API Web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="c8d4b-115">[Registrare un'app Web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="c8d4b-116">[Configurare i criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="c8d4b-117">[Concedere le autorizzazioni all'app Web per usare le API Web](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8d4b-118">L'applicazione client e l'API Web devono usare la stessa directory di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="c8d4b-119">Scaricare il codice</span><span class="sxs-lookup"><span data-stu-id="c8d4b-119">Download the code</span></span>

<span data-ttu-id="c8d4b-120">Il codice per questa esercitazione è salvato su [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="c8d4b-121">È possibile clonare l'esempio eseguendo:</span><span class="sxs-lookup"><span data-stu-id="c8d4b-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="c8d4b-122">Dopo aver scaricato il codice di esempio, aprire il file SLN di Visual Studio per iniziare.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="c8d4b-123">Il file della soluzione contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="c8d4b-124">`TaskWebApp` è un'applicazione Web MVC con cui l'utente interagisce.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="c8d4b-125">`TaskService` è l'API Web back-end dell'app in cui viene archiviato l'elenco attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="c8d4b-126">Questo articolo non descrive la compilazione dell'app Web `TaskWebApp` o delle API Web `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="c8d4b-127">Per informazioni su come compilare un'app Web .NET usando Azure AD B2C, vedere l'[esercitazione sulle app Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="c8d4b-128">Per informazioni su come compilare l'API Web .NET usando Azure AD B2C, vedere l'[esercitazione sulle API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c8d4b-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="c8d4b-129">Aggiornare la configurazione di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c8d4b-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="c8d4b-130">L'esempio è configurato per l'uso dei criteri e dell'ID client del tenant demo.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="c8d4b-131">Se si desidera usare il proprio tenant:</span><span class="sxs-lookup"><span data-stu-id="c8d4b-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="c8d4b-132">Aprire `web.config` nel progetto `TaskService` e sostituire i valori di</span><span class="sxs-lookup"><span data-stu-id="c8d4b-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="c8d4b-133">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="c8d4b-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="c8d4b-134">`ida:ClientId` con l'ID dell'applicazione API Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="c8d4b-135">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="c8d4b-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="c8d4b-136">Aprire `web.config` nel progetto `TaskWebApp` e sostituire i valori di</span><span class="sxs-lookup"><span data-stu-id="c8d4b-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="c8d4b-137">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="c8d4b-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="c8d4b-138">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="c8d4b-139">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="c8d4b-140">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="c8d4b-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="c8d4b-141">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="c8d4b-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="c8d4b-142">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="c8d4b-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="c8d4b-143">Richiesta e salvataggio di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="c8d4b-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="c8d4b-144">Specificare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="c8d4b-144">Specify the permissions</span></span>

<span data-ttu-id="c8d4b-145">Per poter effettuare la chiamata all'API Web, è necessario autenticare l'utente (tramite i criteri di registrazione o accesso) e [ricevere un token di accesso](active-directory-b2c-access-tokens.md) da Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="c8d4b-146">Per ricevere un token di accesso, è necessario specificare le autorizzazioni che si desidera concedere al token di accesso.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="c8d4b-147">Le autorizzazioni vengono specificate nel parametro `scope` quando si effettua la richiesta per l'endpoint `/authorize`.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="c8d4b-148">Ad esempio, per acquisire un token di accesso con l'autorizzazione "lettura" per l'applicazione della risorsa con l'URI ID App di `https://contoso.onmicrosoft.com/tasks`, l'ambito sarà `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="c8d4b-149">Per specificare l'ambito nell'esempio, aprire il file `App_Start\Startup.Auth.cs` e definire la variabile `Scope` in OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="c8d4b-150">Scambiare il codice di autorizzazione con un token di accesso</span><span class="sxs-lookup"><span data-stu-id="c8d4b-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="c8d4b-151">Al termine dell'esperienza di iscrizione o accesso dell'utente, l'applicazione riceverà un codice di autorizzazione da Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="c8d4b-152">Il middleware OWIN OpenID Connect archivierà il codice, ma non lo scambierà per un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="c8d4b-153">È possibile usare la [libreria MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) per fare lo scambio.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="c8d4b-154">Nell'esempio, è stato configurato un callback di notifica nel middleware OpenID Connect ogni volta che viene ricevuto un codice di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="c8d4b-155">Nel callback viene usato MSAL per scambiare il codice con un token e salvare il token nella cache.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="c8d4b-156">Chiamata dell'API Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-156">Calling the web API</span></span>

<span data-ttu-id="c8d4b-157">Questa sezione illustra come usare il token ricevuto durante la registrazione o l'accesso con Azure AD B2C per accedere a un'API Web.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="c8d4b-158">Recuperare il token salvato nei controller</span><span class="sxs-lookup"><span data-stu-id="c8d4b-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="c8d4b-159">`TasksController` è responsabile della comunicazione con l'API Web e dell'invio di richieste HTTP all'API per la lettura, la creazione e l'eliminazione di attività.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="c8d4b-160">Poiché che l'API è protetta da Azure AD B2C, per prima cosa è necessario recuperare il token salvato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="c8d4b-161">Leggere le attività dall'API Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-161">Read tasks from the web API</span></span>

<span data-ttu-id="c8d4b-162">Dopo aver ottenuto un token, collegarlo alla richiesta HTTP `GET` nell'intestazione `Authorization` per chiamare `TaskService` in modo sicuro:</span><span class="sxs-lookup"><span data-stu-id="c8d4b-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="c8d4b-163">Creare ed eliminare attività nell'API Web</span><span class="sxs-lookup"><span data-stu-id="c8d4b-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="c8d4b-164">Seguire lo stesso modello quando si inviano le richieste `POST` e `DELETE` all'API Web, usando MSAL per recuperare il token di accesso dalla cache.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="c8d4b-165">Eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="c8d4b-165">Run the sample app</span></span>

<span data-ttu-id="c8d4b-166">Infine, compilare ed eseguire entrambe le app.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="c8d4b-167">Eseguire l'iscrizione e l'accesso e creare attività per l'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="c8d4b-168">Disconnettersi ed eseguire l'accesso usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="c8d4b-169">Creare le attività per l'utente.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-169">Create tasks for that user.</span></span> <span data-ttu-id="c8d4b-170">Si noti che le attività sono archiviate per ogni utente nell'API, perché l'API estrae l'identità dell'utente dai token che riceve.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="c8d4b-171">Provare inoltre a usare gli ambiti.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-171">Also try playing with the scopes.</span></span> <span data-ttu-id="c8d4b-172">Rimuovere l'autorizzazione "scrivere" e quindi provare ad aggiungere un'attività.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="c8d4b-173">Basta assicurarsi di disconnettersi ogni volta che si modifica l'ambito.</span><span class="sxs-lookup"><span data-stu-id="c8d4b-173">Just make sure to sign out each time you change the scope.</span></span>

