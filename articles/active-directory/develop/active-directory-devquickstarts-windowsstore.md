---
title: aaaAzure AD per Windows Store introduzione | Documenti Microsoft
description: Compilare app di Windows Store che si integrano con Azure AD per la registrazione e per chiamare le API protette di Azure AD tramite il protocollo OAuth.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="b7ece-103">Integrare Azure AD con le app di Windows Store</span><span class="sxs-lookup"><span data-stu-id="b7ece-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="b7ece-104">I progetti di Windows Store 8.1 e della versione precedente non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7ece-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="b7ece-105">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="b7ece-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="b7ece-106">Se si sviluppa App per Windows Store hello, Azure Active Directory (Azure AD) rende tooauthenticate semplici e diretti agli utenti con gli account di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b7ece-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="b7ece-107">Grazie all'integrazione con Azure AD, un'app utilizzabile in modo sicuro da qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7ece-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="b7ece-108">Per applicazioni desktop Windows Store che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="b7ece-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="b7ece-109">Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget hello app.</span><span class="sxs-lookup"><span data-stu-id="b7ece-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="b7ece-110">toodemonstrate facilmente, questo articolo illustra come toobuild un DirectorySearcher di Windows Store app che:</span><span class="sxs-lookup"><span data-stu-id="b7ece-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="b7ece-111">Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7ece-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b7ece-112">Cerca in una directory gli utenti con un determinato nome dell'entità utente (UPN).</span><span class="sxs-lookup"><span data-stu-id="b7ece-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="b7ece-113">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="b7ece-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="b7ece-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b7ece-114">Before you get started</span></span>
* <span data-ttu-id="b7ece-115">Scaricare hello [scheletro di progetto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b7ece-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="b7ece-116">Ognuno è una soluzione di Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b7ece-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="b7ece-117">È inoltre necessario un tenant di Azure Active Directory in cui gli utenti toocreate e registra hello app.</span><span class="sxs-lookup"><span data-stu-id="b7ece-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="b7ece-118">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b7ece-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="b7ece-119">Quando si è pronti, seguire le procedure di hello in hello prossime tre sezioni.</span><span class="sxs-lookup"><span data-stu-id="b7ece-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="b7ece-120">Passaggio 1: Registrare hello DirectorySearcher app</span><span class="sxs-lookup"><span data-stu-id="b7ece-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="b7ece-121">i token tooenable hello app tooget, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="b7ece-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="b7ece-122">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="b7ece-122">Here's how:</span></span>

1. <span data-ttu-id="b7ece-123">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b7ece-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b7ece-124">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="b7ece-124">On hello top bar, click your account.</span></span> <span data-ttu-id="b7ece-125">Quindi, in hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="b7ece-126">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7ece-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b7ece-127">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b7ece-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b7ece-128">Seguire hello richieste toocreate un **applicazione Client nativa**.</span><span class="sxs-lookup"><span data-stu-id="b7ece-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="b7ece-129">**Nome** descrive toousers app hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="b7ece-130">**URI di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte.</span><span class="sxs-lookup"><span data-stu-id="b7ece-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="b7ece-131">Immettere per ora un valore segnaposto, ad esempio **http://DirectorySearcher**.</span><span class="sxs-lookup"><span data-stu-id="b7ece-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="b7ece-132">Il valore di hello verranno sostituiti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b7ece-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="b7ece-133">Dopo aver completato la registrazione di hello, Azure AD le assegna app hello un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="b7ece-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="b7ece-134">Copiare il valore di hello in hello **applicazione** scheda, perché sarà necessaria successivamente.</span><span class="sxs-lookup"><span data-stu-id="b7ece-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="b7ece-135">In hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b7ece-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="b7ece-136">Per hello **Azure Active Directory** app, selezionare **Microsoft Graph** come hello API.</span><span class="sxs-lookup"><span data-stu-id="b7ece-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="b7ece-137">In **autorizzazioni delegate**, aggiungere hello **directory hello accesso come utente connesso di hello** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b7ece-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="b7ece-138">In questo modo consente hello tooquery hello app API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="b7ece-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="b7ece-139">Passaggio 2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="b7ece-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="b7ece-140">Ora che si dispone di un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="b7ece-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="b7ece-141">tooenable toocommunicate ADAL con Azure AD, assegnargli alcune informazioni di registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="b7ece-142">Aggiungere il progetto di DirectorySearcher toohello ADAL tramite la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="b7ece-143">Nel progetto DirectorySearcher hello, Apri il file MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="b7ece-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="b7ece-144">Sostituire i valori hello in hello **valori di configurazione** area con i valori hello immesso nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="b7ece-145">Il codice si riferisce valori toothese ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="b7ece-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b7ece-146">Hello *tenant* hello dominio del tenant di Azure Active Directory (ad esempio, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b7ece-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="b7ece-147">Hello *clientId* hello client ID dell'applicazione hello, che copiato dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="b7ece-148">URI di callback hello toodiscover è ora necessario per l'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b7ece-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="b7ece-149">Impostare un punto di interruzione in questa riga hello `MainPage` metodo:</span><span class="sxs-lookup"><span data-stu-id="b7ece-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="b7ece-150">Compilare la soluzione hello, assicurarsi che vengano ripristinati tutti i riferimenti del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b7ece-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="b7ece-151">Se tutti i pacchetti sono mancanti, aprire Gestione pacchetti NuGet hello e ripristinarli.</span><span class="sxs-lookup"><span data-stu-id="b7ece-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="b7ece-152">Eseguire app hello e copiare il valore di hello di `redirectUri` quando hello punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="b7ece-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="b7ece-153">il valore di Hello dovrebbe essere simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b7ece-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="b7ece-154">In hello **impostazioni** scheda dell'app hello in hello portale di Azure, aggiungere un **RedirectUri** con hello valore precedente.</span><span class="sxs-lookup"><span data-stu-id="b7ece-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="b7ece-155">Passaggio 3: I token usare ADAL tooget da Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7ece-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="b7ece-156">Hello principio fondamentale dietro ADAL è che ogni volta che l'applicazione hello necessita di un token di accesso, chiama semplicemente `authContext.AcquireToken(…)`, e ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="b7ece-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="b7ece-157">Inizializzazione dell'applicazione hello `AuthenticationContext`, ovvero hello classe principale della libreria ADAL.</span><span class="sxs-lookup"><span data-stu-id="b7ece-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="b7ece-158">Questa azione passa coordinate hello ADAL necessarie toocommunicate con Azure AD e indicare come token toocache.</span><span class="sxs-lookup"><span data-stu-id="b7ece-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="b7ece-159">Individuare hello `Search(...)` metodo, che viene richiamato quando gli utenti fanno clic hello **ricerca** pulsante nell'interfaccia utente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="b7ece-160">Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta get per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="b7ece-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="b7ece-161">hello tooquery API Graph, includere un token di accesso nella richiesta di hello **autorizzazione** intestazione.</span><span class="sxs-lookup"><span data-stu-id="b7ece-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="b7ece-162">È qui che entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="b7ece-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="b7ece-163">Quando richiede un token di app hello chiamando `AcquireTokenAsync(...)`, ADAL tenta tooreturn un token senza chiedere utente hello per le credenziali.</span><span class="sxs-lookup"><span data-stu-id="b7ece-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="b7ece-164">Se ADAL rileva che l'utente hello toosign in tooget un token, visualizza una finestra di dialogo di accesso, raccoglie le credenziali dell'utente hello e restituisce un token dopo l'autenticazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="b7ece-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="b7ece-165">Se la libreria ADAL è Impossibile tooreturn un token per qualsiasi motivo, hello *AuthenticationResult* lo stato è un errore.</span><span class="sxs-lookup"><span data-stu-id="b7ece-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="b7ece-166">È ora token di accesso di tempo toouse hello acquisita.</span><span class="sxs-lookup"><span data-stu-id="b7ece-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="b7ece-167">Anche in hello `Search(...)` (metodo), collegare toohello di hello token API Graph richiesta di recupero in hello **autorizzazione** intestazione:</span><span class="sxs-lookup"><span data-stu-id="b7ece-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="b7ece-168">È possibile utilizzare hello `AuthenticationResult` toodisplay informazioni utente hello in app hello, ad esempio hello ID utente dell'oggetto:</span><span class="sxs-lookup"><span data-stu-id="b7ece-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="b7ece-169">È anche possibile utilizzare toosign ADAL utenti all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="b7ece-170">Quando hello scelto hello **Sign Out** , verificare che chiamano Avanti hello troppo`AcquireTokenAsync(...)` viene illustrata una visualizzazione di accesso.</span><span class="sxs-lookup"><span data-stu-id="b7ece-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="b7ece-171">Con ADAL, questa azione è semplice come la cancellazione della cache dei token hello:</span><span class="sxs-lookup"><span data-stu-id="b7ece-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="b7ece-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7ece-172">What's next</span></span>
<span data-ttu-id="b7ece-173">È ora disponibile un'app di Windows Store che può autenticare gli utenti, in modo sicuro chiamare web API mediante OAuth 2.0 e ottenere le informazioni di base utente hello funzionante.</span><span class="sxs-lookup"><span data-stu-id="b7ece-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="b7ece-174">Se non sono stati già popolato il tenant con gli utenti, è pertanto toodo ora hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="b7ece-175">Eseguire l'app DirectorySearcher e quindi accedere con uno degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="b7ece-176">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="b7ece-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="b7ece-177">Chiudere l'applicazione hello ed eseguirla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b7ece-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="b7ece-178">Si noti come hello sessione rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="b7ece-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="b7ece-179">Disconnessione facendo toodisplay hello barra inferiore e quindi eseguire nuovamente l'accesso con un altro utente.</span><span class="sxs-lookup"><span data-stu-id="b7ece-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="b7ece-180">ADAL rende facile tooincorporate tutte queste funzionalità di identità comuni in app hello.</span><span class="sxs-lookup"><span data-stu-id="b7ece-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="b7ece-181">Si occupa di tutto il lavoro dirty hello, quali la gestione della cache, supporto del protocollo OAuth, presentate utente hello con interfaccia utente, un account di accesso e aggiornamento scaduto token.</span><span class="sxs-lookup"><span data-stu-id="b7ece-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="b7ece-182">È necessario tooknow solo una singola API chiamata, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="b7ece-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="b7ece-183">Per riferimento, scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (senza i valori di configurazione).</span><span class="sxs-lookup"><span data-stu-id="b7ece-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="b7ece-184">È possibile procedere in scenari con identità tooadditional.</span><span class="sxs-lookup"><span data-stu-id="b7ece-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="b7ece-185">Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b7ece-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
