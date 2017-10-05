---
title: Introduzione alle app Web .NET per Azure AD | Microsoft Docs
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="58bd6-103">Accesso e disconnessione all'app Web ASP.NET con Azure AD</span><span class="sxs-lookup"><span data-stu-id="58bd6-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="58bd6-104">Con poche righe di codice uniche sia per l'accesso che per la disconnessione, Azure Active Directory (Azure AD) facilita e semplifica l'outsourcing della gestione delle identità delle app Web.</span><span class="sxs-lookup"><span data-stu-id="58bd6-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="58bd6-105">È possibile eseguire l'accesso e la disconnessione degli utenti nelle app Web ASP.NET tramite l'implementazione Microsoft di Open Web Interface per middleware .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="58bd6-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="58bd6-106">Il middleware OWIN gestito dalla community è incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="58bd6-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="58bd6-107">Questo articolo mostra come usare OWIN per:</span><span class="sxs-lookup"><span data-stu-id="58bd6-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="58bd6-108">Far accedere gli utenti alle app Web usando Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="58bd6-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="58bd6-109">Visualizzare alcune informazioni sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="58bd6-109">Display some user information.</span></span>
* <span data-ttu-id="58bd6-110">Far disconnettere gli utenti dalle app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="58bd6-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="58bd6-111">Before you get started</span></span>
* <span data-ttu-id="58bd6-112">Scaricare la [struttura dell'app](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) oppure l'[esempio completato](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="58bd6-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="58bd6-113">È necessario disporre anche di un tenant di Azure AD in cui registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="58bd6-114">Se non si ha già un tenant di Azure AD, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="58bd6-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="58bd6-115">Quando si è pronti, attenersi alle procedure descritte nelle quattro sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="58bd6-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="58bd6-116">Passaggio 1: registrare la nuova app con Azure AD</span><span class="sxs-lookup"><span data-stu-id="58bd6-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="58bd6-117">Per configurare l'app per l'autenticazione degli utenti, registrarla innanzitutto nel tenant eseguendo queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="58bd6-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="58bd6-118">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58bd6-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="58bd6-119">Nella barra superiore fare clic sul nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="58bd6-119">On the top bar, click your account name.</span></span> <span data-ttu-id="58bd6-120">Nell'elenco **Directory** selezionare il tenant di Active Directory in cui si vuole registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="58bd6-121">Fare clic su **More Services** (Altri servizi) nel riquadro a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58bd6-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="58bd6-122">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="58bd6-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="58bd6-123">Seguire le istruzioni e creare un'**applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="58bd6-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="58bd6-124">Il **nome** descrive l'app agli utenti.</span><span class="sxs-lookup"><span data-stu-id="58bd6-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="58bd6-125">L'**URL accesso** è l'URL di base dell'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="58bd6-126">Il valore predefinito della struttura è https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="58bd6-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="58bd6-127">Dopo aver completato la registrazione, Azure AD assegna automaticamente all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="58bd6-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="58bd6-128">Copiare il valore dalla pagina dell'app per usarlo nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="58bd6-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="58bd6-129">Dalla pagina **Impostazioni** -> **Proprietà** dell'applicazione aggiornare l'URI dell'ID app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="58bd6-130">L'**URI ID app** è un identificatore univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="58bd6-131">La convenzione di denominazione è `https://<tenant-domain>/<app-name>`, ad esempio `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="58bd6-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="58bd6-132">Passaggio 2: configurare l'app per l'uso della pipeline di autenticazione OWIN</span><span class="sxs-lookup"><span data-stu-id="58bd6-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="58bd6-133">In questo passaggio, verrà configurato il middleware OWIN per l'uso del protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="58bd6-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="58bd6-134">OWIN verrà usato, tra le altre cose, per inviare le richieste di accesso e disconnessione, gestire la sessione dell'utente e ottenere informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="58bd6-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="58bd6-135">Per iniziare, aggiungere i pacchetti NuGet del middleware OWIN al progetto usando la Console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="58bd6-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="58bd6-136">Per aggiungere al progetto una OWIN Startup Class denominata `Startup.cs`, fare clic con il pulsante destro del mouse sul progetto, selezionare **Aggiungi** --> **Nuovo elemento** e quindi cercare **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="58bd6-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="58bd6-137">OWIN richiama il metodo **Configuration(...)** all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="58bd6-138">Modificare la dichiarazione di classe in `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="58bd6-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="58bd6-139">Parte di questa classe è stata già implementata in un altro file.</span><span class="sxs-lookup"><span data-stu-id="58bd6-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="58bd6-140">Nel metodo **Configuration(...)** effettuare una chiamata a **ConfgureAuth(...)** per configurare l'autenticazione per l'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="58bd6-141">Aprire il file App_Start\Startup.Auth.cs e quindi implementare il metodo **ConfigureAuth(...)**.</span><span class="sxs-lookup"><span data-stu-id="58bd6-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="58bd6-142">I parametri forniti in *OpenIDConnectAuthenticationOptions* fungeranno da coordinate per consentire all'app di comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58bd6-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="58bd6-143">È inoltre necessario impostare l'autenticazione tramite cookie poiché il middleware OpenID Connect usa i cookie in background.</span><span class="sxs-lookup"><span data-stu-id="58bd6-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="58bd6-144">Infine aprire il file web.config nella radice del progetto e immettere i valori di configurazione nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="58bd6-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="58bd6-145">`ida:ClientId`: il GUID copiato dal Portale di Azure in "Passaggio 1: registrare la nuova applicazione con Azure AD."</span><span class="sxs-lookup"><span data-stu-id="58bd6-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="58bd6-146">`ida:Tenant`: il nome del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="58bd6-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="58bd6-147">`ida:PostLogoutRedirectUri`: indica ad Azure AD dove reindirizzare un utente dopo il completamento di una richiesta di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="58bd6-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="58bd6-148">Passaggio 3: usare OWIN per inviare le richieste di accesso e disconnessione ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="58bd6-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="58bd6-149">L'app ora è configurata correttamente per comunicare con Azure AD mediante il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="58bd6-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="58bd6-150">OWIN ha gestito tutti i dettagli relativi alla creazione dei messaggi di autenticazione, alla convalida dei token da Azure AD e alla gestione delle sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="58bd6-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="58bd6-151">Non resta che dare agli utenti un modo per accedere e disconnettersi.</span><span class="sxs-lookup"><span data-stu-id="58bd6-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="58bd6-152">È possibile usare tag di autorizzazione nei controller per obbligare l'utente ad accedere prima di aprire determinate pagine.</span><span class="sxs-lookup"><span data-stu-id="58bd6-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="58bd6-153">A tale scopo, aprire Controllers\HomeController.cs e quindi aggiungere il tag `[Authorize]` al controller About.</span><span class="sxs-lookup"><span data-stu-id="58bd6-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="58bd6-154">È possibile usare OWIN anche per inviare le richieste di autenticazione direttamente dal codice.</span><span class="sxs-lookup"><span data-stu-id="58bd6-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="58bd6-155">A questo fine, aprire Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="58bd6-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="58bd6-156">Poi, nelle azioni SignIn() e SignOut() inoltrare le richieste di verifica e di disconnessione di OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="58bd6-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="58bd6-157">Aprire Views\Shared\_LoginPartial.cshtml per indicare all'utente i collegamenti di accesso e disconnessione dall'app e per stampare il nome dell'utente in una vista.</span><span class="sxs-lookup"><span data-stu-id="58bd6-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="58bd6-158">Passaggio 4: visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="58bd6-158">Step 4: Display user information</span></span>
<span data-ttu-id="58bd6-159">Quando si autenticano gli utenti con OpenID Connect, Azure AD restituisce un id_token all'app contenente attestazioni, ovvero asserzioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="58bd6-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="58bd6-160">È possibile usare tali attestazioni per personalizzare l'app eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="58bd6-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="58bd6-161">Aprire il file Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="58bd6-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="58bd6-162">È possibile accedere alle attestazioni dell'utente nei controller tramite l'oggetto di entità di sicurezza `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="58bd6-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="58bd6-163">Compilare ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="58bd6-163">Build and run the app.</span></span> <span data-ttu-id="58bd6-164">Se non si è ancora creato un nuovo utente nel tenant con un dominio .onmicrosoft.com, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="58bd6-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="58bd6-165">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="58bd6-165">Here's how:</span></span>

  <span data-ttu-id="58bd6-166">a.</span><span class="sxs-lookup"><span data-stu-id="58bd6-166">a.</span></span> <span data-ttu-id="58bd6-167">Accedere con tale utente e notare che l'identità dell'utente è visualizzata nella barra di superiore.</span><span class="sxs-lookup"><span data-stu-id="58bd6-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="58bd6-168">b.</span><span class="sxs-lookup"><span data-stu-id="58bd6-168">b.</span></span> <span data-ttu-id="58bd6-169">Disconnettersi e accedere nuovamente come un altro utente nel tenant.</span><span class="sxs-lookup"><span data-stu-id="58bd6-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="58bd6-170">c.</span><span class="sxs-lookup"><span data-stu-id="58bd6-170">c.</span></span> <span data-ttu-id="58bd6-171">Se lo si desidera, per vedere Single Sign-On in azione, registrare ed eseguire un'altra istanza di questa app (con il suo clientId).</span><span class="sxs-lookup"><span data-stu-id="58bd6-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58bd6-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58bd6-172">Next steps</span></span>
<span data-ttu-id="58bd6-173">Per riferimento, consultare l'[esempio completato](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip), che non contiene i valori di configurazione immessi durante la procedura sopra indicata.</span><span class="sxs-lookup"><span data-stu-id="58bd6-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="58bd6-174">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="58bd6-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="58bd6-175">Provare ad esempio [Proteggere un'API Web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="58bd6-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
