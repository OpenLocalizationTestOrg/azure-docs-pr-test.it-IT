---
title: Azure AD B2C | Documentazione Microsoft
description: Come compilare un'API Web .NET con Azure Active Directory B2C protetta con i token di accesso OAuth 2.0 per l'autenticazione.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="767dc-103">Azure Active Directory B2C: compilare un'API Web .NET</span><span class="sxs-lookup"><span data-stu-id="767dc-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="767dc-104">Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="767dc-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="767dc-105">Questi token consentono alle app client di eseguire l'autenticazione all'API.</span><span class="sxs-lookup"><span data-stu-id="767dc-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="767dc-106">Questo articolo illustra come creare un'API "elenco attività" MVC .NET che consente agli utenti dell'applicazione client di eseguire azioni CRUD sulle attività.</span><span class="sxs-lookup"><span data-stu-id="767dc-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="767dc-107">L'API Web è protetta con Azure AD B2C e consente soltanto agli utenti autenticati di gestire il proprio elenco attività.</span><span class="sxs-lookup"><span data-stu-id="767dc-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="767dc-108">Creare una directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="767dc-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="767dc-109">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="767dc-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="767dc-110">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="767dc-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="767dc-111">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="767dc-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="767dc-112">L'applicazione client e l'API Web devono usare la stessa directory di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="767dc-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="767dc-113">Creare un'API Web</span><span class="sxs-lookup"><span data-stu-id="767dc-113">Create a web API</span></span>

<span data-ttu-id="767dc-114">Successivamente, è necessario creare un'app per le API Web nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="767dc-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="767dc-115">In questo modo Azure AD acquisisce le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="767dc-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="767dc-116">Per creare un'app, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="767dc-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="767dc-117">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="767dc-117">Be sure to:</span></span>

* <span data-ttu-id="767dc-118">Includere un'**app Web** o un'**API Web** nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="767dc-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="767dc-119">Usare l'**URI di reindirizzamento** `https://localhost:44332/` per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="767dc-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="767dc-120">Si tratta della posizione predefinita del client dell'app Web per questo codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="767dc-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="767dc-121">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="767dc-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="767dc-122">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="767dc-122">You'll need it later.</span></span>
* <span data-ttu-id="767dc-123">Immettere un identificatore app in **URI ID app**.</span><span class="sxs-lookup"><span data-stu-id="767dc-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="767dc-124">Aggiungere le autorizzazioni tramite il menu **Ambiti pubblicati**.</span><span class="sxs-lookup"><span data-stu-id="767dc-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="767dc-125">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="767dc-125">Create your policies</span></span>

<span data-ttu-id="767dc-126">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="767dc-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="767dc-127">Sarà necessario creare un criterio per comunicare con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="767dc-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="767dc-128">È consigliabile usare i criteri di iscrizione/accesso combinati, come illustrato nell'[articolo di riferimento sui criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="767dc-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="767dc-129">Durante la creazione dei criteri, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="767dc-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="767dc-130">Scegliere **Nome visualizzato** e altri attributi di iscrizione nei criteri.</span><span class="sxs-lookup"><span data-stu-id="767dc-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="767dc-131">Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="767dc-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="767dc-132">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="767dc-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="767dc-133">Copiare il **Nome** di ogni criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="767dc-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="767dc-134">Il nome dei criteri sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="767dc-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="767dc-135">Dopo aver creato i criteri, è possibile passare alla compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="767dc-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="767dc-136">Scaricare il codice</span><span class="sxs-lookup"><span data-stu-id="767dc-136">Download the code</span></span>

<span data-ttu-id="767dc-137">Il codice per questa esercitazione è salvato su [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="767dc-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="767dc-138">È possibile clonare l'esempio eseguendo:</span><span class="sxs-lookup"><span data-stu-id="767dc-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="767dc-139">Dopo aver scaricato il codice di esempio, aprire il file SLN di Visual Studio per iniziare.</span><span class="sxs-lookup"><span data-stu-id="767dc-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="767dc-140">Il file della soluzione contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="767dc-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="767dc-141">`TaskWebApp` è un'applicazione Web MVC con cui l'utente interagisce.</span><span class="sxs-lookup"><span data-stu-id="767dc-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="767dc-142">`TaskService` è l'API Web back-end dell'app in cui viene archiviato l'elenco attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="767dc-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="767dc-143">Questo articolo illustra solo l'applicazione `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="767dc-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="767dc-144">Per informazioni su come compilare `TaskWebApp` usando Azure AD B2C, vedere l'[esercitazione sulle app Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="767dc-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="767dc-145">Aggiornare la configurazione di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="767dc-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="767dc-146">L'esempio è configurato per l'uso dei criteri e dell'ID client del tenant di demo.</span><span class="sxs-lookup"><span data-stu-id="767dc-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="767dc-147">Se si vuole usare il proprio tenant, sarà necessario seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="767dc-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="767dc-148">Aprire `web.config` nel progetto `TaskService` e sostituire i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="767dc-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="767dc-149">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="767dc-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="767dc-150">`ida:ClientId` con l'ID dell'applicazione API Web</span><span class="sxs-lookup"><span data-stu-id="767dc-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="767dc-151">`ida:SignUpSignInPolicyId` con il nome del criterio "di iscrizione o di accesso"</span><span class="sxs-lookup"><span data-stu-id="767dc-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="767dc-152">Aprire `web.config` nel progetto `TaskWebApp` e sostituire i valori di</span><span class="sxs-lookup"><span data-stu-id="767dc-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="767dc-153">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="767dc-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="767dc-154">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="767dc-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="767dc-155">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="767dc-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="767dc-156">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="767dc-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="767dc-157">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="767dc-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="767dc-158">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="767dc-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="767dc-159">Proteggere l'API</span><span class="sxs-lookup"><span data-stu-id="767dc-159">Secure the API</span></span>

<span data-ttu-id="767dc-160">Quando è disponibile un client che chiama l'API, è possibile proteggere l'API, ad esempio `TaskService`, usando i token di connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="767dc-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="767dc-161">In questo modo si assicura che ogni richiesta all'API sarà valida solo se la richiesta include un token di connessione.</span><span class="sxs-lookup"><span data-stu-id="767dc-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="767dc-162">L'API può accettare e convalidare i token di connessione usando la libreria OWIN (Open Web Interface for .NET) di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="767dc-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="767dc-163">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="767dc-163">Install OWIN</span></span>

<span data-ttu-id="767dc-164">Installare prima di tutto la pipeline di autenticazione OAuth OWIN usando la console di Gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="767dc-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="767dc-165">Verrà installato il middleware OWIN che accetterà e convaliderà i token di connessione.</span><span class="sxs-lookup"><span data-stu-id="767dc-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="767dc-166">Aggiungere una classe di avvio OWIN</span><span class="sxs-lookup"><span data-stu-id="767dc-166">Add an OWIN startup class</span></span>

<span data-ttu-id="767dc-167">Aggiungere una classe di avvio OWIN all'API denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="767dc-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="767dc-168">Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** e quindi **Nuovo elemento** e cercare "OWIN".</span><span class="sxs-lookup"><span data-stu-id="767dc-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="767dc-169">Il middleware OWIN richiamerà il metodo `Configuration(…)` all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="767dc-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="767dc-170">In questo esempio la dichiarazione di classe è stata modificata in `public partial class Startup` ed è stata implementata l'altra parte della classe in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="767dc-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="767dc-171">Nel metodo `Configuration` è stata aggiunta una chiamata a `ConfigureAuth`, definita in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="767dc-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="767dc-172">Dopo le modifiche, `Startup.cs` ha un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="767dc-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="767dc-173">Configurare l'autenticazione OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="767dc-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="767dc-174">Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="767dc-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="767dc-175">Ad esempio può avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="767dc-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="767dc-176">Proteggere il controller dell'attività</span><span class="sxs-lookup"><span data-stu-id="767dc-176">Secure the task controller</span></span>

<span data-ttu-id="767dc-177">Dopo aver configurato l'app per usare l'autenticazione OAuth 2.0, per proteggere l'API Web aggiungere un tag `[Authorize]` al controller dell'attività.</span><span class="sxs-lookup"><span data-stu-id="767dc-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="767dc-178">Si tratta del controller in cui avvengono tutte le modifiche relative all'elenco attività. Sarà quindi necessario proteggere l'intero controller a livello della classe.</span><span class="sxs-lookup"><span data-stu-id="767dc-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="767dc-179">È anche possibile aggiungere il tag `[Authorize]` a singole azioni per un controllo più specifico.</span><span class="sxs-lookup"><span data-stu-id="767dc-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="767dc-180">Ottenere le informazioni utente dal token</span><span class="sxs-lookup"><span data-stu-id="767dc-180">Get user information from the token</span></span>

<span data-ttu-id="767dc-181">`TasksController` archivia le attività in un database in cui a ogni attività è associato un utente "proprietario" dell'attività.</span><span class="sxs-lookup"><span data-stu-id="767dc-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="767dc-182">Il proprietario è identificato dall' **ID oggetto**dell'utente.</span><span class="sxs-lookup"><span data-stu-id="767dc-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="767dc-183">Per questo motivo è necessario aggiungere l'ID oggetto come attestazione dell'applicazione in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="767dc-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="767dc-184">Convalidare le autorizzazioni nel token</span><span class="sxs-lookup"><span data-stu-id="767dc-184">Validate the permissions in the token</span></span>

<span data-ttu-id="767dc-185">Un requisito comune per l'API Web è la convalida degli "ambiti" presenti nel token.</span><span class="sxs-lookup"><span data-stu-id="767dc-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="767dc-186">Ciò garantisce che l'utente goda delle autorizzazioni necessarie per accedere a un servizio di tipo "To Do List".</span><span class="sxs-lookup"><span data-stu-id="767dc-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="767dc-187">Eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="767dc-187">Run the sample app</span></span>

<span data-ttu-id="767dc-188">Compilare ed eseguire infine `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="767dc-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="767dc-189">Creare alcune attività nell'elenco attività dell'utente e osservarne la persistenza nell'API anche dopo l'arresto e il riavvio del client.</span><span class="sxs-lookup"><span data-stu-id="767dc-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="767dc-190">Modificare i criteri</span><span class="sxs-lookup"><span data-stu-id="767dc-190">Edit your policies</span></span>

<span data-ttu-id="767dc-191">Dopo aver protetto l'API con Azure AD B2C, è possibile provare i criteri di iscrizione/di accesso dell'app e visualizzarne gli effetti o l'assenza di effetti nell'API.</span><span class="sxs-lookup"><span data-stu-id="767dc-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="767dc-192">È possibile modificare le attestazioni dell'applicazione nei criteri nonché le informazioni utente disponibili nell'API Web.</span><span class="sxs-lookup"><span data-stu-id="767dc-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="767dc-193">Le eventuali attestazioni aggiunte saranno disponibili per l'API Web MVC .NET nell'oggetto `ClaimsPrincipal` , come descritto in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="767dc-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
