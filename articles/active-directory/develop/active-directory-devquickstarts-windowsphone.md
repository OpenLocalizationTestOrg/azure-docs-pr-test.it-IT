---
title: Introduzione a Windows Phone per Azure AD | Microsoft Docs
description: Come compilare un'applicazione di Windows Phone che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="837ba-103">Integrare Azure AD con un'app di Windows Phone</span><span class="sxs-lookup"><span data-stu-id="837ba-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="837ba-104">I progetti Windows Phone 8.1 e versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="837ba-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="837ba-105">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="837ba-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="837ba-106">Se si sta sviluppando un'app di Windows Phone 8.1, Azure AD semplifica e facilita l'autenticazione degli utenti con gli account Active Directory.</span><span class="sxs-lookup"><span data-stu-id="837ba-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="837ba-107">Consente inoltre all'applicazione di usare in modo sicuro qualsiasi API Web protetta da Azure AD, ad esempio le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="837ba-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="837ba-108">Questo esempio di codice usa ADAL versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="837ba-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="837ba-109">Per la tecnologia più recente, si consiglia di provare invece l' [esercitazione di Windows universale con ADAL versione 3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="837ba-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="837ba-110">Se si sta creando un'app per Windows Phone 8.1, questo è il posto giusto.</span><span class="sxs-lookup"><span data-stu-id="837ba-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="837ba-111">La versione 2.0 di ADAL è ancora completamente supportata ed è lo strumento consigliato per lo sviluppo di app per Windows Phone 8.1 con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="837ba-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="837ba-112">Per i client nativi .NET che devono accedere a risorse protette, Azure AD fornisce Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="837ba-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="837ba-113">La funzione di ADAL è di permettere all'app di ottenere facilmente i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="837ba-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="837ba-114">Per far capire quanto è semplice, verrà compilata un'app di Windows Phone 8.1, "Directory Searcher", che:</span><span class="sxs-lookup"><span data-stu-id="837ba-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="837ba-115">Ottiene i token di accesso per la chiamata all'API Graph di Azure AD con il [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="837ba-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="837ba-116">Cerca in una directory gli utenti con un determinato UPN.</span><span class="sxs-lookup"><span data-stu-id="837ba-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="837ba-117">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="837ba-117">Signs users out.</span></span>

<span data-ttu-id="837ba-118">Per compilare l'applicazione funzionante completa, sarà necessario:</span><span class="sxs-lookup"><span data-stu-id="837ba-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="837ba-119">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="837ba-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="837ba-120">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="837ba-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="837ba-121">Usare ADAL per ottenere i token da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="837ba-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="837ba-122">Per iniziare, [scaricare un progetto struttura](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="837ba-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="837ba-123">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="837ba-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="837ba-124">Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="837ba-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="837ba-125">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="837ba-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="837ba-126">1. Registrare l'applicazione Directory Searcher</span><span class="sxs-lookup"><span data-stu-id="837ba-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="837ba-127">Per consentire all'applicazione di ottenere i token, sarà innanzitutto necessario registrarla nel tenant di Azure AD e concederle l'autorizzazione per accedere all'API Graph di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="837ba-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="837ba-128">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="837ba-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="837ba-129">Nella barra in alto fare clic sull'account e nell'elenco **Directory** scegliere il tenant di Active Directory in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="837ba-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="837ba-130">Fare clic su **Altri servizi** nella barra di spostamento a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="837ba-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="837ba-131">Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="837ba-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="837ba-132">Seguire le istruzioni e creare una nuova **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="837ba-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="837ba-133">Il **Nome** dell'applicazione deve essere una descrizione per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="837ba-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="837ba-134">L' **URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD userà per restituire le risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="837ba-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="837ba-135">Per ora immettere un valore segnaposto, ad esempio `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="837ba-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="837ba-136">Questo valore verrà sostituito in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="837ba-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="837ba-137">Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.</span><span class="sxs-lookup"><span data-stu-id="837ba-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="837ba-138">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla scheda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="837ba-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="837ba-139">Nella pagina **Impostazioni** scegliere **Autorizzazioni necessarie** e quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="837ba-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="837ba-140">Selezionare **Microsoft Graph** come API e aggiungere l'autorizzazione **Lettura dati directory** in **Autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="837ba-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="837ba-141">In questo modo l'applicazione potrà cercare gli utenti nell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="837ba-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="837ba-142">2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="837ba-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="837ba-143">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="837ba-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="837ba-144">Affinché la libreria ADAL possa comunicare con Azure AD, è necessario fornire alcune informazioni relative alla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="837ba-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="837ba-145">Per prima cosa aggiungere ADAL al progetto DirectorySearcher usando la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="837ba-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="837ba-146">Nel progetto DirectorySearcher aprire `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="837ba-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="837ba-147">Sostituire i valori dell'area `Config Values` in modo che corrispondano ai valori inseriti nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="837ba-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="837ba-148">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="837ba-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="837ba-149">`tenant` è il dominio del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="837ba-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="837ba-150">`clientId` è l'ID client dell'applicazione copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="837ba-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="837ba-151">Ora è necessario individuare l'URI di callback per l'app di Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="837ba-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="837ba-152">Impostare un punto di interruzione in questa riga del metodo `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="837ba-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="837ba-153">Eseguire l'app e prendere nota del valore di `redirectUri` quando viene raggiunto il punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="837ba-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="837ba-154">Dovrebbe essere simile a</span><span class="sxs-lookup"><span data-stu-id="837ba-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="837ba-155">Sempre nella scheda **Configura** dell'applicazione nel portale di gestione di Azure sostituire il valore di **RedirectUri** con questo valore.</span><span class="sxs-lookup"><span data-stu-id="837ba-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="837ba-156">3. Usare ADAL per ottenere i token da AAD</span><span class="sxs-lookup"><span data-stu-id="837ba-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="837ba-157">Il principio alla base di ADAL è che l'app, ogni volta che ha bisogno di un token di accesso, deve solo chiamare `authContext.AcquireToken(…)` e ADAL fa il resto.</span><span class="sxs-lookup"><span data-stu-id="837ba-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="837ba-158">Il primo passaggio consiste nell'inizializzare l'oggetto `AuthenticationContext` dell'app, ovvero la classe primaria di ADAL,</span><span class="sxs-lookup"><span data-stu-id="837ba-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="837ba-159">dove si passano ad ADAL le coordinate di cui ha bisogno per comunicare con Azure AD e gli si indica come memorizzare i token nella cache.</span><span class="sxs-lookup"><span data-stu-id="837ba-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="837ba-160">Individuare ora il metodo `Search(...)`, che verrà richiamato quando l'utente fa clic sul pulsante "Search" nell'interfaccia utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="837ba-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="837ba-161">Questo metodo invia una richiesta GET all'API Graph di Azure AD per eseguire una query sugli utenti il cui UPN inizia con il termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="837ba-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="837ba-162">Per eseguire una query nell'API Graph, è però necessario includere un oggetto access_token nell'intestazione `Authorization` della richiesta, dove entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="837ba-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="837ba-163">Se è necessaria l'autenticazione interattiva, ADAL userà WAB (Web Authentication Broker) e il [modello di continuazione](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) di Windows Phone per visualizzare la pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="837ba-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="837ba-164">Quando l'utente effettua l'accesso, l'app deve passare ad ADAL i risultati dell'interazione WAB.</span><span class="sxs-lookup"><span data-stu-id="837ba-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="837ba-165">È semplice come implementare l'interfaccia `ContinueWebAuthentication` :</span><span class="sxs-lookup"><span data-stu-id="837ba-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="837ba-166">Ora è possibile usare l'oggetto `AuthenticationResult` restituito da ADAL all'app.</span><span class="sxs-lookup"><span data-stu-id="837ba-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="837ba-167">Nel callback `QueryGraph(...)` associare l'oggetto access_token acquisito alla richiesta GET nell'intestazione dell'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="837ba-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="837ba-168">È possibile usare l'oggetto `AuthenticationResult` anche per visualizzare informazioni sull'utente nell'app.</span><span class="sxs-lookup"><span data-stu-id="837ba-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="837ba-169">Nel metodo `QueryGraph(...)` usare il risultato per visualizzare l'ID dell'utente nella pagina:</span><span class="sxs-lookup"><span data-stu-id="837ba-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="837ba-170">Infine è possibile usare ADAL anche per disconnettere l'utente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="837ba-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="837ba-171">È opportuno assicurarsi che, quando l'utente fa clic sul pulsante "Sign Out", la chiamata successiva a `AcquireTokenSilentAsync(...)` abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="837ba-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="837ba-172">Con ADAL, basta cancellare la cache dei token:</span><span class="sxs-lookup"><span data-stu-id="837ba-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="837ba-173">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="837ba-173">Congratulations!</span></span> <span data-ttu-id="837ba-174">È stata compilata un'app di Windows Phone in grado di autenticare gli utenti, di chiamare in modo sicuro le API Web usando OAuth 2.0 e di ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="837ba-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="837ba-175">Se non si è ancora popolato il tenant con alcuni utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="837ba-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="837ba-176">Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.</span><span class="sxs-lookup"><span data-stu-id="837ba-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="837ba-177">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="837ba-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="837ba-178">Chiudere l'app e rieseguirla.</span><span class="sxs-lookup"><span data-stu-id="837ba-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="837ba-179">Si noti che la sessione dell'utente non è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="837ba-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="837ba-180">Disconnettersi e accedere nuovamente come un altro utente.</span><span class="sxs-lookup"><span data-stu-id="837ba-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="837ba-181">ADAL consente di incorporare facilmente nell'applicazione tutte queste funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="837ba-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="837ba-182">Esegue automaticamente le attività più complesse: gestione della cache, supporto del protocollo OAuth, presentazione all'utente di un'interfaccia utente di accesso, aggiornamento dei token scaduti e altro.</span><span class="sxs-lookup"><span data-stu-id="837ba-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="837ba-183">Tutto ciò che occorre conoscere è una sola chiamata all'API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="837ba-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="837ba-184">Come riferimento, viene fornito l'esempio completato (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="837ba-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="837ba-185">Ora è possibile passare ad altri scenari relativi alle identità.</span><span class="sxs-lookup"><span data-stu-id="837ba-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="837ba-186">È possibile:</span><span class="sxs-lookup"><span data-stu-id="837ba-186">You may want to try:</span></span>

[<span data-ttu-id="837ba-187">Proteggere un'API Web .NET con Azure AD >></span><span class="sxs-lookup"><span data-stu-id="837ba-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

