---
title: app web .NET di aaaAzure AD introduzione | Documenti Microsoft
description: Compilare un'app Web .NET MVC che si integra con Azure AD per l'accesso.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="df977-103">Accesso e disconnessione all'app Web ASP.NET con Azure AD</span><span class="sxs-lookup"><span data-stu-id="df977-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="df977-104">Fornendo un singolo accesso e disconnessione con poche righe di codice, Azure Active Directory (Azure AD) rende più semplice è toooutsource app web gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="df977-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="df977-105">È possibile firmare gli utenti da e verso le app web ASP.NET tramite l'implementazione Microsoft di hello dell'interfaccia Web aperta per il middleware .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="df977-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="df977-106">Il middleware OWIN gestito dalla community è incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="df977-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="df977-107">Questo articolo viene illustrato come toouse OWIN per:</span><span class="sxs-lookup"><span data-stu-id="df977-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="df977-108">Accesso agli utenti in tooweb App usando Azure AD come provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="df977-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="df977-109">Visualizzare alcune informazioni sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="df977-109">Display some user information.</span></span>
* <span data-ttu-id="df977-110">Accesso agli utenti fuori hello app.</span><span class="sxs-lookup"><span data-stu-id="df977-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="df977-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="df977-111">Before you get started</span></span>
* <span data-ttu-id="df977-112">Scaricare hello [scheletro app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="df977-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="df977-113">È inoltre necessario un tenant di Azure Active Directory nella quale app hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="df977-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="df977-114">Se si dispone già di un tenant di Azure AD, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="df977-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="df977-115">Quando si è pronti, seguire le procedure di hello in hello quattro sezioni.</span><span class="sxs-lookup"><span data-stu-id="df977-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="df977-116">Passaggio 1: Registrare hello nuova app con Azure AD</span><span class="sxs-lookup"><span data-stu-id="df977-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="df977-117">tooset configurazione degli utenti di hello app tooauthenticate, innanzitutto effettuare la registrazione nel tenant di eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="df977-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="df977-118">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df977-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="df977-119">Nella barra superiore hello, scegliere il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="df977-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="df977-120">In hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="df977-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="df977-121">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df977-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="df977-122">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="df977-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="df977-123">Seguire hello richiede toocreate un nuovo **applicazione Web e/o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="df977-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="df977-124">**Nome** descrive toousers app hello.</span><span class="sxs-lookup"><span data-stu-id="df977-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="df977-125">**URL Sign-On** è l'URL di base dell'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="df977-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="df977-126">URL predefinito dell'ossatura Hello è https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="df977-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="df977-127">Dopo aver completato la registrazione di hello, Azure AD le assegna app hello un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="df977-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="df977-128">Copiare il valore di hello hello app pagina toouse nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="df977-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="df977-129">Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App.</span><span class="sxs-lookup"><span data-stu-id="df977-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="df977-130">Hello **URI ID App** è un identificatore univoco per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="df977-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="df977-131">Hello convenzione di denominazione è `https://<tenant-domain>/<app-name>` (ad esempio, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="df977-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="df977-132">Passaggio 2: Impostare la pipeline di autenticazione OWIN hello app toouse hello</span><span class="sxs-lookup"><span data-stu-id="df977-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="df977-133">In questo passaggio verranno configurati hello OWIN middleware toouse hello OpenID Connect protocollo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="df977-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="df977-134">Utilizzare le richieste di accesso e disconnessione tooissue OWIN, gestire le sessioni utente, ottenere le informazioni utente e così via.</span><span class="sxs-lookup"><span data-stu-id="df977-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="df977-135">toobegin, aggiungere il progetto toohello pacchetti NuGet di hello OWIN middleware utilizzando la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="df977-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="df977-136">chiamata di un progetto di avvio di OWIN classe toohello tooadd `Startup.cs`, fare clic sul progetto hello, selezionare **Aggiungi**selezionare **nuovo elemento**e quindi cercare **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="df977-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="df977-137">middleware OWIN Hello richiama hello **Configuration(...)**  metodo hello app all'avvio.</span><span class="sxs-lookup"><span data-stu-id="df977-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="df977-138">Modificare la dichiarazione di classe hello troppo`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="df977-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="df977-139">Parte di questa classe è stata già implementata in un altro file.</span><span class="sxs-lookup"><span data-stu-id="df977-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="df977-140">In hello **Configuration(...)**  (metodo), effettuare una chiamata troppo**ConfgureAuth(...)**  tooset autenticazione per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="df977-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="df977-141">Aprire il file App_Start\Startup.Auth.cs hello e quindi implementare hello **ConfigureAuth(...)**  metodo.</span><span class="sxs-lookup"><span data-stu-id="df977-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="df977-142">parametri che vengono forniti in Hello *OpenIDConnectAuthenticationOptions* fungono da coordinate per hello app toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df977-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="df977-143">È necessario anche tooset di autenticazione dei cookie, perché il middleware di OpenID Connect hello utilizza i cookie in background hello.</span><span class="sxs-lookup"><span data-stu-id="df977-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="df977-144">Aprire hello. config nella directory radice del progetto hello hello e quindi immettere i valori di configurazione hello in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="df977-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="df977-145">`ida:ClientId`: hello GUID copiato dalla hello portale di Azure in "passaggio 1: registrare hello nuova app con Azure AD."</span><span class="sxs-lookup"><span data-stu-id="df977-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="df977-146">`ida:Tenant`: nome hello del tenant di Azure AD (ad esempio, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="df977-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="df977-147">`ida:PostLogoutRedirectUri`: indicatore di hello che indica AD Azure in cui un utente dovrebbe essere reindirizzato dopo una richiesta di disconnessione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="df977-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="df977-148">Passaggio 3: Usare OWIN tooissue accesso e disconnessione richiede tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="df977-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="df977-149">applicazione Hello è ora toocommunicate configurato correttamente con Azure AD con protocollo di autenticazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="df977-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="df977-150">OWIN gestita tutti hello dettagli di creazione di messaggi di autenticazione, convalida dei token da Azure AD e la gestione delle sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="df977-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="df977-151">Che rimane è toogive agli utenti un modo toosign in sia di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="df977-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="df977-152">È possibile utilizzare autorizzare tag toosign di utenti toorequire il controller in prima dell'accesso a determinate pagine.</span><span class="sxs-lookup"><span data-stu-id="df977-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="df977-153">toodo in tal caso, aprire controllers\homecontroller.cs. e quindi aggiungere hello `[Authorize]` tag toohello sul controller.</span><span class="sxs-lookup"><span data-stu-id="df977-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="df977-154">È inoltre possibile utilizzare OWIN toodirectly problema delle richieste di autenticazione all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="df977-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="df977-155">toodo scopo, aprire Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="df977-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="df977-156">In azioni hello SignIn() e SignOut () problema challenge OpenID Connect e richieste di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="df977-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="df977-157">Aprire Views\Shared\_LoginPartial.cshtml tooshow hello utente hello app accesso e disconnessione dei collegamenti e tooprint il nome dell'utente hello in una vista.</span><span class="sxs-lookup"><span data-stu-id="df977-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="df977-158">Passaggio 4: visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="df977-158">Step 4: Display user information</span></span>
<span data-ttu-id="df977-159">Quando autentica gli utenti con OpenID Connect, Azure AD restituisce un'app toohello id_token che contiene "attestazioni", o asserzioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="df977-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="df977-160">È possibile usare queste app di hello toopersonalize basata su attestazioni eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="df977-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="df977-161">Aprire il file controllers\homecontroller.cs. hello.</span><span class="sxs-lookup"><span data-stu-id="df977-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="df977-162">È possibile accedere attestazioni dell'utente hello nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="df977-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="df977-163">Compilare ed eseguire l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="df977-163">Build and run hello app.</span></span> <span data-ttu-id="df977-164">Se è già stato creato un nuovo utente nel tenant con un dominio onmicrosoft.com, è pertanto toodo ora hello.</span><span class="sxs-lookup"><span data-stu-id="df977-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="df977-165">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="df977-165">Here's how:</span></span>

  <span data-ttu-id="df977-166">a.</span><span class="sxs-lookup"><span data-stu-id="df977-166">a.</span></span> <span data-ttu-id="df977-167">Accedere con tale utente e prendere nota come identità dell'utente hello si riflette nella barra superiore hello.</span><span class="sxs-lookup"><span data-stu-id="df977-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="df977-168">b.</span><span class="sxs-lookup"><span data-stu-id="df977-168">b.</span></span> <span data-ttu-id="df977-169">Disconnettersi e accedere nuovamente come un altro utente nel tenant.</span><span class="sxs-lookup"><span data-stu-id="df977-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="df977-170">c.</span><span class="sxs-lookup"><span data-stu-id="df977-170">c.</span></span> <span data-ttu-id="df977-171">Se lo si desidera, per vedere Single Sign-On in azione, registrare ed eseguire un'altra istanza di questa app (con il suo clientId).</span><span class="sxs-lookup"><span data-stu-id="df977-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df977-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df977-172">Next steps</span></span>
<span data-ttu-id="df977-173">Per riferimento, vedere [: esempio hello completato](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (senza i valori di configurazione).</span><span class="sxs-lookup"><span data-stu-id="df977-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="df977-174">È possibile procedere con toomore argomenti avanzati.</span><span class="sxs-lookup"><span data-stu-id="df977-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="df977-175">Provare ad esempio [Proteggere un'API Web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="df977-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
