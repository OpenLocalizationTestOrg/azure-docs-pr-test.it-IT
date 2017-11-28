---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'API Web .NET utilizzando Active B2C Directory di Azure, protette con token di accesso OAuth 2.0 per l'autenticazione.
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
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="58061-103">Azure Active Directory B2C: compilare un'API Web .NET</span><span class="sxs-lookup"><span data-stu-id="58061-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="58061-104">Azure Active Directory (Azure AD) B2C permette di proteggere un'API Web usando i token di accesso OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="58061-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="58061-105">Questi token consentono al client App tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="58061-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="58061-106">Questo articolo illustra come toocreate un'API di .NET MVC "elenco" che consente agli utenti del client attività tooCRUD dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58061-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="58061-107">API web Hello sia protetta con Azure Active Directory B2C e consente solo agli utenti autenticati toomanage proprio elenco di attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="58061-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="58061-108">Creare una directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="58061-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="58061-109">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="58061-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="58061-110">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="58061-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="58061-111">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="58061-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="58061-112">un'applicazione client Hello e API web devono utilizzare directory B2C hello stesso Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58061-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="58061-113">Creare un'API Web</span><span class="sxs-lookup"><span data-stu-id="58061-113">Create a web API</span></span>

<span data-ttu-id="58061-114">Successivamente, è necessario toocreate un'app di API web nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="58061-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="58061-115">In questo modo le informazioni di Azure AD che è necessario toosecurely a comunicare con l'app.</span><span class="sxs-lookup"><span data-stu-id="58061-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="58061-116">toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="58061-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="58061-117">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="58061-117">Be sure to:</span></span>

* <span data-ttu-id="58061-118">Includere un **app web** o **web API** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="58061-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="58061-119">Hello utilizzare **URI di reindirizzamento** `https://localhost:44332/` per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="58061-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="58061-120">Questo è il percorso predefinito hello del client di app web hello per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="58061-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="58061-121">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="58061-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="58061-122">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="58061-122">You'll need it later.</span></span>
* <span data-ttu-id="58061-123">Immettere un identificatore app in **URI ID app**.</span><span class="sxs-lookup"><span data-stu-id="58061-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="58061-124">Aggiungere le autorizzazioni tramite hello **pubblicati ambiti** menu.</span><span class="sxs-lookup"><span data-stu-id="58061-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="58061-125">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="58061-125">Create your policies</span></span>

<span data-ttu-id="58061-126">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="58061-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="58061-127">Sarà necessario toocreate toocommunicate un criterio con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="58061-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="58061-128">È consigliabile utilizzare hello combinazione sign-configurazione/sign-in criteri, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="58061-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="58061-129">Durante la creazione dei criteri, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="58061-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="58061-130">Scegliere **Nome visualizzato** e altri attributi di iscrizione nei criteri.</span><span class="sxs-lookup"><span data-stu-id="58061-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="58061-131">Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="58061-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="58061-132">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="58061-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="58061-133">Hello copia **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="58061-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="58061-134">È necessario il nome di criterio hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="58061-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="58061-135">Dopo avere creato i criteri di hello, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="58061-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="58061-136">Scaricare codice hello</span><span class="sxs-lookup"><span data-stu-id="58061-136">Download hello code</span></span>

<span data-ttu-id="58061-137">codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="58061-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="58061-138">È possibile clonare: esempio hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="58061-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="58061-139">Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58061-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="58061-140">file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="58061-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="58061-141">`TaskWebApp`è un'applicazione web MVC hello utente interagisce con.</span><span class="sxs-lookup"><span data-stu-id="58061-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="58061-142">`TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="58061-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="58061-143">Questo articolo viene illustrato solo hello `TaskService` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58061-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="58061-144">toolearn come toobuild `TaskWebApp` tramite Azure Active Directory B2C, vedere [l'esercitazione di app web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="58061-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="58061-145">Aggiornare la configurazione di hello Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="58061-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="58061-146">L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="58061-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="58061-147">Se si desidera toouse il proprio tenant, sarà necessario hello toodo seguenti:</span><span class="sxs-lookup"><span data-stu-id="58061-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="58061-148">Aprire `web.config` in hello `TaskService` progetti e sostituire i valori hello per</span><span class="sxs-lookup"><span data-stu-id="58061-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="58061-149">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="58061-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="58061-150">`ida:ClientId` con l'ID dell'applicazione API Web</span><span class="sxs-lookup"><span data-stu-id="58061-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="58061-151">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="58061-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="58061-152">Aprire `web.config` in hello `TaskWebApp` progetti e sostituire i valori hello per</span><span class="sxs-lookup"><span data-stu-id="58061-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="58061-153">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="58061-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="58061-154">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="58061-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="58061-155">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="58061-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="58061-156">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="58061-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="58061-157">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="58061-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="58061-158">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="58061-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="58061-159">Proteggi hello API</span><span class="sxs-lookup"><span data-stu-id="58061-159">Secure hello API</span></span>

<span data-ttu-id="58061-160">Quando è disponibile un client che chiama l'API, è possibile proteggere l'API, ad esempio `TaskService`, usando i token di connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="58061-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="58061-161">In questo modo si garantisce che ogni API tooyour richiesta sarà valido solo se la richiesta hello dispone di un token di connessione.</span><span class="sxs-lookup"><span data-stu-id="58061-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="58061-162">L'API può accettare e convalidare i token di connessione usando la libreria OWIN (Open Web Interface for .NET) di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58061-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="58061-163">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="58061-163">Install OWIN</span></span>

<span data-ttu-id="58061-164">Iniziare con l'installazione della pipeline di autenticazione OAuth OWIN hello utilizzando hello Console di gestione di pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58061-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="58061-165">Middleware OWIN hello che verrà accettati e convalidati i token di connessione verrà installato.</span><span class="sxs-lookup"><span data-stu-id="58061-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="58061-166">Aggiungere una classe di avvio OWIN</span><span class="sxs-lookup"><span data-stu-id="58061-166">Add an OWIN startup class</span></span>

<span data-ttu-id="58061-167">Aggiunge un toohello di classe di avvio OWIN API denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="58061-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="58061-168">Fare clic su progetto hello, selezionare **Aggiungi** e **nuovo elemento**e quindi cercare OWIN.</span><span class="sxs-lookup"><span data-stu-id="58061-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="58061-169">middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="58061-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="58061-170">In questo esempio, è stato modificato la dichiarazione di classe hello anche`public partial class Startup` e implementato hello altra parte della classe hello in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="58061-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="58061-171">Inside hello `Configuration` (metodo), è stata aggiunta una chiamata troppo`ConfigureAuth`, definito in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="58061-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="58061-172">Dopo le modifiche di hello, `Startup.cs` sarà simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="58061-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="58061-173">Configurare l'autenticazione OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="58061-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="58061-174">File aperti hello `App_Start\Startup.Auth.cs`e implementare hello `ConfigureAuth(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="58061-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="58061-175">Ad esempio, potrebbe avere questo aspetto hello seguente:</span><span class="sxs-lookup"><span data-stu-id="58061-175">For example, it could look like hello following:</span></span>

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
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="58061-176">Proteggere i controller di attività hello</span><span class="sxs-lookup"><span data-stu-id="58061-176">Secure hello task controller</span></span>

<span data-ttu-id="58061-177">Dopo l'applicazione hello è autenticazione configurata toouse OAuth 2.0, è possibile proteggere l'API web mediante l'aggiunta di un `[Authorize]` controller attività toohello di tag.</span><span class="sxs-lookup"><span data-stu-id="58061-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="58061-178">Questo è il controller hello in cui tutte le relative modifiche elenco attività viene eseguita, pertanto è consigliabile proteggere i controller di intero hello a livello di classe hello.</span><span class="sxs-lookup"><span data-stu-id="58061-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="58061-179">È inoltre possibile aggiungere hello `[Authorize]` tag azioni tooindividual per un controllo più accurato.</span><span class="sxs-lookup"><span data-stu-id="58061-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="58061-180">Ottenere le informazioni utente da hello token</span><span class="sxs-lookup"><span data-stu-id="58061-180">Get user information from hello token</span></span>

<span data-ttu-id="58061-181">`TasksController`Archivia le attività in un database in cui ogni attività dispone di un utente associato "proprietario" attività hello.</span><span class="sxs-lookup"><span data-stu-id="58061-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="58061-182">proprietario Hello è identificato da dell'utente hello **ID di oggetto**.</span><span class="sxs-lookup"><span data-stu-id="58061-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="58061-183">(Questo è il motivo è necessario l'ID di oggetto hello tooadd come un'applicazione in tutti i criteri di attestazione.)</span><span class="sxs-lookup"><span data-stu-id="58061-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="58061-184">Convalidare le autorizzazioni di hello nel token hello</span><span class="sxs-lookup"><span data-stu-id="58061-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="58061-185">Un requisito comune per l'API web è toovalidate hello "ambiti, presenti nel token hello.</span><span class="sxs-lookup"><span data-stu-id="58061-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="58061-186">In questo modo si garantisce che l'utente hello ha accettato le condizioni del servizio di elenco attività toohello autorizzazioni tooaccess obbligatorio hello.</span><span class="sxs-lookup"><span data-stu-id="58061-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="58061-187">Eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="58061-187">Run hello sample app</span></span>

<span data-ttu-id="58061-188">Compilare ed eseguire infine `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="58061-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="58061-189">Creare alcune attività nell'elenco attività dell'utente hello e notare come vengono rese persistenti nell'API hello anche dopo l'arresto e riavvio di client hello.</span><span class="sxs-lookup"><span data-stu-id="58061-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="58061-190">Modificare i criteri</span><span class="sxs-lookup"><span data-stu-id="58061-190">Edit your policies</span></span>

<span data-ttu-id="58061-191">Dopo essersi assicurati un'API con Azure Active Directory B2C, è possibile utilizzare i criteri Sign-in/iscrizione e visualizzare gli effetti di hello (o assenza) su hello API.</span><span class="sxs-lookup"><span data-stu-id="58061-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="58061-192">È possibile modificare le attestazioni applicazione hello nei criteri hello e modificare le informazioni utente hello disponibile nell'API web hello.</span><span class="sxs-lookup"><span data-stu-id="58061-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="58061-193">Tutte le attestazioni che aggiungono sarà API web MVC .NET di tooyour disponibile in hello `ClaimsPrincipal` oggetto, come descritto in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="58061-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
