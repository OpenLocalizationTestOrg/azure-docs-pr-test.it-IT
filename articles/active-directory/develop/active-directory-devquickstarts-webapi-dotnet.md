---
title: aaaAzure AD .NET web API introduzione | Documenti Microsoft
description: Come toobuild un'API web MVC .NET che si integra con Azure AD per l'autenticazione e autorizzazione.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="8cdd7-103">Proteggere un'API Web usando token di connessione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cdd7-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="8cdd7-104">Se si sta creando un'applicazione che fornisce l'accesso alle risorse tooprotected, è necessario tooknow modalità di accesso alle risorse toothose tooprevent non autorizzata.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="8cdd7-105">Azure Active Directory (Azure AD) rende più semplice e diretto toohelp proteggere un'API web tramite i token di accesso di connessione OAuth 2.0 con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="8cdd7-106">Nelle App web ASP.NET, è possibile eseguire questa protezione tramite l'implementazione Microsoft di hello di hello basato sulla community middleware OWIN incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="8cdd7-107">In questo caso si userà OWIN toobuild un'API web "tooDo elenco" che:</span><span class="sxs-lookup"><span data-stu-id="8cdd7-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="8cdd7-108">Designare le API protette.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="8cdd7-109">Convalida che le chiamate API web hello contengano un token di accesso valido.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="8cdd7-110">toobuild hello tooDo API elenco, è innanzitutto necessario:</span><span class="sxs-lookup"><span data-stu-id="8cdd7-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="8cdd7-111">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="8cdd7-112">Impostare la pipeline di autenticazione OWIN hello app toouse hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="8cdd7-113">Configurare un client applicazione toocall hello API web.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="8cdd7-114">tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="8cdd7-115">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="8cdd7-116">È inoltre necessario un tenant di Azure Active Directory in cui tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="8cdd7-117">Se non hai già fatto, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="8cdd7-118">Passaggio 1: Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cdd7-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="8cdd7-119">toohelp proteggere l'applicazione, è innanzitutto necessario toocreate un'applicazione nel tenant di fornire AD Azure con poche alcune informazioni fondamentali.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="8cdd7-120">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8cdd7-121">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-121">On hello top bar, click your account.</span></span> <span data-ttu-id="8cdd7-122">In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="8cdd7-123">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="8cdd7-124">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="8cdd7-125">Seguire le istruzioni di hello e creare un nuovo **applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="8cdd7-126">**Nome** descrive toousers l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="8cdd7-127">Immettere **tooDo servizio elenco**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="8cdd7-128">**Uri di reindirizzamento** è una combinazione di schema e di stringa usato da Azure AD tooreturn qualsiasi token che è richiesta l'app.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="8cdd7-129">Immettere `https://localhost:44321/` per questo valore.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="8cdd7-130">Da hello **impostazioni** -> **proprietà** pagina per l'applicazione, aggiornare hello URI ID App.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="8cdd7-131">Immettere un identificatore specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="8cdd7-132">Ad esempio, immettere `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="8cdd7-133">Salvare la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-133">Save hello configuration.</span></span> <span data-ttu-id="8cdd7-134">Lasciare aperta, portale hello perché è necessario anche tooregister l'applicazione client a breve.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="8cdd7-135">Passaggio 2: Impostare la pipeline di autenticazione OWIN hello app toouse hello</span><span class="sxs-lookup"><span data-stu-id="8cdd7-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="8cdd7-136">le richieste in ingresso toovalidate e i token, è necessario tooset backup toocommunicate l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="8cdd7-137">toobegin, aprire la soluzione hello e aggiungere progetto TodoListService hello OWIN middleware NuGet pacchetti toohello utilizzando la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="8cdd7-138">Aggiungere un progetto TodoListService di avvio di OWIN classi toohello denominato `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="8cdd7-139">Progetto di hello pulsante destro del mouse, selezionare **Aggiungi** > **nuovo elemento**e quindi cercare **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="8cdd7-140">middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="8cdd7-141">Modificare la dichiarazione di classe hello troppo`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="8cdd7-142">Parte di questa classe è stata già implementata in un altro file.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="8cdd7-143">In hello `Configuration(…)` (metodo), effettuare una chiamata troppo`ConfgureAuth(…)` tooset autenticazione per l'app web.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="8cdd7-144">File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(…)` metodo.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="8cdd7-145">Hello parametri forniti nella `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungerà da coordinate per toocommunicate l'app con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="8cdd7-146">È ora possibile usare `[Authorize]` toohelp attributi proteggere i controller e azioni con l'autenticazione della connessione JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="8cdd7-147">Decorare hello `Controllers\TodoListController.cs` classe con un tag authorize.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="8cdd7-148">Questa operazione forzerà toosign utente hello in prima di accedere a tale pagina.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="8cdd7-149">Quando un chiamante autorizzato correttamente richiama uno di hello `TodoListController` API, azione hello potrebbe essere necessario accedere tooinformation sul chiamante hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="8cdd7-150">OWIN fornisce accesso toohello attestazioni in token di connessione hello tramite hello `ClaimsPrincpal` oggetto.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="8cdd7-151">Un requisito comune per l'API web è toovalidate hello "ambiti, presenti nel token hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="8cdd7-152">In questo modo si garantisce che l'utente hello ha accettato le condizioni toohello le autorizzazioni necessarie tooaccess hello tooDo servizio elenco.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="8cdd7-153">Aprire hello `web.config` file nella directory radice del progetto TodoListService hello hello e immettere i valori di configurazione in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="8cdd7-154">`ida:Tenant`è il nome di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="8cdd7-155">`ida:Audience`è hello URI ID App dell'applicazione hello immesso nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="8cdd7-156">Passaggio 3: Configurare un'applicazione client ed eseguire il servizio di hello</span><span class="sxs-lookup"><span data-stu-id="8cdd7-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="8cdd7-157">Prima di poter visualizzare hello tooDo elenco servizio in azione, è necessario tooconfigure hello tooDo elenco client affinché possa ottenere i token da Azure AD e rendere chiamate toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="8cdd7-158">Tornare indietro toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8cdd7-159">Creare una nuova applicazione nel tenant di Azure AD e selezionare **applicazione Client nativa** nel prompt di hello risultante.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="8cdd7-160">**Nome** descrive toousers l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="8cdd7-161">Immettere `http://TodoListClient/` per hello **Uri di reindirizzamento** valore.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="8cdd7-162">Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="8cdd7-163">È necessario che questo valore in passaggi successivi hello, quindi copiarlo dalla pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="8cdd7-164">Da hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="8cdd7-165">Individuare e selezionare hello tooDo servizio elenco, aggiungere hello **accesso TodoListService** autorizzazione in **autorizzazioni delegate**, quindi fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="8cdd7-166">In Visual Studio, aprire `App.config` in hello TodoListClient progetto e quindi immettere i valori di configurazione in hello `<appSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="8cdd7-167">`ida:Tenant`è il nome di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="8cdd7-168">`ida:ClientId`è l'ID app hello copiata dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="8cdd7-169">`todo:TodoListResourceId`è l'URI ID App hello tooDo applicazione di servizio elenco immesso nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cdd7-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8cdd7-170">Next steps</span></span>
<span data-ttu-id="8cdd7-171">Infine pulire, compilare ed eseguire ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="8cdd7-172">Se hai già fatto, è ora hello tempo toocreate un nuovo utente nel tenant con un *. dominio onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="8cdd7-173">Eseguire l'accesso client di elenco tooDo toohello con tale utente e aggiungere l'elenco attività dell'utente toohello alcune attività.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="8cdd7-174">Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8cdd7-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="8cdd7-175">È possibile procedere in scenari con identità toomore.</span><span class="sxs-lookup"><span data-stu-id="8cdd7-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
