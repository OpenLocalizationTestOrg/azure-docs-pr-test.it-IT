---
title: Introduzione a Windows Store per Azure AD | Microsoft Docs
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
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="2d43d-103">Integrare Azure AD con le app di Windows Store</span><span class="sxs-lookup"><span data-stu-id="2d43d-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="2d43d-104">I progetti di Windows Store 8.1 e della versione precedente non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2d43d-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="2d43d-105">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="2d43d-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="2d43d-106">Quando si sviluppano app per Windows Store, Azure Active Directory (Azure AD) semplifica e facilita l'autenticazione degli utenti con gli account Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d43d-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="2d43d-107">Grazie all'integrazione con Azure AD, un'app può usare in modo sicuro qualsiasi API Web protetta da Azure AD, quali ad esempio le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d43d-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="2d43d-108">Per le app desktop di Windows Store che devono accedere a risorse protette, Azure AD offre Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="2d43d-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="2d43d-109">L'unica funzione di ADAL è di semplificare l'acquisizione dei token di accesso da parte delle app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="2d43d-110">Per far capire quanto sia semplice, questo articolo illustra come compilare un'app di Windows Store denominata DirectorySearcher che:</span><span class="sxs-lookup"><span data-stu-id="2d43d-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="2d43d-111">Ottiene i token di accesso per chiamare l'API Graph di Azure AD con il [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d43d-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="2d43d-112">Cerca in una directory gli utenti con un determinato nome dell'entità utente (UPN).</span><span class="sxs-lookup"><span data-stu-id="2d43d-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="2d43d-113">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="2d43d-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2d43d-114">Before you get started</span></span>
* <span data-ttu-id="2d43d-115">Scaricare la [struttura di progetto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip) oppure l'[esempio completato](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="2d43d-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="2d43d-116">Ognuno è una soluzione di Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2d43d-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="2d43d-117">È necessario disporre anche di un tenant di Azure AD in cui creare gli utenti e registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="2d43d-118">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2d43d-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="2d43d-119">Quando si è pronti, attenersi alle procedure descritte nelle tre sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="2d43d-120">Passaggio 1. Registrare l'app DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="2d43d-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="2d43d-121">Per consentire all'app di ottenere i token, sarà prima necessario registrarla nel tenant di Azure AD e concederle l'autorizzazione per accedere all'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d43d-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="2d43d-122">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="2d43d-122">Here's how:</span></span>

1. <span data-ttu-id="2d43d-123">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d43d-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2d43d-124">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="2d43d-124">On the top bar, click your account.</span></span> <span data-ttu-id="2d43d-125">Nell'elenco **Directory** selezionare quindi il tenant di Active Directory in cui si vuole registrare l'app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="2d43d-126">Fare clic su **Altri servizi** nel riquadro a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="2d43d-127">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="2d43d-128">Seguire le istruzioni per creare un'**Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="2d43d-129">Il **nome** descrive l'app agli utenti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="2d43d-130">L'**URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD usa per restituire le risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="2d43d-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="2d43d-131">Immettere per ora un valore segnaposto, ad esempio **http://DirectorySearcher**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="2d43d-132">Si sostituirà il valore in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2d43d-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="2d43d-133">Dopo aver completato la registrazione, Azure AD assegna automaticamente all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="2d43d-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="2d43d-134">Copiare il valore nella scheda **Applicazione**, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2d43d-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="2d43d-135">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="2d43d-136">Per l'app di **Azure Active Directory**, selezionare **Microsoft Graph** come API.</span><span class="sxs-lookup"><span data-stu-id="2d43d-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="2d43d-137">In **Autorizzazioni delegate** aggiungere l'autorizzazione **Accesso alla directory come utente connesso**.</span><span class="sxs-lookup"><span data-stu-id="2d43d-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="2d43d-138">Ciò consente all'app di eseguire query nell'API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="2d43d-139">Passaggio 2. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="2d43d-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="2d43d-140">Ora che si dispone di un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="2d43d-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="2d43d-141">Per abilitare ADAL alla comunicazione con Azure AD, fornire alcune informazioni sulla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="2d43d-142">Aggiungere ADAL al progetto DirectorySearcher usando la Console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="2d43d-143">Nel progetto DirectorySearcher aprire MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="2d43d-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="2d43d-144">Sostituire i valori nell'area **Config Values** con i valori immessi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d43d-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="2d43d-145">Il codice fa riferimento a questi valori ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="2d43d-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="2d43d-146">Il *tenant* è il dominio del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="2d43d-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="2d43d-147">Il *clientId* è l'ID client dell'app. Lo si copia dal portale.</span><span class="sxs-lookup"><span data-stu-id="2d43d-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="2d43d-148">A questo punto è necessario individuare l'URI di callback per l'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="2d43d-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="2d43d-149">Impostare un punto di interruzione in questa riga del metodo `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="2d43d-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="2d43d-150">Compilare la soluzione assicurandosi che vengano ripristinati tutti i riferimenti del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2d43d-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="2d43d-151">Se mancano pacchetti, aprire Gestione pacchetti NuGet e ripristinarli.</span><span class="sxs-lookup"><span data-stu-id="2d43d-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="2d43d-152">Eseguire l'app e prendere nota del valore di `redirectUri` quando viene raggiunto il punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="2d43d-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="2d43d-153">Il valore dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2d43d-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="2d43d-154">Tornare nella scheda **Impostazioni** dell'app nel portale di Azure e sostituire il valore di **RedirectUri** con questo valore.</span><span class="sxs-lookup"><span data-stu-id="2d43d-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="2d43d-155">Passaggio 3. Usare ADAL per ottenere i token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d43d-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="2d43d-156">Il principio alla base di ADAL è che ogni volta che l'app ha bisogno di un token di accesso, deve solo chiamare `authContext.AcquireToken(…)` e ADAL fa il resto.</span><span class="sxs-lookup"><span data-stu-id="2d43d-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="2d43d-157">Inizializzare la classe `AuthenticationContext` dell'app, che è la classe principale di ADAL.</span><span class="sxs-lookup"><span data-stu-id="2d43d-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="2d43d-158">Questa azione passa ad ADAL le coordinate necessarie per comunicare con Azure AD e gli indica come memorizzare i token nella cache.</span><span class="sxs-lookup"><span data-stu-id="2d43d-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="2d43d-159">Individuare il metodo `Search(...)`, che viene richiamato quando l'utente sceglie il pulsante **Cerca** nell'interfaccia utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="2d43d-160">Questo metodo invia una richiesta GET all'API Graph di Azure AD per eseguire una query sugli utenti il cui UPN inizia con il termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="2d43d-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="2d43d-161">Per eseguire una query nell'API Graph, includere un token di accesso nell'intestazione **Authorization** della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2d43d-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="2d43d-162">È qui che entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="2d43d-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="2d43d-163">Quando l'app richiede un token mediante la chiamata a `AcquireTokenAsync(...)`, ADAL tenta di restituire un token senza chiedere le credenziali all'utente.</span><span class="sxs-lookup"><span data-stu-id="2d43d-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="2d43d-164">Se ADAL determina che l'utente deve eseguire l'accesso per ottenere un token, visualizza una finestra di dialogo di accesso, raccoglie le credenziali dell'utente e restituisce un token al termine dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2d43d-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="2d43d-165">Se per qualsiasi motivo ADAL non può restituire un token, lo stato di *AuthenticationResult* sarà un errore.</span><span class="sxs-lookup"><span data-stu-id="2d43d-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="2d43d-166">È ora di usare il token di accesso appena acquisito.</span><span class="sxs-lookup"><span data-stu-id="2d43d-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="2d43d-167">Nel metodo `Search(...)` associare il token alla richiesta get dell'API Graph nell'intestazione **Authorization**:</span><span class="sxs-lookup"><span data-stu-id="2d43d-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="2d43d-168">È possibile usare l'oggetto `AuthenticationResult` anche per visualizzare informazioni sull'utente nell'app, ad esempio l'ID dell'utente:</span><span class="sxs-lookup"><span data-stu-id="2d43d-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="2d43d-169">È inoltre possibile usare ADAL per disconnettere gli utenti dall'app.</span><span class="sxs-lookup"><span data-stu-id="2d43d-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="2d43d-170">Quando l'utente fa clic sul pulsante **Sign Out** (Disconnetti), è opportuno assicurarsi che la chiamata successiva a `AcquireTokenAsync(...)` mostri una vista di accesso.</span><span class="sxs-lookup"><span data-stu-id="2d43d-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="2d43d-171">Con ADAL, questa azione è facile quanto cancellare la cache dei token:</span><span class="sxs-lookup"><span data-stu-id="2d43d-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="2d43d-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d43d-172">What's next</span></span>
<span data-ttu-id="2d43d-173">È stata compilata un'app di Windows Store in grado di autenticare gli utenti, di chiamare in modo sicuro le API Web usando OAuth 2.0 e di ottenere le informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="2d43d-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="2d43d-174">Se non è stato ancora popolato il tenant con degli utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="2d43d-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="2d43d-175">Eseguire l'app DirectorySearcher e accedere usando le credenziali di uno di questi utenti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="2d43d-176">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="2d43d-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="2d43d-177">Chiudere l'app e rieseguirla.</span><span class="sxs-lookup"><span data-stu-id="2d43d-177">Close the app, and rerun it.</span></span> <span data-ttu-id="2d43d-178">Si noti che la sessione dell'utente non è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="2d43d-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="2d43d-179">Disconnettersi facendo clic con il pulsante destro del mouse per visualizzare la barra in basso e quindi accedere nuovamente con le credenziali di un altro utente.</span><span class="sxs-lookup"><span data-stu-id="2d43d-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="2d43d-180">ADAL consente di incorporare facilmente nell'app tutte queste funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="2d43d-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="2d43d-181">Esegue automaticamente le attività più complesse: gestione della cache, supporto del protocollo OAuth, visualizzazione all'utente di un'interfaccia utente di accesso, aggiornamento dei token scaduti.</span><span class="sxs-lookup"><span data-stu-id="2d43d-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="2d43d-182">È necessario conoscere una sola chiamata API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="2d43d-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="2d43d-183">Per riferimento, scaricare l'[esempio completato](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip), che non contiene i valori di configurazione immessi durante la procedura sopra indicata.</span><span class="sxs-lookup"><span data-stu-id="2d43d-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="2d43d-184">Ora è possibile passare ad altri scenari relativi alle identità.</span><span class="sxs-lookup"><span data-stu-id="2d43d-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="2d43d-185">Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2d43d-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
