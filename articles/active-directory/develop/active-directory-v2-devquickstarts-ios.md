---
title: Aggiungere informazioni di accesso a un'applicazione iOS usando l'endpoint 2.0 di Azure AD | Documentazione Microsoft
description: Come compilare un'app per iOS che consente agli utenti di accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione usando librerie di terze parti.
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="433fe-103">Aggiungere informazioni di accesso a un'app iOS usando una libreria di terze parti con l'API Graph mediante l'endpoint v2.0</span><span class="sxs-lookup"><span data-stu-id="433fe-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="433fe-104">La piattaforma delle identità Microsoft usa standard aperti, ad esempio OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="433fe-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="433fe-105">Gli sviluppatori possono usare qualsiasi libreria che desiderano integrare ai servizi.</span><span class="sxs-lookup"><span data-stu-id="433fe-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="433fe-106">Per aiutare gli sviluppatori a usare la piattaforma con altre librerie, sono state scritte alcune procedure dettagliate come questa, che illustrano come configurare le librerie di terze parti per connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="433fe-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="433fe-107">La maggior parte delle librerie che implementano [la specifica OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) possono connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="433fe-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="433fe-108">Con l'applicazione creata in questa procedura dettagliata, gli utenti possono accedere alla propria organizzazione e cercare altro all'interno dell'organizzazione tramite l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="433fe-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="433fe-109">Se non si ha familiarità con OAuth2 o OpenID Connect, gran parte di questo esempio risulterà poco chiara.</span><span class="sxs-lookup"><span data-stu-id="433fe-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="433fe-110">Per informazioni, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="433fe-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="433fe-111">Per alcune funzionalità della piattaforma che trovano espressione negli standard OAuth2 o OpenID Connect, ad esempio l'accesso condizionale e la gestione criteri di Intune, è necessario usare le librerie di identità open source di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="433fe-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="433fe-112">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="433fe-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="433fe-113">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="433fe-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="433fe-114">Scaricare il codice da GitHub</span><span class="sxs-lookup"><span data-stu-id="433fe-114">Download code from GitHub</span></span>
<span data-ttu-id="433fe-115">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="433fe-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="433fe-116">Per seguire la procedura è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="433fe-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="433fe-117">È anche possibile scaricare l'esempio e iniziare subito:</span><span class="sxs-lookup"><span data-stu-id="433fe-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="433fe-118">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="433fe-118">Register an app</span></span>
<span data-ttu-id="433fe-119">Creare una nuova app nel [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) oppure seguire la procedura dettagliata descritta in [Come registrare un'app con l'endpoint v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="433fe-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="433fe-120">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="433fe-120">Make sure to:</span></span>

* <span data-ttu-id="433fe-121">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="433fe-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="433fe-122">Aggiungere la piattaforma **Mobile** per l'app.</span><span class="sxs-lookup"><span data-stu-id="433fe-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="433fe-123">Copiare l' **URI di reindirizzamento** dal portale.</span><span class="sxs-lookup"><span data-stu-id="433fe-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="433fe-124">È necessario usare il valore predefinito `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="433fe-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="433fe-125">Scaricare la libreria di terze parti NXOAuth2 e creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="433fe-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="433fe-126">Per questa procedura dettagliata verrà usato OAuth2Client di GitHub, una libreria OAuth2 per Mac OS X e iOS (Cocoa e Cocoa Touch).</span><span class="sxs-lookup"><span data-stu-id="433fe-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="433fe-127">Questa libreria si basa sulla bozza 10 della specifica OAuth2.</span><span class="sxs-lookup"><span data-stu-id="433fe-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="433fe-128">Questa libreria implementa il profilo dell'applicazione nativa e supporta l'endpoint di autorizzazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="433fe-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="433fe-129">Ecco tutto ciò che serve per l'integrazione con la piattaforma delle identità di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="433fe-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="433fe-130">Aggiungere la libreria al progetto con CocoaPods</span><span class="sxs-lookup"><span data-stu-id="433fe-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="433fe-131">CocoaPods è un gestore delle dipendenze per i progetti Xcode.</span><span class="sxs-lookup"><span data-stu-id="433fe-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="433fe-132">Gestisce automaticamente i passaggi di installazione precedenti.</span><span class="sxs-lookup"><span data-stu-id="433fe-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="433fe-133">Aggiungere il codice seguente al podfile:</span><span class="sxs-lookup"><span data-stu-id="433fe-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="433fe-134">Caricare il podfile usando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="433fe-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="433fe-135">Verrà creata una nuova area di lavoro Xcode da caricare.</span><span class="sxs-lookup"><span data-stu-id="433fe-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="433fe-136">Esplorare la struttura del progetto</span><span class="sxs-lookup"><span data-stu-id="433fe-136">Explore the structure of the project</span></span>
<span data-ttu-id="433fe-137">Nello scheletro è configurata la struttura seguente per il progetto:</span><span class="sxs-lookup"><span data-stu-id="433fe-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="433fe-138">Una visualizzazione master con una ricerca UPN</span><span class="sxs-lookup"><span data-stu-id="433fe-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="433fe-139">Una visualizzazione dettagli per i dati sull'utente selezionato</span><span class="sxs-lookup"><span data-stu-id="433fe-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="433fe-140">Una visualizzazione di accesso che consente a un utente di accedere all'app per eseguire query al grafico</span><span class="sxs-lookup"><span data-stu-id="433fe-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="433fe-141">Si passerà a diversi file nella struttura per aggiungere l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="433fe-142">Altre parti del codice, ad esempio il codice visivo, non sono pertinenti all'identità e vengono fornite automaticamente.</span><span class="sxs-lookup"><span data-stu-id="433fe-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="433fe-143">Configurare il file settings.plst nella libreria</span><span class="sxs-lookup"><span data-stu-id="433fe-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="433fe-144">Nel progetto QuickStart, aprire il file `settings.plist` .</span><span class="sxs-lookup"><span data-stu-id="433fe-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="433fe-145">Sostituire i valori degli elementi nella sezione in modo che corrispondano ai valori usati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="433fe-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="433fe-146">Il codice farà riferimento a questi valori ogni volta che viene usata la libreria di autenticazione di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="433fe-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="433fe-147">`clientId` è l'ID client dell'applicazione copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="433fe-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="433fe-148">`redirectUri` è l'URL di reindirizzamento fornito dal portale.</span><span class="sxs-lookup"><span data-stu-id="433fe-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="433fe-149">Configurare la libreria NXOAuth2Client in LoginViewController</span><span class="sxs-lookup"><span data-stu-id="433fe-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="433fe-150">Per configurare la libreria NXOAuth2Client, sono necessari alcuni valori.</span><span class="sxs-lookup"><span data-stu-id="433fe-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="433fe-151">Dopo avere completato questa attività, è possibile usare il token acquisito per le chiamate all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="433fe-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="433fe-152">Poiché `LoginView` verrà chiamato ogni volta che è necessario eseguire l'autenticazione, è opportuno inserire i valori di configurazione nel file.</span><span class="sxs-lookup"><span data-stu-id="433fe-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="433fe-153">Aggiungere alcuni valori al file `LoginViewController.m` per impostare il contesto per l'autenticazione e l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="433fe-154">I dettagli sui valori seguono il codice.</span><span class="sxs-lookup"><span data-stu-id="433fe-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="433fe-155">Esaminiamo i dettagli del codice.</span><span class="sxs-lookup"><span data-stu-id="433fe-155">Let's look at details about the code.</span></span>

<span data-ttu-id="433fe-156">La prima stringa è per `scopes`.</span><span class="sxs-lookup"><span data-stu-id="433fe-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="433fe-157">Il valore `User.Read` consente di leggere il profilo di base dell'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="433fe-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="433fe-158">Per altre informazioni su tutti gli ambiti disponibili, vedere [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes)(Ambiti di autorizzazione di Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="433fe-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="433fe-159">Per `authURL`, `loginURL`, `bhh`, `tokenURL` è consigliabile usare i valori specificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="433fe-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="433fe-160">Se si usano le librerie di identità di Microsoft Azure open source, verrà eseguito il pull automatico di questi dati usando gli endpoint dei metadati.</span><span class="sxs-lookup"><span data-stu-id="433fe-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="433fe-161">L'estrazione di questi valori è stata eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="433fe-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="433fe-162">Il valore `keychain` è il contenitore che la libreria NXOAuth2Client userà per creare un portachiavi in cui archiviare i token.</span><span class="sxs-lookup"><span data-stu-id="433fe-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="433fe-163">Per ottenere l'accesso Single Sign-On SSO in più app, è possibile specificare lo stesso portachiavi in ogni applicazione, oltre a richiedere l'uso di tale portachiavi nei diritti XCode.</span><span class="sxs-lookup"><span data-stu-id="433fe-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="433fe-164">Questa procedura è illustrata nella documentazione di Apple.</span><span class="sxs-lookup"><span data-stu-id="433fe-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="433fe-165">Gli altri valori sono necessari per usare la libreria e creare automaticamente le posizioni per inserire i valori nel contesto.</span><span class="sxs-lookup"><span data-stu-id="433fe-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="433fe-166">Creare una cache di URL</span><span class="sxs-lookup"><span data-stu-id="433fe-166">Create a URL cache</span></span>
<span data-ttu-id="433fe-167">All'interno di `(void)viewDidLoad()`, che viene sempre chiamato dopo il caricamento della visualizzazione, il codice seguente prepara una cache per l'uso.</span><span class="sxs-lookup"><span data-stu-id="433fe-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="433fe-168">Aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="433fe-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="433fe-169">Creare una visualizzazione Web per l'accesso</span><span class="sxs-lookup"><span data-stu-id="433fe-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="433fe-170">Una visualizzazione Web consente di chiedere all'utente altri fattori, ad esempio un SMS (se configurato), o di restituire messaggi di errore all'utente.</span><span class="sxs-lookup"><span data-stu-id="433fe-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="433fe-171">Ora verrà configurata la visualizzazione Web e in seguito verrà scritto il codice per gestire i callback che si verificheranno nella visualizzazione Web dal servizio di gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="433fe-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="433fe-172">Eseguire l'override dei metodi WebView per gestire l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="433fe-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="433fe-173">Per indicare alla visualizzazione Web cosa accade quando un utente deve eseguire l'accesso come illustrato in precedenza, è possibile incollare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="433fe-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="433fe-174">Scrivere il codice per gestire il risultato della richiesta OAuth2.</span><span class="sxs-lookup"><span data-stu-id="433fe-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="433fe-175">Il codice seguente gestirà l'URL di reindirizzamento restituito dalla visualizzazione Web.</span><span class="sxs-lookup"><span data-stu-id="433fe-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="433fe-176">Se l'autenticazione ha esito negativo, il codice ripete l'operazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="433fe-177">Nel frattempo la libreria visualizzerà l'errore che è possibile visualizzare nella console o gestire in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="433fe-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="433fe-178">Configurare il contesto OAuth (archivio di account chiamato)</span><span class="sxs-lookup"><span data-stu-id="433fe-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="433fe-179">Qui è possibile chiamare `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` nell'archivio account condiviso per ogni servizio a cui si desidera che l'applicazione abbia accesso.</span><span class="sxs-lookup"><span data-stu-id="433fe-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="433fe-180">Il tipo di account è una stringa che viene usata come identificatore per un determinato servizio.</span><span class="sxs-lookup"><span data-stu-id="433fe-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="433fe-181">Poiché si accede all'API Graph, il codice fa riferimento a esso come `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="433fe-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="433fe-182">Verrà quindi configurato un osservatore che segnalerà eventuali modifiche al token.</span><span class="sxs-lookup"><span data-stu-id="433fe-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="433fe-183">Dopo aver ottenuto il token, l'utente torna a `masterView`.</span><span class="sxs-lookup"><span data-stu-id="433fe-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="433fe-184">Configurare la visualizzazione master per cercare e visualizzare gli utenti dall'API Graph</span><span class="sxs-lookup"><span data-stu-id="433fe-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="433fe-185">Un'app Master-View-Controller (MVC) che visualizza i dati restituiti nella griglia non rientra nell'ambito di questa procedura dettagliata, ma online sono disponibili diverse esercitazioni che illustrano come compilarne una.</span><span class="sxs-lookup"><span data-stu-id="433fe-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="433fe-186">Tutto il codice è contenuto nel file dello scheletro.</span><span class="sxs-lookup"><span data-stu-id="433fe-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="433fe-187">È tuttavia necessario gestire alcuni elementi dell'applicazione MVC:</span><span class="sxs-lookup"><span data-stu-id="433fe-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="433fe-188">Rilevare quando un utente digita qualcosa nel campo di ricerca</span><span class="sxs-lookup"><span data-stu-id="433fe-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="433fe-189">Fornire un oggetto di dati a MasterView in modo che possa visualizzare i risultati nella griglia</span><span class="sxs-lookup"><span data-stu-id="433fe-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="433fe-190">Queste operazioni verranno eseguite sotto.</span><span class="sxs-lookup"><span data-stu-id="433fe-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="433fe-191">Aggiungere un controllo per verificare se si è connessi</span><span class="sxs-lookup"><span data-stu-id="433fe-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="433fe-192">Le funzionalità dell'applicazione sono limitate se l'utente non è connesso, quindi è opportuno controllare se è già presente un token nella cache.</span><span class="sxs-lookup"><span data-stu-id="433fe-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="433fe-193">Se il token non è presente, l'utente viene reindirizzato a LoginView per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="433fe-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="433fe-194">Se si richiama, il modo migliore per eseguire azioni quando viene caricata una visualizzazione consiste nell'usare il metodo `viewDidLoad()` fornito da Apple.</span><span class="sxs-lookup"><span data-stu-id="433fe-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="433fe-195">Aggiornare la visualizzazione tabella quando vengono ricevuti i dati</span><span class="sxs-lookup"><span data-stu-id="433fe-195">Update the Table View when data is received</span></span>
<span data-ttu-id="433fe-196">Quando l'API Graph restituisce i dati, è necessario visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="433fe-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="433fe-197">Per semplicità viene fornito tutto il codice necessario per aggiornare la tabella.</span><span class="sxs-lookup"><span data-stu-id="433fe-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="433fe-198">È sufficiente incollare i valori corretti nel codice boilerplate MVC.</span><span class="sxs-lookup"><span data-stu-id="433fe-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="433fe-199">Consente di chiamare l'API Graph quando qualcuno digita nel campo di ricerca</span><span class="sxs-lookup"><span data-stu-id="433fe-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="433fe-200">Quando un utente digita un testo di ricerca nella casella, è necessario inserirlo nell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="433fe-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="433fe-201">La classe `GraphAPICaller` , che verrà compilata nel codice seguente, separa le funzionalità di ricerca dalla presentazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="433fe-202">Per ora è opportuno scrivere il codice che alimenta i caratteri di ricerca dell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="433fe-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="433fe-203">A questo scopo, viene fornito un metodo denominato `lookupInGraph`che considera la stringa che si vuole cercare.</span><span class="sxs-lookup"><span data-stu-id="433fe-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="433fe-204">Scrivere una classe helper per accedere all'API Graph</span><span class="sxs-lookup"><span data-stu-id="433fe-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="433fe-205">Questo è l'elemento principale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-205">This is the core of our application.</span></span> <span data-ttu-id="433fe-206">Mentre prima è stato inserito il codice nel modello MVC predefinito da Apple, qui viene scritto il codice per eseguire una query del grafico mentre l'utente digita e per restituire tali dati.</span><span class="sxs-lookup"><span data-stu-id="433fe-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="433fe-207">Di seguito viene riportato il codice con una spiegazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="433fe-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="433fe-208">Creare un nuovo file di intestazione Objective C</span><span class="sxs-lookup"><span data-stu-id="433fe-208">Create a new Objective C header file</span></span>
<span data-ttu-id="433fe-209">Assegnare al file il nome `GraphAPICaller.h`e aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="433fe-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="433fe-210">Qui è possibile osservare che si sta specificando un metodo che accetta una stringa e restituisce completionBlock.</span><span class="sxs-lookup"><span data-stu-id="433fe-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="433fe-211">Questo completionBlock, come è intuibile, aggiornerà la tabella fornendo un oggetto con dati popolati in tempo reale mentre l'utente esegue la ricerca.</span><span class="sxs-lookup"><span data-stu-id="433fe-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="433fe-212">Creare un nuovo file Objective C</span><span class="sxs-lookup"><span data-stu-id="433fe-212">Create a new Objective C file</span></span>
<span data-ttu-id="433fe-213">Assegnare al file il nome `GraphAPICaller.m`e aggiungere il metodo seguente.</span><span class="sxs-lookup"><span data-stu-id="433fe-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="433fe-214">Ora questo metodo verrà analizzato in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="433fe-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="433fe-215">L'elemento principale di questo codice è il metodo `NXOAuth2Request`che accetta i parametri definiti prima nel file settings.plist.</span><span class="sxs-lookup"><span data-stu-id="433fe-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="433fe-216">Il primo passaggio consiste nel creare la chiamata API Graph corretta.</span><span class="sxs-lookup"><span data-stu-id="433fe-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="433fe-217">Poiché si sta chiamando `/users`, lo si specifica aggiungendolo alla risorsa API Graph insieme alla versione.</span><span class="sxs-lookup"><span data-stu-id="433fe-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="433fe-218">Questi elementi vengono inseriti in un file delle impostazioni esterno perché possono essere modificati man mano che l'API evolve.</span><span class="sxs-lookup"><span data-stu-id="433fe-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="433fe-219">È quindi necessario specificare altri parametri che verranno forniti alla chiamata API Graph.</span><span class="sxs-lookup"><span data-stu-id="433fe-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="433fe-220">È *molto importante* non inserire i parametri nell'endpoint della risorsa perché i caratteri non conformi all'URI vengono eliminati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="433fe-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="433fe-221">Tutto il codice della query deve essere fornito nei parametri.</span><span class="sxs-lookup"><span data-stu-id="433fe-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="433fe-222">Come si può notare, viene chiamato un metodo `convertParamsToDictionary` che non è ancora stato scritto.</span><span class="sxs-lookup"><span data-stu-id="433fe-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="433fe-223">Verrà fatto ora alla fine del file:</span><span class="sxs-lookup"><span data-stu-id="433fe-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="433fe-224">Ora il metodo `NXOAuth2Request` verrà usato per ottenere di nuovo i dati dall'API in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="433fe-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="433fe-225">Infine si esaminerà come vengono restituiti i dati a MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="433fe-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="433fe-226">I dati vengono restituiti come serializzati e devono essere deserializzati e caricati in un oggetto che MainViewController possa usare.</span><span class="sxs-lookup"><span data-stu-id="433fe-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="433fe-227">A questo scopo, la struttura include un file `User.m/h` che crea un oggetto User.</span><span class="sxs-lookup"><span data-stu-id="433fe-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="433fe-228">L'oggetto User viene popolato con le informazioni del grafico.</span><span class="sxs-lookup"><span data-stu-id="433fe-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="433fe-229">Eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="433fe-229">Run the sample</span></span>
<span data-ttu-id="433fe-230">Se è stata usata la struttura o si è seguita la procedura dettagliata, l'applicazione verrà ora eseguita.</span><span class="sxs-lookup"><span data-stu-id="433fe-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="433fe-231">Avviare il simulatore e fare clic su **Accedi** per usare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="433fe-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="433fe-232">Ottenere aggiornamenti della sicurezza per il prodotto</span><span class="sxs-lookup"><span data-stu-id="433fe-232">Get security updates for our product</span></span>
<span data-ttu-id="433fe-233">È consigliabile ricevere notifiche in caso di problemi di sicurezza. A tale scopo, visitare [Security TechCenter](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="433fe-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

