---
title: Guida introduttiva di Windows Phone AD aaaAzure | Documenti Microsoft
description: Toobuild un'applicazione Windows Phone che si integra con Azure AD per l'accesso di Azure AD come protetto tramite OAuth API.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="9b02d-103">Integrare Azure AD con un'app di Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9b02d-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="9b02d-104">I progetti Windows Phone 8.1 e versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9b02d-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="9b02d-105">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="9b02d-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="9b02d-106">Se si sta sviluppando un'app di Windows Phone 8.1, Azure AD rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b02d-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="9b02d-107">Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b02d-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="9b02d-108">Questo esempio di codice usa ADAL versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="9b02d-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="9b02d-109">Per la tecnologia più recente di hello, è possibile provare a tooinstead nostri [esercitazione di Windows universale usando v 3.0 ADAL](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="9b02d-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="9b02d-110">Se si tratta effettivamente di un'app per Windows Phone 8.1, è giusto hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="9b02d-111">ADAL v 2.0 è ancora completamente supportata e hello modo consigliato di agianst lo sviluppo di App Windows Phone 8.1 Usa Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b02d-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="9b02d-112">Per .NET native client che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library o ADAL.</span><span class="sxs-lookup"><span data-stu-id="9b02d-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="9b02d-113">Obiettivo esclusivo della libreria ADAL è toomake è più facile per i token di accesso tooget app.</span><span class="sxs-lookup"><span data-stu-id="9b02d-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="9b02d-114">la semplicità è, toodemonstrate qui, verrà creata una "ricerca di Directory" app di Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="9b02d-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="9b02d-115">Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b02d-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="9b02d-116">Cerca in una directory gli utenti con un determinato UPN.</span><span class="sxs-lookup"><span data-stu-id="9b02d-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="9b02d-117">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b02d-117">Signs users out.</span></span>

<span data-ttu-id="9b02d-118">toobuild hello completo lavoro dell'applicazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9b02d-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="9b02d-119">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b02d-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="9b02d-120">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="9b02d-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="9b02d-121">Usare i token ADAL tooget da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b02d-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="9b02d-122">tooget avviato, [scaricare un progetto di base](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9b02d-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="9b02d-123">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9b02d-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="9b02d-124">Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b02d-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="9b02d-125">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9b02d-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="9b02d-126">1. Registrare l'applicazione di funzione di ricerca di Directory hello</span><span class="sxs-lookup"><span data-stu-id="9b02d-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="9b02d-127">tooenable token tooget app, è prima necessario tooregister tenant in Azure AD e concedergli hello tooaccess autorizzazione API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="9b02d-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="9b02d-128">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b02d-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b02d-129">Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b02d-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="9b02d-130">Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b02d-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9b02d-131">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b02d-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="9b02d-132">Seguire le istruzioni di hello e creare un nuovo **applicazione Client nativa**.</span><span class="sxs-lookup"><span data-stu-id="9b02d-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="9b02d-133">Hello **nome** di hello applicazione descriverà tooend utenti applicazione</span><span class="sxs-lookup"><span data-stu-id="9b02d-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="9b02d-134">Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD utilizzerà le risposte token tooreturn.</span><span class="sxs-lookup"><span data-stu-id="9b02d-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="9b02d-135">Per ora immettere un valore segnaposto, ad esempio `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="9b02d-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="9b02d-136">Questo valore verrà sostituito in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9b02d-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="9b02d-137">Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.</span><span class="sxs-lookup"><span data-stu-id="9b02d-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="9b02d-138">È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="9b02d-139">Da hello **impostazioni** pagina, scegliere **autorizzazioni obbligatorie** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b02d-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="9b02d-140">Seleziona hello **Microsoft Graph** come hello API e aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="9b02d-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="9b02d-141">In questo modo hello di tooquery l'applicazione API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b02d-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="9b02d-142">2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="9b02d-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="9b02d-143">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="9b02d-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="9b02d-144">Affinché toocommunicate in grado di toobe ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9b02d-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="9b02d-145">Inizia ad aggiungere il progetto di DirectorySearcher toohello ADAL utilizzando Console Gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="9b02d-146">Nel progetto DirectorySearcher hello aprire `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="9b02d-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="9b02d-147">Sostituire i valori hello in hello `Config Values` hello tooreflect area valori input in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b02d-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="9b02d-148">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="9b02d-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="9b02d-149">Hello `tenant` dominio hello del tenant di Azure AD, ad esempio contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="9b02d-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="9b02d-150">Hello `clientId` è clientId hello dell'applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="9b02d-151">Uri di callback toodiscover hello è ora necessario per l'app di Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="9b02d-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="9b02d-152">Impostare un punto di interruzione in questa riga hello `MainPage` metodo:</span><span class="sxs-lookup"><span data-stu-id="9b02d-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="9b02d-153">Eseguire app hello e copiare riservato valore hello `redirectUri` quando hello punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="9b02d-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="9b02d-154">Dovrebbe essere simile a</span><span class="sxs-lookup"><span data-stu-id="9b02d-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="9b02d-155">In hello **configura** scheda dell'applicazione nel portale di gestione di Azure, hello sostituire il valore di hello di hello **RedirectUri** con questo valore.</span><span class="sxs-lookup"><span data-stu-id="9b02d-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="9b02d-156">3. Usare ADAL tooGet token da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b02d-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="9b02d-157">Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente `authContext.AcquireToken(…)`, e ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="9b02d-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="9b02d-158">primo passaggio Hello è tooinitialize dell'app `AuthenticationContext` -ADAL della classe primaria.</span><span class="sxs-lookup"><span data-stu-id="9b02d-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="9b02d-159">Si tratta in cui si passa ADAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.</span><span class="sxs-lookup"><span data-stu-id="9b02d-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="9b02d-160">Ora individuare hello `Search(...)` metodo, che verrà richiamato quando hello utente cliks hello "Ricerca" pulsante nell'interfaccia utente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="9b02d-161">Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="9b02d-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="9b02d-162">Ma in hello tooquery ordine API Graph, è necessario tooinclude access_token in hello `Authorization` richiesta di intestazione di hello - si tratta in cui è disponibile in ADAL.</span><span class="sxs-lookup"><span data-stu-id="9b02d-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="9b02d-163">Se è necessaria l'autenticazione interattiva, ADAL utilizzerà Web l'autenticazione di Service Broker (Rubrica di Windows Phone) e [modello continuazione](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="9b02d-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="9b02d-164">Quando l'accesso dell'utente hello, l'app deve risultati hello ADAL toopass di interazione della Rubrica di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="9b02d-165">Questo è semplice come l'implementazione di hello `ContinueWebAuthentication` interfaccia:</span><span class="sxs-lookup"><span data-stu-id="9b02d-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="9b02d-166">Ora è hello toouse ora `AuthenticationResult` che ADAL restituito tooyour app.</span><span class="sxs-lookup"><span data-stu-id="9b02d-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="9b02d-167">In hello `QueryGraph(...)` callback, collegare access_token hello è stato acquistato toohello GET richiesta nell'intestazione di autorizzazione hello:</span><span class="sxs-lookup"><span data-stu-id="9b02d-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="9b02d-168">È inoltre possibile utilizzare hello `AuthenticationResult` toodisplay informazioni utente hello nell'app dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9b02d-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="9b02d-169">In hello `QueryGraph(...)` metodo, utilizzare hello risultato tooshow hello l'id dell'utente nella pagina hello:</span><span class="sxs-lookup"><span data-stu-id="9b02d-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="9b02d-170">Infine, è possibile utilizzare utente hello toosign ADAL fuori anche dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b02d-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="9b02d-171">Quando l'utente hello fa clic sul pulsante "Sign Out" hello, si vuole tooensure che hello chiamata successiva troppo`AcquireTokenSilentAsync(...)` avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9b02d-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="9b02d-172">Con ADAL, non è semplice come la cancellazione della cache dei token hello:</span><span class="sxs-lookup"><span data-stu-id="9b02d-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="9b02d-173">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="9b02d-173">Congratulations!</span></span> <span data-ttu-id="9b02d-174">È ora un'app di Windows Phone con gli utenti di hello possibilità tooauthenticate funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="9b02d-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="9b02d-175">Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="9b02d-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="9b02d-176">Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.</span><span class="sxs-lookup"><span data-stu-id="9b02d-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="9b02d-177">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="9b02d-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="9b02d-178">Chiudere l'applicazione hello ed eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9b02d-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="9b02d-179">Si noti come hello sessione rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="9b02d-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="9b02d-180">Disconnettersi e accedere nuovamente come un altro utente.</span><span class="sxs-lookup"><span data-stu-id="9b02d-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="9b02d-181">ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b02d-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="9b02d-182">Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="9b02d-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="9b02d-183">Ciò che occorre tooknow è una singola chiamata API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="9b02d-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="9b02d-184">Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9b02d-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="9b02d-185">È possibile procedere in scenari con identità tooadditional.</span><span class="sxs-lookup"><span data-stu-id="9b02d-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="9b02d-186">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="9b02d-186">You may want tootry:</span></span>

[<span data-ttu-id="9b02d-187">Proteggere un'API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="9b02d-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

