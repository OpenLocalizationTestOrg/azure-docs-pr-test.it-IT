---
title: .NET aaaAzure AD introduzione | Documenti Microsoft
description: Toobuild un'applicazione Desktop di Windows .NET che si integra con Azure AD per l'accesso di Azure AD come protetto tramite OAuth API.
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="51a65-103">Integrare Azure AD in un'app WPF desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="51a65-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="51a65-104">Se si sta sviluppando un'applicazione desktop, Azure AD rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51a65-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="51a65-105">Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.</span><span class="sxs-lookup"><span data-stu-id="51a65-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="51a65-106">Per .NET native client che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library o ADAL.</span><span class="sxs-lookup"><span data-stu-id="51a65-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="51a65-107">Obiettivo esclusivo della libreria ADAL è toomake è più facile per i token di accesso tooget app.</span><span class="sxs-lookup"><span data-stu-id="51a65-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="51a65-108">la semplicità è, toodemonstrate qui creeremo un'applicazione elenco attività di WPF .NET che:</span><span class="sxs-lookup"><span data-stu-id="51a65-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="51a65-109">Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="51a65-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="51a65-110">Cerca in una directory gli utenti con un determinato alias.</span><span class="sxs-lookup"><span data-stu-id="51a65-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="51a65-111">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="51a65-111">Signs users out.</span></span>

<span data-ttu-id="51a65-112">toobuild hello completo lavoro dell'applicazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="51a65-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="51a65-113">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51a65-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="51a65-114">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="51a65-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="51a65-115">Usare i token ADAL tooget da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51a65-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="51a65-116">tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="51a65-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="51a65-117">Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="51a65-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="51a65-118">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="51a65-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="51a65-119">1. Registrare hello DirectorySearcher applicazione</span><span class="sxs-lookup"><span data-stu-id="51a65-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="51a65-120">tooenable token tooget app, è prima necessario tooregister tenant in Azure AD e concedergli hello tooaccess autorizzazione API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="51a65-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="51a65-121">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51a65-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="51a65-122">Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="51a65-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="51a65-123">Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51a65-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="51a65-124">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="51a65-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="51a65-125">Seguire le istruzioni di hello e creare un nuovo **applicazione Client nativa**.</span><span class="sxs-lookup"><span data-stu-id="51a65-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="51a65-126">Hello **nome** di hello applicazione descriverà tooend utenti applicazione</span><span class="sxs-lookup"><span data-stu-id="51a65-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="51a65-127">Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD utilizzerà le risposte token tooreturn.</span><span class="sxs-lookup"><span data-stu-id="51a65-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="51a65-128">Immettere ad esempio, un'applicazione specifica tooyour valore `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="51a65-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="51a65-129">Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.</span><span class="sxs-lookup"><span data-stu-id="51a65-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="51a65-130">È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="51a65-131">Da hello **impostazioni** pagina, scegliere **autorizzazioni obbligatorie** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="51a65-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="51a65-132">Seleziona hello **Microsoft Graph** come hello API e aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="51a65-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="51a65-133">In questo modo hello di tooquery l'applicazione API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="51a65-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="51a65-134">2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="51a65-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="51a65-135">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="51a65-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="51a65-136">Affinché toocommunicate in grado di toobe ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="51a65-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="51a65-137">Inizia ad aggiungere il progetto di DirectorySearcher toohello ADAL utilizzando Console Gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="51a65-138">Nel progetto DirectorySearcher hello aprire `app.config`.</span><span class="sxs-lookup"><span data-stu-id="51a65-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="51a65-139">Sostituire i valori hello elementi hello in hello `<appSettings>` hello tooreflect sezione valori di input nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="51a65-140">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="51a65-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="51a65-141">Hello `ida:Tenant` dominio hello del tenant di Azure AD, ad esempio contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="51a65-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="51a65-142">Hello `ida:ClientId` è clientId hello dell'applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="51a65-143">Hello `ida:RedirectUri` è hello è registrato nel portale di hello url di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="51a65-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="51a65-144">3.    Usare ADAL tooGet token da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51a65-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="51a65-145">Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente `authContext.AcquireTokenAsync(...)`, e ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="51a65-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="51a65-146">In hello `DirectorySearcher` progetto, aprire `MainWindow.xaml.cs` e individuare hello `MainWindow()` metodo.</span><span class="sxs-lookup"><span data-stu-id="51a65-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="51a65-147">primo passaggio Hello è tooinitialize dell'app `AuthenticationContext` -ADAL della classe primaria.</span><span class="sxs-lookup"><span data-stu-id="51a65-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="51a65-148">Si tratta in cui si passa ADAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.</span><span class="sxs-lookup"><span data-stu-id="51a65-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="51a65-149">Ora individuare hello `Search(...)` metodo, che verrà richiamato quando hello utente cliks hello "Ricerca" pulsante nell'interfaccia utente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="51a65-150">Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="51a65-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="51a65-151">Ma in hello tooquery ordine API Graph, è necessario tooinclude access_token in hello `Authorization` richiesta di intestazione di hello - si tratta in cui è disponibile in ADAL.</span><span class="sxs-lookup"><span data-stu-id="51a65-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="51a65-152">Quando l'app richiede un token chiamando `AcquireTokenAsync(...)`, ADAL tenterà tooreturn un token senza chiedere utente hello per le credenziali.</span><span class="sxs-lookup"><span data-stu-id="51a65-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="51a65-153">Se ADAL rileva che l'utente hello toosign in tooget un token, verrà visualizzato una finestra di dialogo account di accesso, raccogliere le credenziali dell'utente hello e restituisce un token alla riuscita dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="51a65-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="51a65-154">Se la libreria ADAL è Impossibile tooreturn un token per qualsiasi motivo, verrà generata una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="51a65-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="51a65-155">Si noti che hello `AuthenticationResult` oggetto contiene un `UserInfo` oggetto che può essere utilizzato toocollect informazioni dell'app potrebbe essere necessario.</span><span class="sxs-lookup"><span data-stu-id="51a65-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="51a65-156">In hello DirectorySearcher, `UserInfo` è l'interfaccia utente dell'applicazione hello toocustomize utilizzato con l'id dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="51a65-157">Quando l'utente hello fa clic sul pulsante "Sign Out" hello, si vuole tooensure che hello chiamata successiva troppo`AcquireTokenAsync(...)` chiederà toosign utente hello in.</span><span class="sxs-lookup"><span data-stu-id="51a65-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="51a65-158">Con ADAL, non è semplice come la cancellazione della cache dei token hello:</span><span class="sxs-lookup"><span data-stu-id="51a65-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="51a65-159">Tuttavia, se utente hello non fa clic sul pulsante "Sign Out" hello, si desidererà toomaintain hello sessione utente per hello successiva esecuzione hello DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="51a65-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="51a65-160">Quando viene avviata l'applicazione hello, è possibile controllare cache del token della libreria ADAL per un token esistente e aggiornare di conseguenza hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="51a65-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="51a65-161">In hello `CheckForCachedToken()` (metodo), eseguire un'altra chiamata troppo`AcquireTokenAsync(...)`, questa volta passando hello `PromptBehavior.Never` parametro.</span><span class="sxs-lookup"><span data-stu-id="51a65-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="51a65-162">`PromptBehavior.Never`indicherà ADAL che hello utente non viene richiesto per l'accesso e ADAL deve invece generare un'eccezione se è Impossibile tooreturn un token.</span><span class="sxs-lookup"><span data-stu-id="51a65-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="51a65-163">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="51a65-163">Congratulations!</span></span> <span data-ttu-id="51a65-164">È ora un'applicazione WPF .NET con gli utenti di hello possibilità tooauthenticate funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="51a65-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="51a65-165">Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="51a65-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="51a65-166">Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.</span><span class="sxs-lookup"><span data-stu-id="51a65-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="51a65-167">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="51a65-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="51a65-168">Chiudere l'applicazione hello ed eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="51a65-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="51a65-169">Si noti come hello sessione rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="51a65-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="51a65-170">Disconnettersi e accedere nuovamente come un altro utente.</span><span class="sxs-lookup"><span data-stu-id="51a65-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="51a65-171">ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="51a65-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="51a65-172">Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="51a65-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="51a65-173">Ciò che occorre tooknow è una singola chiamata API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="51a65-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="51a65-174">Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="51a65-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="51a65-175">È possibile procedere con tooadditional scenari.</span><span class="sxs-lookup"><span data-stu-id="51a65-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="51a65-176">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="51a65-176">You may want tootry:</span></span>

[<span data-ttu-id="51a65-177">Proteggere un'API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="51a65-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

