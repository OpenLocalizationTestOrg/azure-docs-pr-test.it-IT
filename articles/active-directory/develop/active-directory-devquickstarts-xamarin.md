---
title: aaaAzure AD Xamarin introduzione | Documenti Microsoft
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="33abe-103">Integrare Azure AD in app Xamarin</span><span class="sxs-lookup"><span data-stu-id="33abe-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="33abe-104">Xamarin consente di scrivere app per dispositivi mobili in C# che possono essere eseguite in iOS, Android e Windows, in dispositivi mobili e PC.</span><span class="sxs-lookup"><span data-stu-id="33abe-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="33abe-105">Se si sta creando un'app con Xamarin, Azure Active Directory (Azure AD) consente agli utenti di tooauthenticate semplice con gli account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33abe-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="33abe-106">applicazione Hello utilizzabile anche in modo sicuro da qualsiasi API web protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.</span><span class="sxs-lookup"><span data-stu-id="33abe-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="33abe-107">Per le app Xamarin che necessitano di risorse tooaccess protetto da Azure AD fornisce hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="33abe-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="33abe-108">Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget app.</span><span class="sxs-lookup"><span data-stu-id="33abe-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="33abe-109">toodemonstrate facilmente, questo articolo viene illustrato come le app DirectorySearcher toobuild che:</span><span class="sxs-lookup"><span data-stu-id="33abe-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="33abe-110">Viene eseguita in iOS, Android, Windows Desktop, Windows Phone e Windows Store.</span><span class="sxs-lookup"><span data-stu-id="33abe-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="33abe-111">Utilizzare una singola classe portabile libreria (PCL) tooauthenticate utenti e di ottenere token per hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="33abe-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="33abe-112">Cerca in una directory gli utenti con un determinato UPN.</span><span class="sxs-lookup"><span data-stu-id="33abe-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="33abe-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="33abe-113">Before you get started</span></span>
* <span data-ttu-id="33abe-114">Scaricare hello [scheletro di progetto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="33abe-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="33abe-115">Ognuno è una soluzione di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="33abe-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="33abe-116">È inoltre necessario un tenant di Azure Active Directory in cui gli utenti toocreate e registra hello app.</span><span class="sxs-lookup"><span data-stu-id="33abe-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="33abe-117">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="33abe-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="33abe-118">Quando si è pronti, seguire le procedure di hello in hello quattro sezioni.</span><span class="sxs-lookup"><span data-stu-id="33abe-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="33abe-119">Passaggio 1: Configurare l'ambiente di sviluppo Xamarin</span><span class="sxs-lookup"><span data-stu-id="33abe-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="33abe-120">Dal momento che questa esercitazione include progetti per iOS, Android e Windows, sono necessari sia Visual Studio che Xamarin.</span><span class="sxs-lookup"><span data-stu-id="33abe-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="33abe-121">ambiente necessarie toocreate hello, il processo di completamento hello in [impostare backup e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) su MSDN.</span><span class="sxs-lookup"><span data-stu-id="33abe-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="33abe-122">istruzioni di Hello includono materiale che è possibile esaminare informazioni su Xamarin toolearn durante l'attesa per hello installazioni toobe completato.</span><span class="sxs-lookup"><span data-stu-id="33abe-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="33abe-123">Dopo aver completato l'installazione di hello, aprire la soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33abe-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="33abe-124">Sono presenti sei progetti: cinque progetti specifici delle piattaforme e una libreria di classi portabile, DirectorySearcher.cs, che verrà condivisa tra tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="33abe-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="33abe-125">Passaggio 2: Registrare hello DirectorySearcher app</span><span class="sxs-lookup"><span data-stu-id="33abe-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="33abe-126">i token tooenable hello app tooget, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="33abe-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="33abe-127">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="33abe-127">Here's how:</span></span>

1. <span data-ttu-id="33abe-128">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33abe-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="33abe-129">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="33abe-129">On hello top bar, click your account.</span></span> <span data-ttu-id="33abe-130">Quindi, in hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="33abe-131">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33abe-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="33abe-132">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33abe-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="33abe-133">toocreate un nuovo **applicazione Client nativa**, seguire le istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="33abe-134">**Nome** descrive toousers app hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="33abe-135">**URI di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte.</span><span class="sxs-lookup"><span data-stu-id="33abe-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="33abe-136">Immettere un valore, ad esempio http://DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="33abe-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="33abe-137">Dopo aver completato la registrazione, Azure AD le assegna app hello un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="33abe-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="33abe-138">Copiare il valore di hello hello **applicazione** scheda, perché sarà necessaria successivamente.</span><span class="sxs-lookup"><span data-stu-id="33abe-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="33abe-139">In hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33abe-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="33abe-140">Selezionare **Microsoft Graph** come hello API.</span><span class="sxs-lookup"><span data-stu-id="33abe-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="33abe-141">In **autorizzazioni delegate**, aggiungere hello **lettura dati Directory** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="33abe-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="33abe-142">Questa azione Abilita hello tooquery hello app API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="33abe-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="33abe-143">Passaggio 3: Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="33abe-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="33abe-144">Ora che si dispone di un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="33abe-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="33abe-145">tooenable toocommunicate ADAL con Azure AD, assegnargli alcune informazioni di registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="33abe-146">Aggiungere il progetto di DirectorySearcher toohello ADAL tramite la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

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

    <span data-ttu-id="33abe-147">Si noti che i due riferimenti alla libreria vengono aggiunti progetto tooeach: hello PCL parte ADAL e una parte specifica della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="33abe-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="33abe-148">Nel progetto DirectorySearcherLib hello aprire DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="33abe-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="33abe-149">Sostituire i valori dei membri di classe hello con valori di hello immesso nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="33abe-150">Il codice si riferisce valori toothese ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="33abe-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="33abe-151">Hello *tenant* hello dominio del tenant di Azure Active Directory (ad esempio, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="33abe-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="33abe-152">Hello *clientId* hello client ID dell'applicazione hello, che copiato dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="33abe-153">Hello *returnUri* è hello reindirizzamento URI immesso nel portale di hello (ad esempio, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="33abe-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="33abe-154">Passaggio 4: I token usare ADAL tooget da Azure AD</span><span class="sxs-lookup"><span data-stu-id="33abe-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="33abe-155">Quasi tutta la logica di autenticazione dell'applicazione hello si trova `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="33abe-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="33abe-156">Tutto ciò che è necessario nei progetti specifici della piattaforma hello è toopass toohello un parametro contestuali `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="33abe-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="33abe-157">Aprire DirectorySearcher.cs e quindi aggiungere un nuovo toohello parametro `SearchByAlias(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="33abe-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="33abe-158">`IPlatformParameters`è che l'autenticazione hello tooperform ADAL esigenze di oggetti parametro hello contestuali che incapsula hello specifico della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="33abe-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="33abe-159">Inizializzare `AuthenticationContext`, ovvero hello classe principale della libreria ADAL.</span><span class="sxs-lookup"><span data-stu-id="33abe-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="33abe-160">Hello ADAL di passaggi di questa azione è coordinate toocommunicate esigenze con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33abe-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="33abe-161">Chiamare `AcquireTokenAsync(...)`, che accetta hello `IPlatformParameters` dell'oggetto e richiama il flusso di autenticazione hello che è necessario tooreturn un'app toohello token.</span><span class="sxs-lookup"><span data-stu-id="33abe-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

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

    <span data-ttu-id="33abe-162">`AcquireTokenAsync(...)`primo tentativi tooreturn un token per hello richiesto risorsa (Buongiorno API Graph in questo caso) senza chiedere conferma tooenter agli utenti le proprie credenziali (tramite la memorizzazione nella cache o l'aggiornamento di un token precedente).</span><span class="sxs-lookup"><span data-stu-id="33abe-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="33abe-163">Se necessario, viene prima di acquisire token richiesto hello utenti hello Azure AD nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="33abe-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="33abe-164">Collegare una richiesta all'API Graph toohello token accesso hello in hello **autorizzazione** intestazione:</span><span class="sxs-lookup"><span data-stu-id="33abe-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="33abe-165">Questo è tutto per hello `DirectorySearcher` codice relative alle identità PCL e hello dell'app.</span><span class="sxs-lookup"><span data-stu-id="33abe-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="33abe-166">È comunque toocall hello `SearchByAlias(...)` metodo nelle visualizzazioni di ciascuna piattaforma e, se necessario, tooadd codice per la gestione corretta di hello del ciclo di vita dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="33abe-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="33abe-167">Android</span><span class="sxs-lookup"><span data-stu-id="33abe-167">Android</span></span>
1. <span data-ttu-id="33abe-168">In Mainactivity, aggiungere una chiamata troppo`SearchByAlias(...)` nel pulsante hello gestore click:</span><span class="sxs-lookup"><span data-stu-id="33abe-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="33abe-169">Eseguire l'override di hello `OnActivityResult` del ciclo di vita metodo tooforward alcuna autenticazione reindirizza toohello indietro di metodo appropriato.</span><span class="sxs-lookup"><span data-stu-id="33abe-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="33abe-170">ADAL fornisce un apposito metodo helper in Android:</span><span class="sxs-lookup"><span data-stu-id="33abe-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="33abe-171">Desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="33abe-171">Windows Desktop</span></span>
<span data-ttu-id="33abe-172">In MainWindow.xaml.cs, effettuare una chiamata troppo`SearchByAlias(...)` passando un `WindowInteropHelper` in desktop hello `PlatformParameters` oggetto:</span><span class="sxs-lookup"><span data-stu-id="33abe-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="33abe-173">iOS</span><span class="sxs-lookup"><span data-stu-id="33abe-173">iOS</span></span>
<span data-ttu-id="33abe-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` oggetto assume un toohello riferimento View Controller:</span><span class="sxs-lookup"><span data-stu-id="33abe-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="33abe-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="33abe-175">Windows Universal</span></span>
<span data-ttu-id="33abe-176">In Windows universale, Apri il file MainPage.xaml.cs e quindi implementare hello `Search` metodo.</span><span class="sxs-lookup"><span data-stu-id="33abe-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="33abe-177">Questo metodo Usa un metodo di supporto in un progetto condiviso tooupdate dell'interfaccia utente, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="33abe-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="33abe-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33abe-178">What's next</span></span>
<span data-ttu-id="33abe-179">È stata compilata un'app Xamarin funzionante che può autenticare gli utenti e chiamare in modo sicuro le API Web usando OAuth 2.0 in cinque diverse piattaforme.</span><span class="sxs-lookup"><span data-stu-id="33abe-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="33abe-180">Se non sono stati già popolato il tenant con gli utenti, è pertanto toodo ora hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="33abe-181">Eseguire l'app DirectorySearcher e quindi accedere con uno degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="33abe-182">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="33abe-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="33abe-183">ADAL lo rende facile tooincorporate funzionalità comuni delle identità applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="33abe-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="33abe-184">Si occupa di tutto il lavoro dirty hello, quali la gestione della cache, supporto del protocollo OAuth, presentate utente hello con interfaccia utente, un account di accesso e aggiornamento scaduto token.</span><span class="sxs-lookup"><span data-stu-id="33abe-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="33abe-185">È necessario tooknow solo una singola API chiamata, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="33abe-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="33abe-186">Per riferimento, scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (senza i valori di configurazione).</span><span class="sxs-lookup"><span data-stu-id="33abe-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="33abe-187">È possibile procedere in scenari con identità tooadditional.</span><span class="sxs-lookup"><span data-stu-id="33abe-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="33abe-188">Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="33abe-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
