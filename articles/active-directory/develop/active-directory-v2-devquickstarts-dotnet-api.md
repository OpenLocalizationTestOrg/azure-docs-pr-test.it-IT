---
title: aaaAdd tooa accesso API web MVC .NET utilizzando hello endpoint v 2.0 di Azure AD | Documenti Microsoft
description: Come toobuild un'Api Web MVC di .NET che accetta i token da entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
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
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="96819-103">Proteggere un'API Web MVC</span><span class="sxs-lookup"><span data-stu-id="96819-103">Secure an MVC web API</span></span>
<span data-ttu-id="96819-104">Con l'endpoint di Azure Active Directory hello v 2.0, è possibile proteggere un utilizzo di API Web [OAuth 2.0](active-directory-v2-protocols.md) i token di accesso, l'attivazione di utenti con entrambi account Microsoft personale e gli account aziendali o dell'istituto di istruzione toosecurely accedere l'API Web.</span><span class="sxs-lookup"><span data-stu-id="96819-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="96819-105">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="96819-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="96819-106">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="96819-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="96819-107">Nelle API Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="96819-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="96819-108">In questo caso si userà OWIN toobuild un'API Web MVC di "tooDo elenco" che consente ai client toocreate e leggere le attività dall'elenco di attività dell'utente.</span><span class="sxs-lookup"><span data-stu-id="96819-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="96819-109">API web Hello convalida che le richieste in ingresso contengono un token di accesso valido e rifiutare le richieste che non passano la convalida su una route protetta.</span><span class="sxs-lookup"><span data-stu-id="96819-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="96819-110">Questo esempio è stato creato con Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="96819-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="96819-111">Scaricare</span><span class="sxs-lookup"><span data-stu-id="96819-111">Download</span></span>
<span data-ttu-id="96819-112">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="96819-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="96819-113">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="96819-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="96819-114">app scheletro Hello include tutto il codice boilerplate hello per una semplice API, ma mancano le parti relative alle identità hello.</span><span class="sxs-lookup"><span data-stu-id="96819-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="96819-115">Se non si desidera toofollow lungo, è possibile clonare o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="96819-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="96819-116">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="96819-116">Register an app</span></span>
<span data-ttu-id="96819-117">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="96819-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="96819-118">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="96819-118">Make sure to:</span></span>

* <span data-ttu-id="96819-119">Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="96819-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="96819-120">Questa soluzione di visual studio contiene anche una "TodoListClient", che è una semplice applicazione WPF.</span><span class="sxs-lookup"><span data-stu-id="96819-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="96819-121">Hello TodoListClient è toodemonstrate utilizzato come un accesso dell'utente e la modalità con cui un client può inviare richieste tooyour API Web.</span><span class="sxs-lookup"><span data-stu-id="96819-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="96819-122">In questo caso, sia hello TodoListClient hello TodoListService sono rappresentati da e hello stessa app.</span><span class="sxs-lookup"><span data-stu-id="96819-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="96819-123">tooconfigure hello TodoListClient, è inoltre necessario:</span><span class="sxs-lookup"><span data-stu-id="96819-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="96819-124">Aggiungere hello **Mobile** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="96819-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="96819-125">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="96819-125">Install OWIN</span></span>
<span data-ttu-id="96819-126">Una volta registrato un'app, è necessario tooset backup toocommunicate l'app con endpoint v 2.0 hello in richieste in ingresso di ordine toovalidate & token.</span><span class="sxs-lookup"><span data-stu-id="96819-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="96819-127">toobegin, aprire la soluzione hello e aggiungere hello OWIN middleware NuGet pacchetti toohello progetto TodoListService utilizzando Console Gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="96819-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="96819-128">Configurare l'autenticazione OAuth</span><span class="sxs-lookup"><span data-stu-id="96819-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="96819-129">Aggiungere un progetto TodoListService di avvio di OWIN classi toohello denominato `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="96819-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="96819-130">--> Destro fare clic sul progetto hello **Aggiungi** --> **nuovo elemento** --> ricerca per "OWIN".</span><span class="sxs-lookup"><span data-stu-id="96819-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="96819-131">middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="96819-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="96819-132">Modificare anche la dichiarazione di classe hello`public partial class Startup` -è stato già parte di questa classe è implementato in un altro file.</span><span class="sxs-lookup"><span data-stu-id="96819-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="96819-133">In hello `Configuration(…)` (metodo), apportare una tooset tooConfgureAuth(...) chiamata di autenticazione per l'app web.</span><span class="sxs-lookup"><span data-stu-id="96819-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="96819-134">File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(…)` metodo, che verrà configurati i token di tooaccept hello Web API dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="96819-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="96819-135">È ora possibile usare `[Authorize]` attributi tooprotect i controller e azioni con l'autenticazione della connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="96819-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="96819-136">Decorare hello `Controllers\TodoListController.cs` classe con un tag authorize.</span><span class="sxs-lookup"><span data-stu-id="96819-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="96819-137">Questa operazione forzerà toosign utente hello in prima di accedere a tale pagina.</span><span class="sxs-lookup"><span data-stu-id="96819-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="96819-138">Quando un chiamante autorizzato correttamente richiama uno di hello `TodoListController` API, azione hello potrebbe essere necessario accedere tooinformation sul chiamante hello.</span><span class="sxs-lookup"><span data-stu-id="96819-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="96819-139">OWIN fornisce accesso toohello attestazioni in token di connessione hello tramite hello `ClaimsPrincpal` oggetto.</span><span class="sxs-lookup"><span data-stu-id="96819-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="96819-140">Infine, aprire hello `web.config` file nella directory radice del progetto TodoListService hello hello e immettere i valori di configurazione in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="96819-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="96819-141">Il `ida:Audience` è hello **Id applicazione** dell'app hello immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="96819-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="96819-142">Configurare l'applicazione client hello</span><span class="sxs-lookup"><span data-stu-id="96819-142">Configure hello client app</span></span>
<span data-ttu-id="96819-143">Prima di poter visualizzare hello servizio elenco attività nell'azione, è necessario tooconfigure hello Client elenco attività, affinché possa ottenere token dall'endpoint v 2.0 hello e rendere chiamate toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="96819-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="96819-144">Nel progetto TodoListClient hello aprire `App.config` e immettere i valori di configurazione in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="96819-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="96819-145">Il `ida:ClientId` Id applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="96819-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="96819-146">Infine pulire, compilare ed eseguire ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="96819-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="96819-147">È ora disponibile un'API Web .NET MVC che accetta token da account Microsoft personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="96819-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="96819-148">Accedere al hello TodoListClient e chiamare l'elenco di attività web api tooadd attività toohello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="96819-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="96819-149">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="96819-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="96819-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96819-150">Next steps</span></span>
<span data-ttu-id="96819-151">È ora possibile passare ad altri argomenti.</span><span class="sxs-lookup"><span data-stu-id="96819-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="96819-152">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="96819-152">You may want tootry:</span></span>

[<span data-ttu-id="96819-153">Chiamare un'API Web da un'app Web &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="96819-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="96819-154">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="96819-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="96819-155">Guida per sviluppatori v 2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="96819-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="96819-156">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="96819-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="96819-157">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="96819-157">Get security updates for our products</span></span>
<span data-ttu-id="96819-158">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="96819-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
