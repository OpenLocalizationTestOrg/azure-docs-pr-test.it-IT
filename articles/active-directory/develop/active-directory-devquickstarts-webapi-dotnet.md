---
title: Introduzione alle API Web .NET per Azure AD | Microsoft Docs
description: Come compilare un'API Web MVC per Node.js che si integra con Azure AD per l'autenticazione e l'autorizzazione.
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="d882e-103">Proteggere un'API Web usando token di connessione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d882e-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d882e-104">Se si compila un'applicazione che fornisce l'accesso alle risorse protette, è necessario sapere come prevenire l'accesso non protetto a tali risorse.</span><span class="sxs-lookup"><span data-stu-id="d882e-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="d882e-105">Azure Active Directory (Azure AD) rende semplici e dirette le operazioni per la protezione di un'API Web usando i token di connessione dell'accesso di OAuth 2.0 con solo poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="d882e-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="d882e-106">Nelle app Web Asp.NET, a questo scopo si usa l'implementazione di Microsoft del middleware OWIN gestito dalla community e incluso in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d882e-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="d882e-107">Qui OWIN verrà usato per creare un'API Web "Elenco attività" in grado di:</span><span class="sxs-lookup"><span data-stu-id="d882e-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="d882e-108">Designare le API protette.</span><span class="sxs-lookup"><span data-stu-id="d882e-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="d882e-109">Verificare che le chiamate all'API Web contengano un token di accesso valido.</span><span class="sxs-lookup"><span data-stu-id="d882e-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="d882e-110">Per compilare l'API "To Do List", è innanzitutto necessario:</span><span class="sxs-lookup"><span data-stu-id="d882e-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="d882e-111">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d882e-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="d882e-112">Configurare l'app per l'uso della pipeline di autenticazione OWIN.</span><span class="sxs-lookup"><span data-stu-id="d882e-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="d882e-113">Configurare un'applicazione client per chiamare l'API Web.</span><span class="sxs-lookup"><span data-stu-id="d882e-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="d882e-114">Per iniziare, [scaricare la struttura dell'app](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d882e-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d882e-115">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d882e-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="d882e-116">È necessario anche un tenant di Azure AD in cui registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d882e-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="d882e-117">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d882e-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="d882e-118">Passaggio 1: Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="d882e-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="d882e-119">Per proteggere l'applicazione, si dovrà per prima cosa creare un'applicazione nel proprio tenant e fornire ad Azure AD alcune informazioni fondamentali.</span><span class="sxs-lookup"><span data-stu-id="d882e-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="d882e-120">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d882e-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d882e-121">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="d882e-121">On the top bar, click your account.</span></span> <span data-ttu-id="d882e-122">Nell'elenco di **Directory** scegliere il tenant di Azure AD in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d882e-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="d882e-123">Fare clic su **More Services** (Altri servizi) nel riquadro sinistro, quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d882e-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="d882e-124">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d882e-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="d882e-125">Seguire le istruzioni e creare una nuova **applicazione Web e/o API Web**.</span><span class="sxs-lookup"><span data-stu-id="d882e-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="d882e-126">**Nome** descrive l'applicazione agli utenti.</span><span class="sxs-lookup"><span data-stu-id="d882e-126">**Name** describes your application to users.</span></span> <span data-ttu-id="d882e-127">Immettere **To Do List Service**.</span><span class="sxs-lookup"><span data-stu-id="d882e-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="d882e-128">**URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD userà per restituire i token richiesti dall'app.</span><span class="sxs-lookup"><span data-stu-id="d882e-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="d882e-129">Immettere `https://localhost:44321/` per questo valore.</span><span class="sxs-lookup"><span data-stu-id="d882e-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="d882e-130">Dalla pagina **Impostazioni** -> **Proprietà** dell'applicazione aggiornare l'URI dell'ID app.</span><span class="sxs-lookup"><span data-stu-id="d882e-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="d882e-131">Immettere un identificatore specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="d882e-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="d882e-132">Ad esempio, immettere `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="d882e-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="d882e-133">Salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d882e-133">Save the configuration.</span></span> <span data-ttu-id="d882e-134">Lasciare aperto il portale, poiché tra poco si dovrà registrare anche l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="d882e-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="d882e-135">Passaggio 2: Configurare l'app per l'uso della pipeline di autenticazione OWIN</span><span class="sxs-lookup"><span data-stu-id="d882e-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="d882e-136">Per convalidare le richieste in ingresso e i token, è necessario configurare l'applicazione per la comunicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d882e-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="d882e-137">Per iniziare, aprire la soluzione e aggiungere i pacchetti NuGet del middleware OWIN al progetto TodoListService usando la Console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d882e-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="d882e-138">Aggiungere al progetto TodoListService una OWIN Startup Class denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d882e-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d882e-139">Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** > **Nuovo elemento** e cercare **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="d882e-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="d882e-140">Il middleware OWIN richiamerà il metodo `Configuration(…)` all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="d882e-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="d882e-141">Modificare la dichiarazione di classe in `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="d882e-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="d882e-142">Parte di questa classe è stata già implementata in un altro file.</span><span class="sxs-lookup"><span data-stu-id="d882e-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="d882e-143">Nel metodo `Configuration(…)` effettuare una chiamata a `ConfgureAuth(…)` per configurare l'autenticazione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="d882e-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="d882e-144">Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(…)`.</span><span class="sxs-lookup"><span data-stu-id="d882e-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="d882e-145">I parametri forniti in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungeranno da coordinate per consentire all'app di comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d882e-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="d882e-146">A questo punto è possibile usare gli attributi `[Authorize]` per proteggere i controller e le azioni con l'autenticazione della connessione al token JSON Web (JWT).</span><span class="sxs-lookup"><span data-stu-id="d882e-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="d882e-147">Decorare la classe `Controllers\TodoListController.cs` con un tag di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="d882e-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="d882e-148">Ciò forzerà l'utente a eseguire l'accesso prima di accedere alla pagina.</span><span class="sxs-lookup"><span data-stu-id="d882e-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="d882e-149">Quando un chiamante autorizzato riesce a chiamare una delle API `TodoListController` , l'azione potrebbe richiedere l'accesso alle informazioni relative al chiamante.</span><span class="sxs-lookup"><span data-stu-id="d882e-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="d882e-150">OWIN fornisce l'accesso alle attestazioni all'interno del token di connessione tramite l'oggetto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="d882e-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="d882e-151">Un requisito comune per l'API Web è la convalida degli "ambiti" presenti nel token.</span><span class="sxs-lookup"><span data-stu-id="d882e-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="d882e-152">Ciò garantisce che l'utente goda delle autorizzazioni necessarie per accedere a To Do List Service.</span><span class="sxs-lookup"><span data-stu-id="d882e-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="d882e-153">Aprire il file `web.config` nella radice del progetto TodoListService e immettere i valori di configurazione nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="d882e-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d882e-154">`ida:Tenant` è il nome del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d882e-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d882e-155">`ida:Audience` è l'URI ID app dell'applicazione immesso nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d882e-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="d882e-156">Passaggio 3: Configurare un'applicazione client ed eseguire il servizio</span><span class="sxs-lookup"><span data-stu-id="d882e-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="d882e-157">Prima di poter vedere To Do List Service in azione, è necessario configurare To Do List Client, in modo che possa ricevere i token da Azure AD ed effettuare chiamate al servizio.</span><span class="sxs-lookup"><span data-stu-id="d882e-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="d882e-158">Tornare al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d882e-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d882e-159">Creare una nuova applicazione nel tenant di Azure AD e selezionare **Applicazione client nativa** nella richiesta risultante.</span><span class="sxs-lookup"><span data-stu-id="d882e-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="d882e-160">**Nome** descrive l'applicazione agli utenti.</span><span class="sxs-lookup"><span data-stu-id="d882e-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="d882e-161">Immettere `http://TodoListClient/` per il valore di **URI di reindirizzamento** .</span><span class="sxs-lookup"><span data-stu-id="d882e-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="d882e-162">Dopo aver completato la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="d882e-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="d882e-163">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d882e-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="d882e-164">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d882e-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="d882e-165">Individuare e selezionare To Do List Service, aggiungere l'autorizzazione di **Access TodoListService** in **Autorizzazioni delegate** e quindi fare clic su **Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="d882e-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="d882e-166">In Visual Studio aprire `App.config` nel progetto TodoListClient e quindi immettere i valori di configurazione nella sezione `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="d882e-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="d882e-167">`ida:Tenant` è il nome del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d882e-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d882e-168">`ida:ClientId` è l'ID app copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d882e-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="d882e-169">`todo:TodoListResourceId` è l'URI ID app dell'applicazione To Do List Service immesso nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d882e-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d882e-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d882e-170">Next steps</span></span>
<span data-ttu-id="d882e-171">Infine pulire, compilare ed eseguire ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="d882e-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="d882e-172">Se non si è ancora creato un nuovo utente nel tenant con un dominio *.onmicrosoft.com, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="d882e-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="d882e-173">Accedere al client To Do List come l'utente creato e aggiungere alcune attività all'elenco delle attività dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d882e-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="d882e-174">Come riferimento, l'esempio completo, senza valori di configurazione, è disponibile in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d882e-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d882e-175">È ora possibile passare ad altri scenari relativi alle identità.</span><span class="sxs-lookup"><span data-stu-id="d882e-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
