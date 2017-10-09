---
title: versione 2.0 di Active Directory aaaAzure .NET Native App | Documenti Microsoft
description: Come toobuild un'applicazione nativa .NET che esegue l'accesso agli utenti con entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="f9b77-103">Aggiungere app per Windows Desktop Accedi tooa</span><span class="sxs-lookup"><span data-stu-id="f9b77-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="f9b77-104">Con l'endpoint di hello hello v 2.0 è possibile aggiungere rapidamente applicazioni desktop per l'autenticazione tooyour con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="f9b77-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="f9b77-105">È anche Abilita toosecurely l'app di comunicare con un back-end web api, nonché [hello Microsoft Graph](https://graph.microsoft.io) e alcuni di hello [Unified API di Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="f9b77-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="f9b77-106">Non tutte le caratteristiche e gli scenari di Azure Active Directory (AD) sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9b77-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="f9b77-107">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f9b77-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="f9b77-108">Per [app .NET native eseguite in un dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), Azure Active Directory fornisce hello libreria di autenticazione di Microsoft Identity o MSAL.</span><span class="sxs-lookup"><span data-stu-id="f9b77-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="f9b77-109">Unico scopo del MSAL vita è toomake è più facile per l'app tooget token per chiamare i servizi web.</span><span class="sxs-lookup"><span data-stu-id="f9b77-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="f9b77-110">la semplicità è, toodemonstrate qui creeremo un'app di elenco attività di WPF .NET che:</span><span class="sxs-lookup"><span data-stu-id="f9b77-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="f9b77-111">Segni di hello utente nel & ottiene accesso token usando hello [protocollo di autenticazione OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f9b77-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="f9b77-112">Chiama in modo sicuro un servizio Web To Do List di back-end, anch'esso protetto da OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9b77-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="f9b77-113">Utente di hello segni out.</span><span class="sxs-lookup"><span data-stu-id="f9b77-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="f9b77-114">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="f9b77-114">Download sample code</span></span>
<span data-ttu-id="f9b77-115">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f9b77-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="f9b77-116">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="f9b77-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="f9b77-117">app Hello completato è disponibile alla fine hello anche in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f9b77-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="f9b77-118">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="f9b77-118">Register an app</span></span>
<span data-ttu-id="f9b77-119">Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f9b77-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f9b77-120">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="f9b77-120">Make sure to:</span></span>

* <span data-ttu-id="f9b77-121">Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="f9b77-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="f9b77-122">Aggiungere hello **Mobile** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="f9b77-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="f9b77-123">Installare e configurare MSAL</span><span class="sxs-lookup"><span data-stu-id="f9b77-123">Install & Configure MSAL</span></span>
<span data-ttu-id="f9b77-124">A questo punto si ha un'app registrata in Microsoft ed è possibile installare MSAL e trascrivere il codice correlato all'identità.</span><span class="sxs-lookup"><span data-stu-id="f9b77-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="f9b77-125">Per l'endpoint MSAL toobe toocommunicate in grado di hello v 2.0, è necessario tooprovide con alcune informazioni la registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9b77-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="f9b77-126">Iniziare aggiungendo MSAL toohello TodoListClient progetto utilizzando la Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="f9b77-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="f9b77-127">Nel progetto TodoListClient hello aprire `app.config`.</span><span class="sxs-lookup"><span data-stu-id="f9b77-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="f9b77-128">Sostituire i valori hello elementi hello in hello `<appSettings>` hello tooreflect sezione valori di input nel portale di registrazione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f9b77-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="f9b77-129">Il codice farà riferimento a questi valori ogni volta che userà MSAL.</span><span class="sxs-lookup"><span data-stu-id="f9b77-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="f9b77-130">Hello `ida:ClientId` è hello **Id applicazione** dell'app dal portale hello copiato.</span><span class="sxs-lookup"><span data-stu-id="f9b77-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="f9b77-131">Nel progetto hello servizio elenco attività, aprire `web.config` nella directory radice del progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9b77-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="f9b77-132">Sostituire hello `ida:Audience` stesso valore con hello **Id applicazione** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="f9b77-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="f9b77-133">Utilizzare i token tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="f9b77-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="f9b77-134">Hello principio fondamentale dietro MSAL è che ogni volta che è necessario un token di accesso dell'app, è sufficiente chiamare `app.AcquireToken(...)`, e MSAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="f9b77-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="f9b77-135">In hello `TodoListClient` progetto, aprire `MainWindow.xaml.cs` e individuare hello `OnInitialized(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="f9b77-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="f9b77-136">innanzitutto Hello è tooinitialize dell'app `PublicClientApplication` -classe del MSAL principale che rappresenta le applicazioni native.</span><span class="sxs-lookup"><span data-stu-id="f9b77-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="f9b77-137">Si tratta in cui si passa MSAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.</span><span class="sxs-lookup"><span data-stu-id="f9b77-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="f9b77-138">All'avvio dell'applicazione hello, si desidera toocheck e vedere se l'utente hello è già connesso in app hello.</span><span class="sxs-lookup"><span data-stu-id="f9b77-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="f9b77-139">Tuttavia, non vogliamo tooinvoke un'interfaccia utente Accedi ancora - ci accerteremo utente hello fare clic su "Accedi" toodo così.</span><span class="sxs-lookup"><span data-stu-id="f9b77-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="f9b77-140">Anche in hello `OnInitialized(...)` metodo:</span><span class="sxs-lookup"><span data-stu-id="f9b77-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="f9b77-141">Se hello utente non è registrato e si fa clic pulsante "Accedi" hello, si desidera tooinvoke un account di accesso dell'interfaccia utente di utente hello immettere le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="f9b77-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="f9b77-142">Implementare il gestore del pulsante hello Accedi:</span><span class="sxs-lookup"><span data-stu-id="f9b77-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="f9b77-143">Se hello correttamente accesso dell'utente, MSAL riceverà e memorizzare nella cache un token per l'utente, ed è possibile procedere hello toocall `GetTodoList()` metodo con confidenza.</span><span class="sxs-lookup"><span data-stu-id="f9b77-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="f9b77-144">Tutto ciò che ha lasciato tooget attività dell'utente è hello tooimplement `GetTodoList()` metodo.</span><span class="sxs-lookup"><span data-stu-id="f9b77-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="f9b77-145">Esegui</span><span class="sxs-lookup"><span data-stu-id="f9b77-145">Run</span></span>
<span data-ttu-id="f9b77-146">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f9b77-146">Congratulations!</span></span> <span data-ttu-id="f9b77-147">Ora disponibile un'applicazione WPF .NET con gli utenti di hello possibilità tooauthenticate funzionante & in modo sicuro chiamare le API Web mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9b77-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="f9b77-148">Eseguire entrambi i progetti e accedere con un account Microsoft personale oppure con un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="f9b77-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="f9b77-149">Aggiungere l'elenco di attività dell'utente toothat di attività.</span><span class="sxs-lookup"><span data-stu-id="f9b77-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="f9b77-150">Disconnettersi e accedere di nuovo come un altro utente tooview proprio elenco di attività da eseguire.</span><span class="sxs-lookup"><span data-stu-id="f9b77-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="f9b77-151">Chiudere l'applicazione hello ed eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f9b77-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="f9b77-152">Si noti come hello sessione rimane invariata, perché l'applicazione hello memorizza nella cache i token in un file locale.</span><span class="sxs-lookup"><span data-stu-id="f9b77-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="f9b77-153">MSAL rende facile tooincorporate funzionalità comuni delle identità nell'app, tramite gli account personali e aziendali.</span><span class="sxs-lookup"><span data-stu-id="f9b77-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="f9b77-154">Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f9b77-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="f9b77-155">Ciò che occorre tooknow è una singola chiamata API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="f9b77-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="f9b77-156">Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="f9b77-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="f9b77-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9b77-157">Next steps</span></span>
<span data-ttu-id="f9b77-158">Ora è possibile passare ad argomenti più avanzati.</span><span class="sxs-lookup"><span data-stu-id="f9b77-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="f9b77-159">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="f9b77-159">You may want tootry:</span></span>

* [<span data-ttu-id="f9b77-160">Protezione hello TodoListService Web API con endpoint v 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="f9b77-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="f9b77-161">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="f9b77-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="f9b77-162">Guida per sviluppatori v 2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="f9b77-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="f9b77-163">StackOverflow: tag "msal" &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="f9b77-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f9b77-164">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="f9b77-164">Get security updates for our products</span></span>
<span data-ttu-id="f9b77-165">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="f9b77-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

