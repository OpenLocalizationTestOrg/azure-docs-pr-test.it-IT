---
title: Aggiungere informazioni di accesso a un'API Web .NET MVC usando l'endpoint 2.0 di Azure AD | Documentazione Microsoft
description: Come creare un'API Web .NET MVC che accetta token da account Microsoft personali, aziendali e dell'istituto di istruzione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="ab54a-103">Proteggere un'API Web MVC</span><span class="sxs-lookup"><span data-stu-id="ab54a-103">Secure an MVC web API</span></span>
<span data-ttu-id="ab54a-104">Con l'endpoint v2.0 di Azure Active Directory è possibile proteggere un'API Web usando token di accesso [OAuth 2.0](active-directory-v2-protocols.md) in modo da consentire agli utenti di accedere all'API Web in modo sicuro con un account Microsoft personale, aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="ab54a-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="ab54a-105">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab54a-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="ab54a-106">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ab54a-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="ab54a-107">Nelle API Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="ab54a-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="ab54a-108">Verrà usato OWIN per compilare un'API Web MVC "Elenco attività" che consente ai client di creare e leggere le attività dall'elenco di attività dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ab54a-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="ab54a-109">L'API Web verifica che le richieste in ingresso contengano un token di accesso valido e rifiuta le richieste che non superano la convalida su una route protetta.</span><span class="sxs-lookup"><span data-stu-id="ab54a-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="ab54a-110">Questo esempio è stato creato con Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ab54a-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="ab54a-111">Scaricare</span><span class="sxs-lookup"><span data-stu-id="ab54a-111">Download</span></span>
<span data-ttu-id="ab54a-112">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="ab54a-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="ab54a-113">Per seguire la procedura è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="ab54a-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="ab54a-114">Lo scheletro di un'app include tutto il codice boilerplate per una semplice API, ma non tutte le parti relative all'identità.</span><span class="sxs-lookup"><span data-stu-id="ab54a-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="ab54a-115">Se non si vuole proseguire, in alternativa è possibile clonare o [scaricare l'esempio completo](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ab54a-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="ab54a-116">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="ab54a-116">Register an app</span></span>
<span data-ttu-id="ab54a-117">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ab54a-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="ab54a-118">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="ab54a-118">Make sure to:</span></span>

* <span data-ttu-id="ab54a-119">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="ab54a-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="ab54a-120">Questa soluzione di visual studio contiene anche una "TodoListClient", che è una semplice applicazione WPF.</span><span class="sxs-lookup"><span data-stu-id="ab54a-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="ab54a-121">La TodoListClient viene utilizzata per illustrare come avviene l’accesso dell'utente e come un client può inviare le richieste all’API Web.</span><span class="sxs-lookup"><span data-stu-id="ab54a-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="ab54a-122">In questo caso, sia TodoListClient sia il TodoListService sono rappresentati dalla stessa app.</span><span class="sxs-lookup"><span data-stu-id="ab54a-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="ab54a-123">Per configurare il TodoListClient, è necessario inoltre:</span><span class="sxs-lookup"><span data-stu-id="ab54a-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="ab54a-124">Aggiungere la piattaforma **Mobile** per l'app.</span><span class="sxs-lookup"><span data-stu-id="ab54a-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="ab54a-125">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="ab54a-125">Install OWIN</span></span>
<span data-ttu-id="ab54a-126">Dopo aver registrato un'app, si dovrà configurarla in modo che comunichi con l'endpoint v 2.0 per convalidare le richieste in ingresso e i token.</span><span class="sxs-lookup"><span data-stu-id="ab54a-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="ab54a-127">Per iniziare, aprire la soluzione e aggiungere i pacchetti NuGet del middleware OWIN al progetto TodoListService usando la Console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ab54a-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="ab54a-128">Configurare l'autenticazione OAuth</span><span class="sxs-lookup"><span data-stu-id="ab54a-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="ab54a-129">Aggiungere al progetto TodoListService una OWIN Startup Class denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="ab54a-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="ab54a-130">Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** --> **Nuovo elemento** e quindi cercare"OWIN".</span><span class="sxs-lookup"><span data-stu-id="ab54a-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="ab54a-131">Il middleware OWIN richiamerà il metodo `Configuration(…)` all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="ab54a-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="ab54a-132">Sostituire la dichiarazione della classe con `public partial class Startup` .</span><span class="sxs-lookup"><span data-stu-id="ab54a-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="ab54a-133">Nel metodo `Configuration(…)` effettuare una chiamata a ConfgureAuth(...) per configurare l'autenticazione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="ab54a-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="ab54a-134">Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(…)`, che configura l'API Web per accettare token dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab54a-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="ab54a-135">È ora possibile usare gli attributi `[Authorize]` per proteggere i controller e le azioni con l'autenticazione della connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab54a-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="ab54a-136">Decorare la classe `Controllers\TodoListController.cs` con un tag di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ab54a-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="ab54a-137">Ciò forzerà l'utente a eseguire l'accesso prima di accedere alla pagina.</span><span class="sxs-lookup"><span data-stu-id="ab54a-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="ab54a-138">Quando un chiamante autorizzato riesce a chiamare una delle API `TodoListController` , l'azione potrebbe richiedere l'accesso alle informazioni relative al chiamante.</span><span class="sxs-lookup"><span data-stu-id="ab54a-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="ab54a-139">OWIN fornisce l'accesso alle attestazioni all'interno del token di connessione tramite l'oggetto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="ab54a-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="ab54a-140">Infine aprire il file `web.config` nella radice del progetto TodoListService e immettere i valori di configurazione nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="ab54a-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="ab54a-141">`ida:Audience` rappresenta l' **ID applicazione** dell'app immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="ab54a-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="ab54a-142">Configurare l'app client</span><span class="sxs-lookup"><span data-stu-id="ab54a-142">Configure the client app</span></span>
<span data-ttu-id="ab54a-143">Prima di poter vedere in azione il servizio To Do List, è necessario configurare il client To Do List in modo che possa ricevere i token dall'endpoint 2.0 ed eseguire chiamate al servizio.</span><span class="sxs-lookup"><span data-stu-id="ab54a-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="ab54a-144">Nel progetto client To Do List aprire `App.config` e immettere i valori di configurazione nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="ab54a-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="ab54a-145">ID applicazione `ida:ClientId` copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="ab54a-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="ab54a-146">Infine pulire, compilare ed eseguire ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="ab54a-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="ab54a-147">È ora disponibile un'API Web .NET MVC che accetta token da account Microsoft personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="ab54a-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="ab54a-148">Accedere al client To Do List e chiamare l'API Web in modo che aggiunga attività all'elenco di attività da svolgere dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ab54a-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="ab54a-149">Come riferimento, l'esempio completato (senza i valori di configurazione) [è disponibile in un file con estensione .zip qui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip). In alternativa, è possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="ab54a-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="ab54a-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab54a-150">Next steps</span></span>
<span data-ttu-id="ab54a-151">È ora possibile passare ad altri argomenti.</span><span class="sxs-lookup"><span data-stu-id="ab54a-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="ab54a-152">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ab54a-152">You may want to try:</span></span>

[<span data-ttu-id="ab54a-153">Chiamare un'API Web da un'app Web >></span><span class="sxs-lookup"><span data-stu-id="ab54a-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="ab54a-154">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="ab54a-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="ab54a-155">Guida per sviluppatori v2.0 >></span><span class="sxs-lookup"><span data-stu-id="ab54a-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="ab54a-156">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="ab54a-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="ab54a-157">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="ab54a-157">Get security updates for our products</span></span>
<span data-ttu-id="ab54a-158">È consigliabile ricevere notifiche in caso di problemi di sicurezza. A tale scopo, visitare [questa pagina](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ab54a-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
