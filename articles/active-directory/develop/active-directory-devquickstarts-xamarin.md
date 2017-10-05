---
title: Introduzione a Xamarin per Azure AD | Microsoft Docs
description: Compilare un'applicazione Xamarin che si integra con Azure AD per l'accesso e chiama le API protette da Azure AD usando OAuth.
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="70a69-103">Integrare Azure AD in app Xamarin</span><span class="sxs-lookup"><span data-stu-id="70a69-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="70a69-104">Xamarin consente di scrivere app per dispositivi mobili in C# che possono essere eseguite in iOS, Android e Windows, in dispositivi mobili e PC.</span><span class="sxs-lookup"><span data-stu-id="70a69-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="70a69-105">Per la compilazione di un'app con Xamarin, Azure Active Directory (Azure AD) semplifica l'autenticazione degli utenti con i relativi account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a69-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="70a69-106">L'app può utilizzare in modo sicuro qualsiasi API Web protetta da Azure AD, come le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a69-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="70a69-107">Per le app Xamarin che devono accedere a risorse protette, in Azure AD è disponibile Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="70a69-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="70a69-108">L'unica funzione di ADAL è semplificare l'acquisizione dei token di accesso da parte delle app.</span><span class="sxs-lookup"><span data-stu-id="70a69-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="70a69-109">Per far capire quanto sia semplice, questo articolo illustra come compilare un'app DirectorySearcher che:</span><span class="sxs-lookup"><span data-stu-id="70a69-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="70a69-110">Viene eseguita in iOS, Android, Windows Desktop, Windows Phone e Windows Store.</span><span class="sxs-lookup"><span data-stu-id="70a69-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="70a69-111">Usa una sola libreria di classi portabile per autenticare gli utenti e ottenere i token per l'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a69-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="70a69-112">Cerca in una directory gli utenti con un determinato UPN.</span><span class="sxs-lookup"><span data-stu-id="70a69-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="70a69-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="70a69-113">Before you get started</span></span>
* <span data-ttu-id="70a69-114">Scaricare il [progetto struttura](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip) oppure l'[esempio completato](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="70a69-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="70a69-115">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="70a69-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="70a69-116">È necessario anche un tenant di Azure AD in cui creare gli utenti e registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="70a69-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="70a69-117">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="70a69-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="70a69-118">Quando si è pronti, attenersi alle procedure descritte nelle quattro sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="70a69-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="70a69-119">Passaggio 1: Configurare l'ambiente di sviluppo Xamarin</span><span class="sxs-lookup"><span data-stu-id="70a69-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="70a69-120">Dal momento che questa esercitazione include progetti per iOS, Android e Windows, sono necessari sia Visual Studio che Xamarin.</span><span class="sxs-lookup"><span data-stu-id="70a69-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="70a69-121">Per creare l'ambiente necessario, seguire la procedura riportata in [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) in MSDN.</span><span class="sxs-lookup"><span data-stu-id="70a69-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="70a69-122">Le istruzioni includono informazioni relative a Xamarin che è possibile leggere in attesa del completamento delle installazioni.</span><span class="sxs-lookup"><span data-stu-id="70a69-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="70a69-123">Al termine della configurazione, aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70a69-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="70a69-124">Sono presenti sei progetti: cinque progetti specifici delle piattaforme e una libreria di classi portabile, DirectorySearcher.cs, che verrà condivisa tra tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="70a69-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="70a69-125">Passaggio 2: Registrare l'app DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="70a69-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="70a69-126">Per consentire all'app di ottenere i token, sarà prima necessario registrarla nel tenant di Azure AD e concederle l'autorizzazione per accedere all'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a69-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="70a69-127">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="70a69-127">Here's how:</span></span>

1. <span data-ttu-id="70a69-128">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70a69-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="70a69-129">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="70a69-129">On the top bar, click your account.</span></span> <span data-ttu-id="70a69-130">Nell'elenco **Directory** selezionare quindi il tenant di Active Directory in cui si vuole registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="70a69-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="70a69-131">Fare clic su **Altri servizi** nel riquadro a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70a69-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="70a69-132">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="70a69-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="70a69-133">Seguire le istruzioni e creare una nuova **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="70a69-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="70a69-134">Il **Nome** descrive l'app agli utenti.</span><span class="sxs-lookup"><span data-stu-id="70a69-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="70a69-135">L'**URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD usa per restituire le risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="70a69-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="70a69-136">Immettere un valore, ad esempio http://DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="70a69-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="70a69-137">Dopo aver completato la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="70a69-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="70a69-138">Copiare il valore dalla scheda **Applicazione**, perché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="70a69-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="70a69-139">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="70a69-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="70a69-140">Selezionare l'API **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="70a69-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="70a69-141">In **Autorizzazioni delegate** aggiungere l'autorizzazione **Lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="70a69-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="70a69-142">Ciò consente all'app di eseguire query nell'API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="70a69-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="70a69-143">Passaggio 3: Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="70a69-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="70a69-144">Ora che è disponibile un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="70a69-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="70a69-145">Per abilitare ADAL alla comunicazione con Azure AD, fornire alcune informazioni sulla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="70a69-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="70a69-146">Aggiungere ADAL al progetto DirectorySearcher usando la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="70a69-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="70a69-147">Si noti che a ogni progetto vengono aggiunti due riferimenti alla libreria, ovvero la parte relativa alla libreria di classi portabile di ADAL e una parte specifica della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="70a69-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="70a69-148">Nel progetto DirectorySearcherLib aprire DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="70a69-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="70a69-149">Sostituire i valori dei membri della classe con i valori immessi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a69-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="70a69-150">Il codice fa riferimento a questi valori ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="70a69-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="70a69-151">Il *tenant* è il dominio del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="70a69-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="70a69-152">Il *clientId* è l'ID client dell'app che è stato copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="70a69-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="70a69-153">Il *returnUri* è l'URI di reindirizzamento immesso nel portale, ad esempio http://DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="70a69-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="70a69-154">Passaggio 4: Usare ADAL per ottenere token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a69-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="70a69-155">Quasi tutta la logica di autenticazione dell'app si basa su `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="70a69-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="70a69-156">Nei progetti specifici delle piattaforme è sufficiente passare un parametro contestuale alla libreria di classi portabile di `DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="70a69-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="70a69-157">Aprire DirectorySearcher.cs e quindi aggiungere un nuovo parametro per il metodo `SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="70a69-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="70a69-158">`IPlatformParameters` è il parametro contestuale che incapsula gli oggetti specifici delle piattaforme necessari ad ADAL per eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="70a69-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="70a69-159">Inizializzare `AuthenticationContext`, ovvero la classe primaria di ADAL.</span><span class="sxs-lookup"><span data-stu-id="70a69-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="70a69-160">Questa azione permette di passare ad ADAL le coordinate necessarie per comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a69-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="70a69-161">Chiamare `AcquireTokenAsync(...)`, che accetta l'oggetto `IPlatformParameters` e richiama il flusso di autenticazione necessario per restituire un token all'app.</span><span class="sxs-lookup"><span data-stu-id="70a69-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="70a69-162">`AcquireTokenAsync(...)` tenta prima di restituire un token per la risorsa necessaria, in questo caso, l'API Graph, senza chiedere all'utente di immettere le credenziali. A questo scopo vengono usati i token memorizzati nella cache o vengono aggiornati i token precedenti.</span><span class="sxs-lookup"><span data-stu-id="70a69-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="70a69-163">Se necessario, viene visualizzata la pagina di accesso di Azure AD prima di acquisire il token richiesto.</span><span class="sxs-lookup"><span data-stu-id="70a69-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="70a69-164">Associare il token di accesso alla richiesta dell'API Graph nell'intestazione **Authorization**:</span><span class="sxs-lookup"><span data-stu-id="70a69-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="70a69-165">Non sono necessarie altre operazioni per la libreria di classi portabile di `DirectorySearcher` e il codice relativo all'identità dell'app.</span><span class="sxs-lookup"><span data-stu-id="70a69-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="70a69-166">Non resta che chiamare il metodo `SearchByAlias(...)` nelle visualizzazioni di ciascuna piattaforma e, se necessario, aggiungere il codice per la corretta gestione del ciclo di vita dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="70a69-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="70a69-167">Android</span><span class="sxs-lookup"><span data-stu-id="70a69-167">Android</span></span>
1. <span data-ttu-id="70a69-168">In MainActivity.cs aggiungere una chiamata a `SearchByAlias(...)` nel gestore di clic del pulsante:</span><span class="sxs-lookup"><span data-stu-id="70a69-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="70a69-169">Eseguire l'override del metodo del ciclo di vita `OnActivityResult` per inoltrare i reindirizzamenti dell'autenticazione al metodo appropriato.</span><span class="sxs-lookup"><span data-stu-id="70a69-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="70a69-170">ADAL fornisce un apposito metodo helper in Android:</span><span class="sxs-lookup"><span data-stu-id="70a69-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="70a69-171">Desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="70a69-171">Windows Desktop</span></span>
<span data-ttu-id="70a69-172">In MainWindow.xaml.cs effettuare una chiamata a `SearchByAlias(...)` passando `WindowInteropHelper` nell'oggetto `PlatformParameters` del desktop:</span><span class="sxs-lookup"><span data-stu-id="70a69-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="70a69-173">iOS</span><span class="sxs-lookup"><span data-stu-id="70a69-173">iOS</span></span>
<span data-ttu-id="70a69-174">In DirSearchClient_iOSViewController.cs l'oggetto iOS `PlatformParameters` accetta un riferimento al controller di visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="70a69-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="70a69-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="70a69-175">Windows Universal</span></span>
<span data-ttu-id="70a69-176">In Windows universale, aprire MainPage.xaml.cs e quindi implementare il metodo `Search`.</span><span class="sxs-lookup"><span data-stu-id="70a69-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="70a69-177">Quest'ultimo si serve di un metodo helper in un progetto condiviso per aggiornare l'interfaccia utente in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="70a69-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="70a69-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70a69-178">What's next</span></span>
<span data-ttu-id="70a69-179">È stata compilata un'app Xamarin funzionante che può autenticare gli utenti e chiamare in modo sicuro le API Web usando OAuth 2.0 in cinque diverse piattaforme.</span><span class="sxs-lookup"><span data-stu-id="70a69-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="70a69-180">Se non è stato ancora popolato il tenant con degli utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="70a69-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="70a69-181">Eseguire l'app DirectorySearcher e accedere usando le credenziali di uno di questi utenti.</span><span class="sxs-lookup"><span data-stu-id="70a69-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="70a69-182">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="70a69-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="70a69-183">ADAL consente di incorporare facilmente nell'app funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="70a69-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="70a69-184">Esegue automaticamente le attività più complesse, ovvero gestione della cache, supporto del protocollo OAuth, visualizzazione all'utente di un'interfaccia utente di accesso e aggiornamento dei token scaduti.</span><span class="sxs-lookup"><span data-stu-id="70a69-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="70a69-185">È necessario conoscere una sola chiamata API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="70a69-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="70a69-186">Per riferimento, scaricare l'[esempio completato](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip), che non contiene i valori di configurazione immessi durante la procedura sopra indicata.</span><span class="sxs-lookup"><span data-stu-id="70a69-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="70a69-187">Ora è possibile passare ad altri scenari relativi alle identità.</span><span class="sxs-lookup"><span data-stu-id="70a69-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="70a69-188">Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="70a69-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
