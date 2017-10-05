---
title: Introduzione all'accesso alle App Web Azure AD v2.0 .NET | Documentazione Microsoft
description: Come creare un'app Web .NET MVC che consente agli utenti di accedere sia con un account Microsoft personale sia con quello aziendale o dell'istituto di istruzione.
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="55872-103">Aggiungere l'accesso a un'app Web .NET MVC</span><span class="sxs-lookup"><span data-stu-id="55872-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="55872-104">Con l'endpoint v2.0 è possibile aggiungere rapidamente l'autenticazione alle app Web con supporto per account Microsoft personali, aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="55872-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="55872-105">Nelle app Web ASP.NET, a questo scopo si usa il middleware OWIN di Microsoft incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="55872-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="55872-106">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="55872-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="55872-107">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="55872-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="55872-108">Verrà compilata un'applicazione Web che utilizza OWIN per l'accesso dell'utente, la visualizzazione di informazioni sull'utente e la disconnessione dell'utente dall'app.</span><span class="sxs-lookup"><span data-stu-id="55872-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="55872-109">Scaricare</span><span class="sxs-lookup"><span data-stu-id="55872-109">Download</span></span>
<span data-ttu-id="55872-110">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="55872-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="55872-111">Per seguire la procedura è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="55872-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="55872-112">Al termine dell'esercitazione, verrà fornita anche l'app completata.</span><span class="sxs-lookup"><span data-stu-id="55872-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="55872-113">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="55872-113">Register an app</span></span>
<span data-ttu-id="55872-114">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="55872-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="55872-115">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="55872-115">Make sure to:</span></span>

* <span data-ttu-id="55872-116">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="55872-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="55872-117">Aggiungere la piattaforma **Web** per l'app.</span><span class="sxs-lookup"><span data-stu-id="55872-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="55872-118">Immettere l' **URI di reindirizzamento**corretto.</span><span class="sxs-lookup"><span data-stu-id="55872-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="55872-119">L'URI di reindirizzamento indica ad Azure AD dove indirizzare le risposte di autenticazione. Il valore predefinito per questa esercitazione è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="55872-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="55872-120">Installare e configurare l'autenticazione OWIN</span><span class="sxs-lookup"><span data-stu-id="55872-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="55872-121">In questo caso, verrà configurato il middleware OWIN per l'uso del protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="55872-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="55872-122">OWIN verrà usato, tra le altre cose, per inviare le richieste di accesso e disconnessione, gestire la sessione dell'utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="55872-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="55872-123">Per iniziare, aprire il file `web.config` nella radice del progetto e immettere i valori di configurazione dell'app nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="55872-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="55872-124">`ida:ClientId` rappresenta l' **ID applicazione** assegnato all'app nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="55872-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="55872-125">`ida:RedirectUri` rappresenta l' **URI di reindirizzamento** immesso nel portale.</span><span class="sxs-lookup"><span data-stu-id="55872-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="55872-126">Successivamente, aggiungere il middleware NuGet al progetto usando la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="55872-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="55872-127">Aggiungere al progetto una classe OWIN Startup denominata `Startup.cs`. Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** --> **Nuovo elemento** e quindi cercare "OWIN".</span><span class="sxs-lookup"><span data-stu-id="55872-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="55872-128">Il middleware OWIN richiamerà il metodo `Configuration(...)` all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="55872-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="55872-129">Sostituire la dichiarazione della classe con `public partial class Startup`. Parte di questa classe è già stata implementata in un altro file.</span><span class="sxs-lookup"><span data-stu-id="55872-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="55872-130">Nel metodo `Configuration(...)` eseguire una chiamata a ConfigureAuth(...) per configurare l'autenticazione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="55872-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="55872-131">Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="55872-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="55872-132">I parametri forniti in `OpenIdConnectAuthenticationOptions` fungeranno da coordinate per consentire all'app di comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55872-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="55872-133">È inoltre necessario impostare l'autenticazione tramite cookie: il middleware OpenID Connect usa i cookie in background.</span><span class="sxs-lookup"><span data-stu-id="55872-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="55872-134">Invio di richieste di autenticazione</span><span class="sxs-lookup"><span data-stu-id="55872-134">Send authentication requests</span></span>
<span data-ttu-id="55872-135">L'app ora è configurata correttamente per comunicare con l'endpoint 2.0 mediante il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="55872-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="55872-136">OWIN ha gestito tutte le difficoltà derivanti dalla creazione dei messaggi di autenticazione, dalla convalida dei token da Azure AD e dalla gestione della sessione utente.</span><span class="sxs-lookup"><span data-stu-id="55872-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="55872-137">Non resta che dare agli utenti un modo per accedere e disconnettersi.</span><span class="sxs-lookup"><span data-stu-id="55872-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="55872-138">È possibile usare tag di autorizzazione nei controller per obbligare l'utente ad accedere prima di aprire una determinata pagina.</span><span class="sxs-lookup"><span data-stu-id="55872-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="55872-139">Aprire `Controllers\HomeController.cs` e aggiungere il tag `[Authorize]` al controller About.</span><span class="sxs-lookup"><span data-stu-id="55872-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="55872-140">È possibile usare OWIN anche per inviare le richieste di autenticazione direttamente dal codice.</span><span class="sxs-lookup"><span data-stu-id="55872-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="55872-141">Aprire `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="55872-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="55872-142">Nelle azioni SignIn() e SignOut() inoltrare rispettivamente le richieste di verifica e di disconnessione di OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="55872-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="55872-143">Ora aprire `Views\Shared\_LoginPartial.cshtml`,</span><span class="sxs-lookup"><span data-stu-id="55872-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="55872-144">dove si mostreranno all'utente i collegamenti di accesso e disconnessione e si visualizzerà il nome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="55872-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="55872-145">Visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="55872-145">Display user information</span></span>
<span data-ttu-id="55872-146">Quando si autenticano gli utenti con OpenID Connect, l'endpoint v2.0 restituisce un token ID all'app che contiene attestazioni o asserzioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="55872-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="55872-147">È possibile usare queste attestazioni per personalizzare l'app:</span><span class="sxs-lookup"><span data-stu-id="55872-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="55872-148">Aprire il file `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="55872-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="55872-149">È possibile accedere alle attestazioni dell'utente nei controller tramite l'oggetto di entità di sicurezza `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="55872-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="55872-150">Esegui</span><span class="sxs-lookup"><span data-stu-id="55872-150">Run</span></span>
<span data-ttu-id="55872-151">Infine compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="55872-151">Finally, build and run your app!</span></span>   <span data-ttu-id="55872-152">Accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione e osservare come l'identità dell'utente è indicata nella barra di spostamento superiore.</span><span class="sxs-lookup"><span data-stu-id="55872-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="55872-153">È ora disponibile un'app Web protetta usando protocolli standard del settore in grado di autenticare gli utenti con account personali, aziendali e dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="55872-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="55872-154">Come riferimento, l'esempio completato (senza i valori di configurazione) [è disponibile in un file con estensione .zip qui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip). In alternativa, è possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="55872-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="55872-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55872-155">Next steps</span></span>
<span data-ttu-id="55872-156">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="55872-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="55872-157">È possibile:</span><span class="sxs-lookup"><span data-stu-id="55872-157">You may want to try:</span></span>

[<span data-ttu-id="55872-158">Proteggere un'API Web con l'endpoint 2.0 >></span><span class="sxs-lookup"><span data-stu-id="55872-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="55872-159">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="55872-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="55872-160">Guida per sviluppatori v2.0 >></span><span class="sxs-lookup"><span data-stu-id="55872-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="55872-161">StackOverflow: tag "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="55872-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="55872-162">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="55872-162">Get security updates for our products</span></span>
<span data-ttu-id="55872-163">È consigliabile ricevere notifiche in caso di problemi di sicurezza. A tale scopo, visitare [questa pagina](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="55872-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
