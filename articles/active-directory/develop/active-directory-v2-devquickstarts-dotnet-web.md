---
title: v 2.0 aaaAzure AD .NET web app Accedi introduzione | Documenti Microsoft
description: Come toobuild un'App Web di MVC .NET che esegue l'accesso agli utenti con entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="74e07-103">Aggiungere app web di accesso tooan MVC .NET</span><span class="sxs-lookup"><span data-stu-id="74e07-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="74e07-104">Con l'endpoint di hello v 2.0, è possibile aggiungere rapidamente applicazioni web per l'autenticazione tooyour con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="74e07-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="74e07-105">Nelle app Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="74e07-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="74e07-106">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="74e07-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="74e07-107">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="74e07-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="74e07-108">Qui creeremo un'app web che usa utente OWIN toosign hello in, visualizzare alcune informazioni sull'utente hello e sign hello utente all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="74e07-109">Scaricare</span><span class="sxs-lookup"><span data-stu-id="74e07-109">Download</span></span>
<span data-ttu-id="74e07-110">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="74e07-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="74e07-111">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="74e07-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="74e07-112">app Hello completato è disponibile alla fine hello anche in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="74e07-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="74e07-113">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="74e07-113">Register an app</span></span>
<span data-ttu-id="74e07-114">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="74e07-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="74e07-115">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="74e07-115">Make sure to:</span></span>

* <span data-ttu-id="74e07-116">Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="74e07-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="74e07-117">Aggiungere hello **Web** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="74e07-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="74e07-118">Immettere hello corretto **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="74e07-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="74e07-119">uri di reindirizzamento Hello indica tooAzure Active Directory in cui devono essere indirizzate le risposte di autenticazione: hello valore predefinito per questa esercitazione è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="74e07-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="74e07-120">Installare e configurare l'autenticazione OWIN</span><span class="sxs-lookup"><span data-stu-id="74e07-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="74e07-121">In questo caso, è possibile configurare hello OWIN middleware toouse hello OpenID Connect protocollo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="74e07-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="74e07-122">OWIN verrà essere tooissue utilizzato le richieste di accesso e disconnessione, gestire la sessione dell'utente hello e ottenere informazioni sull'utente hello, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="74e07-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="74e07-123">toobegin, aprire hello `web.config` file nella directory radice del progetto hello hello e immettere i valori di configurazione dell'applicazione in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="74e07-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="74e07-124">Hello `ida:ClientId` è hello **Id applicazione** assegnato tooyour app nel portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="74e07-125">Hello `ida:RedirectUri` è hello **Uri di reindirizzamento** immesso nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="74e07-126">Successivamente, aggiungere hello OWIN middleware NuGet pacchetti toohello progetto utilizzando la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="74e07-127">Aggiungi un progetto di toohello "Classe di avvio di OWIN" denominato `Startup.cs` destro fare clic sul progetto hello--> **Aggiungi** --> **nuovo elemento** --> ricerca per "OWIN".</span><span class="sxs-lookup"><span data-stu-id="74e07-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="74e07-128">middleware OWIN Hello richiamerà hello `Configuration(...)` metodo all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="74e07-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="74e07-129">Modificare anche la dichiarazione di classe hello`public partial class Startup` -è stato già parte di questa classe è implementato in un altro file.</span><span class="sxs-lookup"><span data-stu-id="74e07-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="74e07-130">In hello `Configuration(...)` (metodo), apportare una tooset tooConfigureAuth(...) chiamata di autenticazione per l'app web</span><span class="sxs-lookup"><span data-stu-id="74e07-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="74e07-131">File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="74e07-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="74e07-132">parametri che vengono forniti in Hello `OpenIdConnectAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74e07-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="74e07-133">È anche necessario tooset Cookie di autenticazione: hello middleware di OpenID Connect utilizza i cookie sotto copre hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="74e07-134">Invio di richieste di autenticazione</span><span class="sxs-lookup"><span data-stu-id="74e07-134">Send authentication requests</span></span>
<span data-ttu-id="74e07-135">L'app è configurato correttamente toocommunicate con endpoint v 2.0 hello utilizzando hello protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="74e07-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="74e07-136">OWIN ha preso in considerazione tutti i dettagli di propriamente hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione sessione utente.</span><span class="sxs-lookup"><span data-stu-id="74e07-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="74e07-137">Che rimane è toogive agli utenti un modo toosign in sia di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="74e07-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="74e07-138">È possibile utilizzare autorizzare tag in toorequire il controller che l'utente accede prima di accedere a una determinata pagina.</span><span class="sxs-lookup"><span data-stu-id="74e07-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="74e07-139">Aprire `Controllers\HomeController.cs`e aggiungere hello `[Authorize]` tag toohello sul controller.</span><span class="sxs-lookup"><span data-stu-id="74e07-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="74e07-140">È inoltre possibile utilizzare OWIN toodirectly problema delle richieste di autenticazione all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="74e07-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="74e07-141">Aprire `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="74e07-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="74e07-142">In hello SignIn() e azioni SignOut (), emettere challenge OpenID Connect e richieste di disconnessione, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="74e07-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="74e07-143">Ora aprire `Views\Shared\_LoginPartial.cshtml`,</span><span class="sxs-lookup"><span data-stu-id="74e07-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="74e07-144">Si tratta in cui verranno Mostra utente hello collegamenti di accesso e disconnessione dell'app e stampare il nome dell'utente hello in una vista.</span><span class="sxs-lookup"><span data-stu-id="74e07-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a><span data-ttu-id="74e07-145">Visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="74e07-145">Display user information</span></span>
<span data-ttu-id="74e07-146">Quando l'autenticazione degli utenti con OpenID Connect, l'endpoint v 2.0 hello restituisce un'app toohello id_token contenente attestazioni o asserzioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="74e07-147">È possibile utilizzare questi toopersonalize attestazioni app:</span><span class="sxs-lookup"><span data-stu-id="74e07-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="74e07-148">Aprire hello `Controllers\HomeController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="74e07-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="74e07-149">È possibile accedere attestazioni dell'utente hello nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="74e07-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="74e07-150">Esegui</span><span class="sxs-lookup"><span data-stu-id="74e07-150">Run</span></span>
<span data-ttu-id="74e07-151">Infine compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="74e07-151">Finally, build and run your app!</span></span>   <span data-ttu-id="74e07-152">Accedere con un Account Microsoft personale o un account aziendale o dell'istituto di istruzione e notare come identità dell'utente hello si riflette nella barra di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="74e07-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="74e07-153">È ora disponibile un'app Web protetta usando protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="74e07-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="74e07-154">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="74e07-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="74e07-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74e07-155">Next steps</span></span>
<span data-ttu-id="74e07-156">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="74e07-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="74e07-157">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="74e07-157">You may want tootry:</span></span>

[<span data-ttu-id="74e07-158">Proteggere un'API Web con endpoint di hello hello v 2.0 >></span><span class="sxs-lookup"><span data-stu-id="74e07-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="74e07-159">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="74e07-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="74e07-160">Guida per sviluppatori v 2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="74e07-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="74e07-161">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="74e07-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="74e07-162">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="74e07-162">Get security updates for our products</span></span>
<span data-ttu-id="74e07-163">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="74e07-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
