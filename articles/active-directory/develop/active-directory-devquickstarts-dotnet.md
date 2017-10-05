---
title: Introduzione a .NET per Azure AD | Documentazione Microsoft
description: Come compilare un'applicazione desktop di Windows .NET che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="48e75-103">Integrare Azure AD in un'app WPF desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="48e75-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="48e75-104">Se si sta sviluppando un'applicazione desktop, Azure AD semplifica e facilita l'autenticazione degli utenti con gli account Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48e75-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="48e75-105">Consente inoltre all'applicazione di usare in modo sicuro qualsiasi API Web protetta da Azure AD, ad esempio le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="48e75-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="48e75-106">Per i client nativi .NET che devono accedere a risorse protette, Azure AD fornisce Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="48e75-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="48e75-107">La funzione di ADAL è di permettere all'app di ottenere facilmente i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="48e75-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="48e75-108">Per far capire quanto è semplice, verrà compilata un'applicazione WPF .NET To-Do List che:</span><span class="sxs-lookup"><span data-stu-id="48e75-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="48e75-109">Ottiene i token di accesso per la chiamata all'API Graph di Azure AD con il [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="48e75-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="48e75-110">Cerca in una directory gli utenti con un determinato alias.</span><span class="sxs-lookup"><span data-stu-id="48e75-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="48e75-111">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="48e75-111">Signs users out.</span></span>

<span data-ttu-id="48e75-112">Per compilare l'applicazione funzionante completa, sarà necessario:</span><span class="sxs-lookup"><span data-stu-id="48e75-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="48e75-113">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e75-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="48e75-114">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="48e75-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="48e75-115">Usare ADAL per ottenere i token da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e75-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="48e75-116">Per iniziare, [scaricare la struttura dell'app](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="48e75-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="48e75-117">Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48e75-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="48e75-118">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="48e75-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="48e75-119">1. Registrare l'applicazione DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="48e75-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="48e75-120">Per consentire all'applicazione di ottenere i token, sarà innanzitutto necessario registrarla nel tenant di Azure AD e concederle l'autorizzazione per accedere all'API Graph di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="48e75-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="48e75-121">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48e75-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="48e75-122">Nella barra in alto fare clic sull'account e nell'elenco **Directory** scegliere il tenant di Active Directory in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48e75-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="48e75-123">Fare clic su **Altri servizi** nella barra di spostamento a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48e75-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="48e75-124">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="48e75-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="48e75-125">Seguire le istruzioni e creare una nuova **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="48e75-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="48e75-126">Il **Nome** dell'applicazione deve essere una descrizione per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="48e75-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="48e75-127">L' **URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD userà per restituire le risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="48e75-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="48e75-128">Immettere un valore specifico per l'applicazione, ad esempio `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="48e75-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="48e75-129">Dopo avere completato la registrazione, AAD assegnerà all'app un'ID app univoca.</span><span class="sxs-lookup"><span data-stu-id="48e75-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="48e75-130">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48e75-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="48e75-131">Nella pagina **Impostazioni** scegliere **Autorizzazioni necessarie** e quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="48e75-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="48e75-132">Selezionare **Microsoft Graph** come API e aggiungere l'autorizzazione **Lettura dati directory** in **Autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="48e75-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="48e75-133">In questo modo l'applicazione potrà cercare gli utenti nell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="48e75-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="48e75-134">2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="48e75-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="48e75-135">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="48e75-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="48e75-136">Affinché la libreria ADAL possa comunicare con Azure AD, è necessario fornire alcune informazioni relative alla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="48e75-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="48e75-137">Per prima cosa aggiungere ADAL al progetto DirectorySearcher usando la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="48e75-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="48e75-138">Nel progetto DirectorySearcher aprire `app.config`.</span><span class="sxs-lookup"><span data-stu-id="48e75-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="48e75-139">Sostituire i valori degli elementi nella sezione `<appSettings>` in modo che corrispondano ai valori inseriti nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="48e75-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="48e75-140">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="48e75-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="48e75-141">`ida:Tenant` è il dominio del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="48e75-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="48e75-142">`ida:ClientId` è l'ID client dell'applicazione copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="48e75-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="48e75-143">`ida:RedirectUri` è l'URL di reindirizzamento registrato nel portale.</span><span class="sxs-lookup"><span data-stu-id="48e75-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="48e75-144">3.    Usare ADAL per ottenere i token da AAD</span><span class="sxs-lookup"><span data-stu-id="48e75-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="48e75-145">Il principio alla base di ADAL è che l'app, ogni volta che ha bisogno di un token di accesso, deve solo chiamare `authContext.AcquireTokenAsync(...)` e ADAL fa il resto.</span><span class="sxs-lookup"><span data-stu-id="48e75-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="48e75-146">Nel progetto `DirectorySearcher` aprire `MainWindow.xaml.cs` e individuare il metodo `MainWindow()`.</span><span class="sxs-lookup"><span data-stu-id="48e75-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="48e75-147">Il primo passaggio consiste nell'inizializzare l'oggetto `AuthenticationContext` dell'app, ovvero la classe primaria di ADAL,</span><span class="sxs-lookup"><span data-stu-id="48e75-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="48e75-148">dove si passano ad ADAL le coordinate di cui ha bisogno per comunicare con Azure AD e gli si indica come memorizzare i token nella cache.</span><span class="sxs-lookup"><span data-stu-id="48e75-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="48e75-149">Individuare ora il metodo `Search(...)`, che verrà richiamato quando l'utente fa clic sul pulsante "Search" nell'interfaccia utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="48e75-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="48e75-150">Questo metodo invia una richiesta GET all'API Graph di Azure AD per eseguire una query sugli utenti il cui UPN inizia con il termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="48e75-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="48e75-151">Per eseguire una query nell'API Graph, è però necessario includere un oggetto access_token nell'intestazione `Authorization` della richiesta, dove entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="48e75-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="48e75-152">Quando l'app richiede un token chiamando `AcquireTokenAsync(...)`, ADAL tenterà di restituire un token senza chiedere le credenziali all'utente.</span><span class="sxs-lookup"><span data-stu-id="48e75-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="48e75-153">Se ADAL determina che l'utente deve effettuare l'accesso per ottenere un token, visualizzerà una finestra di dialogo di accesso, raccoglierà le credenziali dell'utente e restituirà un token al termine dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="48e75-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="48e75-154">Se ADAL non può restituire un token per qualsiasi motivo, genera una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="48e75-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="48e75-155">Si noti che l'oggetto `AuthenticationResult` contiene un oggetto `UserInfo` che può essere usato per raccogliere informazioni che potrebbero essere richieste dall'app.</span><span class="sxs-lookup"><span data-stu-id="48e75-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="48e75-156">In DirectorySearcher `UserInfo` viene usato per personalizzare l'interfaccia utente dell'app con l'ID dell'utente.</span><span class="sxs-lookup"><span data-stu-id="48e75-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="48e75-157">È opportuno assicurarsi che, quando l'utente fa clic sul pulsante "Sign Out", la chiamata successiva a `AcquireTokenAsync(...)` chiederà all'utente di accedere.</span><span class="sxs-lookup"><span data-stu-id="48e75-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="48e75-158">Con ADAL, basta cancellare la cache dei token:</span><span class="sxs-lookup"><span data-stu-id="48e75-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="48e75-159">Se tuttavia l'utente non fa clic sul pulsante di "disconnessione", è consigliabile mantenere la sessione dell'utente per la prossima esecuzione di DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="48e75-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="48e75-160">Quando viene avviata l'app, è possibile cercare nella cache dei token di ADAL se esiste un token e aggiornare di conseguenza l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="48e75-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="48e75-161">Nel metodo `CheckForCachedToken()`, eseguire un'altra chiamata a `AcquireTokenAsync(...)`, questa volta superando il parametro `PromptBehavior.Never`.</span><span class="sxs-lookup"><span data-stu-id="48e75-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="48e75-162">`PromptBehavior.Never` comunicherà ad ADAL che non dovrà richiedere all'utente di accedere e dovrà invece generare un'eccezione se non è in grado di restituire un token.</span><span class="sxs-lookup"><span data-stu-id="48e75-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
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

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="48e75-163">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="48e75-163">Congratulations!</span></span> <span data-ttu-id="48e75-164">È stata compilata un'applicazione WPF .NET in grado di autenticare gli utenti, di chiamare in modo sicuro le API Web usando OAuth 2.0 e di ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="48e75-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="48e75-165">Se non si è ancora popolato il tenant con alcuni utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="48e75-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="48e75-166">Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.</span><span class="sxs-lookup"><span data-stu-id="48e75-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="48e75-167">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="48e75-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="48e75-168">Chiudere l'app e rieseguirla.</span><span class="sxs-lookup"><span data-stu-id="48e75-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="48e75-169">Si noti che la sessione dell'utente non è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="48e75-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="48e75-170">Disconnettersi e accedere nuovamente come un altro utente.</span><span class="sxs-lookup"><span data-stu-id="48e75-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="48e75-171">ADAL consente di incorporare facilmente nell'applicazione tutte queste funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="48e75-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="48e75-172">Esegue automaticamente le attività più complesse: gestione della cache, supporto del protocollo OAuth, presentazione all'utente di un'interfaccia utente di accesso, aggiornamento dei token scaduti e altro.</span><span class="sxs-lookup"><span data-stu-id="48e75-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="48e75-173">Tutto ciò che occorre conoscere è una sola chiamata all'API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="48e75-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="48e75-174">Come riferimento, viene fornito l'esempio completato (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="48e75-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="48e75-175">Ora è possibile passare ad altri scenari.</span><span class="sxs-lookup"><span data-stu-id="48e75-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="48e75-176">È possibile:</span><span class="sxs-lookup"><span data-stu-id="48e75-176">You may want to try:</span></span>

[<span data-ttu-id="48e75-177">Proteggere un'API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="48e75-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

