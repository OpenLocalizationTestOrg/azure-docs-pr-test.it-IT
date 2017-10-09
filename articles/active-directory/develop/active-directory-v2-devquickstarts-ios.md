---
title: aaaAdd Accedi tooan iOS applicazione usando hello endpoint v 2.0 di Azure AD | Documenti Microsoft
description: Come toobuild un'app iOS che accede agli utenti con entrambi account Microsoft personale e gli account aziendali o dell'istituto di istruzione tramite le librerie di terze parti.
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
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="c1e8e-103">Aggiungere app per iOS tooan Accedi con l'API Graph utilizzando hello v 2.0 endpoint di una libreria di terze parti</span><span class="sxs-lookup"><span data-stu-id="c1e8e-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="c1e8e-104">piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="c1e8e-105">Gli sviluppatori possono utilizzare qualsiasi libreria desiderano toointegrate grazie ai servizi.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="c1e8e-106">gli sviluppatori di toohelp utilizzano la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come piattaforma delle identità Microsoft tooconnect toohello tooconfigure librerie di terze parti.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="c1e8e-107">La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) possono connettersi toohello piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="c1e8e-108">Con un'applicazione hello creati in questa procedura dettagliata, gli utenti possono accedere tootheir organizzazione e quindi cercare altri utenti nell'organizzazione utilizzando hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="c1e8e-109">Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questa configurazione di esempio può non avere senso tooyou.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="c1e8e-110">Per informazioni, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e8e-111">Alcune funzionalità di piattaforma che dispone di un'espressione in hello OAuth2 o OpenID Connect standard, ad esempio l'accesso condizionale e gestione di criteri di Intune, richiedono si toouse l'open source di librerie di identità di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="c1e8e-112">endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e8e-113">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="c1e8e-114">Scaricare il codice da GitHub</span><span class="sxs-lookup"><span data-stu-id="c1e8e-114">Download code from GitHub</span></span>
<span data-ttu-id="c1e8e-115">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="c1e8e-116">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="c1e8e-117">È possibile anche scaricare l'esempio di hello e iniziare subito:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="c1e8e-118">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="c1e8e-118">Register an app</span></span>
<span data-ttu-id="c1e8e-119">Creare una nuova app hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire hello i passaggi dettagliati in [come un'app con endpoint v 2.0 hello tooregister](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="c1e8e-120">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-120">Make sure to:</span></span>

* <span data-ttu-id="c1e8e-121">Hello copia **Id applicazione** che è assegnato tooyour app perché è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="c1e8e-122">Aggiungere hello **Mobile** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="c1e8e-123">Hello copia **URI di reindirizzamento** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="c1e8e-124">È necessario utilizzare il valore predefinito hello di `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="c1e8e-125">Scaricare libreria NXOAuth2 di terze parti hello e creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="c1e8e-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="c1e8e-126">Questa procedura dettagliata, si utilizzerà hello OAuth2Client da GitHub, che è una libreria OAuth2 per Mac OS X e iOS (Cocoa e Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="c1e8e-127">Questa libreria è basata sulla bozza 10 della specifica OAuth2 hello. Implementa il profilo di applicazione nativa hello e supporta l'endpoint di autorizzazione hello dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="c1e8e-128">Questi sono tutti aspetti di hello, occorre toointegrate con la piattaforma di identità Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="c1e8e-129">Aggiungi progetto di libreria di tooyour hello utilizzando CocoaPods</span><span class="sxs-lookup"><span data-stu-id="c1e8e-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="c1e8e-130">CocoaPods è un gestore delle dipendenze per i progetti Xcode.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="c1e8e-131">Gestisce automaticamente i passaggi di installazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="c1e8e-132">Aggiungere hello toothis podfile seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="c1e8e-133">Caricare hello podfile mediante CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="c1e8e-134">Verrà creata una nuova area di lavoro Xcode da caricare.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="c1e8e-135">Esplorare la struttura del progetto hello hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="c1e8e-136">Hello seguente struttura è impostato per il progetto nella struttura hello:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="c1e8e-137">Una visualizzazione master con una ricerca UPN</span><span class="sxs-lookup"><span data-stu-id="c1e8e-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="c1e8e-138">Una vista di dettaglio per i dati di hello sull'utente selezionato hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="c1e8e-139">Una vista di account di accesso in cui un utente possa accedere nel grafico di hello toohello app tooquery</span><span class="sxs-lookup"><span data-stu-id="c1e8e-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="c1e8e-140">File toovarious nell'autenticazione di base tooadd hello verrà spostato.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="c1e8e-141">Altre parti di codice hello, ad esempio di codice visual hello, non pertinenti tooidentity ma vengono forniti per l'utente.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="c1e8e-142">Impostare il file settings.plst hello nella libreria hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="c1e8e-143">Nel progetto di avvio rapido hello, aprire hello `settings.plist` file.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="c1e8e-144">Sostituire i valori hello elementi hello in hello sezione tooreflect hello valori utilizzati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="c1e8e-145">Il codice farà riferimento a questi valori ogni volta che viene utilizzato Active Directory Authentication Library hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="c1e8e-146">Hello `clientId` hello client ID dell'applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="c1e8e-147">Hello `redirectUri` è l'URL di reindirizzamento hello tale portale hello fornito.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="c1e8e-148">Impostare la libreria NXOAuth2Client hello nel LoginViewController</span><span class="sxs-lookup"><span data-stu-id="c1e8e-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="c1e8e-149">libreria NXOAuth2Client Hello richiede tooget alcuni valori impostato.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="c1e8e-150">Dopo avere completato questa attività, è possibile utilizzare hello toocall token acquisito hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="c1e8e-151">Poiché `LoginView` verrà chiamato ogni volta che è necessario tooauthenticate, avrebbe senso tooput i valori di configurazione nel file toothat.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="c1e8e-152">Aggiungere alcuni valori toohello `LoginViewController.m` contesto hello tooset di file per l'autenticazione e autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="c1e8e-153">Dettagli sui valori hello seguono codice hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="c1e8e-154">Esaminare i dettagli sul codice hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="c1e8e-155">prima stringa Hello è per `scopes`.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="c1e8e-156">Hello `User.Read` valore consente di profilo di base hello tooread di hello effettuato l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="c1e8e-157">Maggiori informazioni su tutti gli ambiti disponibili hello in [gli ambiti di autorizzazione di Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="c1e8e-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="c1e8e-158">Per `authURL`, `loginURL`, `bhh`, e `tokenURL`, è consigliabile utilizzare valori hello forniti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="c1e8e-159">Se si usa l'open source di hello librerie di identità di Microsoft Azure, è abbassare questi dati per l'utente tramite l'endpoint dei metadati.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="c1e8e-160">Che abbiamo realizzato operazioni di estrazione di questi valori si hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="c1e8e-161">Hello `keychain` valore è contenitore hello hello NXOAuth2Client libreria utilizzerà toocreate toostore un portachiavi dei token.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="c1e8e-162">Se si desidera tooget single sign-on (SSO) in numerose applicazioni, è possibile specificare hello stesso portachiavi in ognuna delle applicazioni e richiedere l'uso hello di tale portachiavi in Xcode diritti.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="c1e8e-163">Ciò è illustrato nella documentazione di Apple hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="c1e8e-164">rest Hello di questi valori sono libreria hello toouse necessarie e creare posizioni di contesto di toohello toocarry valori.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="c1e8e-165">Creare una cache di URL</span><span class="sxs-lookup"><span data-stu-id="c1e8e-165">Create a URL cache</span></span>
<span data-ttu-id="c1e8e-166">All'interno di `(void)viewDidLoad()`, che viene sempre chiamato dopo il caricamento della visualizzazione hello, codice hello primes una cache per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="c1e8e-167">Aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="c1e8e-168">Creare una visualizzazione Web per l'accesso</span><span class="sxs-lookup"><span data-stu-id="c1e8e-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="c1e8e-169">WebView può richiedere all'utente di hello di altri fattori come messaggio SMS (se configurata) o dall'utente toohello i messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="c1e8e-170">Qui verranno configuri hello WebView e successivamente hello scrittura i callback di hello toohandle codice che verranno eseguito in hello WebView dai servizi di identità hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="c1e8e-171">Eseguire l'override di autenticazione di hello WebView metodi toohandle</span><span class="sxs-lookup"><span data-stu-id="c1e8e-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="c1e8e-172">hello tootell WebView cosa accade quando un utente deve toosign in come descritto in precedenza, è possibile incollare hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

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

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="c1e8e-173">Scrivere codice toohandle hello risultato della richiesta OAuth2 hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="c1e8e-174">Hello codice riportato di seguito gestirà redirectURL hello restituiti da hello WebView.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="c1e8e-175">Se l'autenticazione non è riuscita, codice hello tenterà di nuovo.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="c1e8e-176">Nel frattempo, la libreria hello fornirà errore hello che è possibile vedere nella console di hello o gestire in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="c1e8e-177">Impostare hello contesto OAuth (denominata archivio account)</span><span class="sxs-lookup"><span data-stu-id="c1e8e-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="c1e8e-178">Qui è possibile chiamare `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` nell'archivio di hello account condiviso per ogni servizio che si desidera hello applicazione toobe in grado di tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="c1e8e-179">tipo di account Hello è una stringa che viene utilizzata come identificatore per un determinato servizio.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="c1e8e-180">Poiché si accede hello API Graph, codice hello fa riferimento tooit come `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="c1e8e-181">Impostare quindi un osservatore che indica quando nulla cambia con token hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="c1e8e-182">Dopo avere ottenuto il token hello, viene restituito hello utente indietro toohello `masterView`.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="c1e8e-183">Consente di impostare hello toosearch visualizzazione Master e visualizzare gli utenti di hello da hello API Graph</span><span class="sxs-lookup"><span data-stu-id="c1e8e-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="c1e8e-184">Un'applicazione Master-View-Controller (MVC) che visualizza i dati restituito nella griglia hello hello esula dall'ambito hello di questa procedura dettagliata e molte esercitazioni online spiegano come toobuild uno.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="c1e8e-185">Tutto questo codice è in file scheletro hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="c1e8e-186">Tuttavia, è necessario toodeal con poche operazioni nell'applicazione MVC:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="c1e8e-187">Intercept quando un utente digita un valore nel campo di ricerca hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="c1e8e-188">Fornire un oggetto di dati back-toohello MasterView, pertanto può visualizzare i risultati di hello nella griglia hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="c1e8e-189">Queste operazioni verranno eseguite sotto.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="c1e8e-190">Aggiungere un toosee di controllo se si è connessi</span><span class="sxs-lookup"><span data-stu-id="c1e8e-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="c1e8e-191">un'applicazione Hello non offre se hello utente non è connesso, pertanto se è già presente un token nella cache di hello è toocheck smart.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="c1e8e-192">Se non si reindirizza toohello LoginView per toosign utente hello in.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="c1e8e-193">Se si ricorderà, hello migliore modo toodo azioni quando si carica una visualizzazione è hello toouse `viewDidLoad()` metodo che fornisce Apple.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="c1e8e-194">Aggiornare hello tabella vista quando vengono ricevuti dati</span><span class="sxs-lookup"><span data-stu-id="c1e8e-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="c1e8e-195">Quando si hello API Graph restituisce dati, è necessario dati hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="c1e8e-196">Per semplicità, ecco tutte hello codice tooupdate hello alla tabella.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="c1e8e-197">Nel codice boilerplate MVC, è possibile incollare solo i valori corretti di hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="c1e8e-198">Fornire un hello toocall modo API Graph, quando l'utente immette nel campo di ricerca hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="c1e8e-199">Quando un utente digita una ricerca nella casella hello, è necessario tooshove che su toohello API Graph.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="c1e8e-200">Hello `GraphAPICaller` classe, si compilerà nel seguente codice hello, separa le funzionalità di ricerca hello dalla presentazione hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="c1e8e-201">Per il momento opportuno scrivere codice hello feed qualsiasi toohello caratteri ricerca API Graph.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="c1e8e-202">A tale scopo occorre fornire un metodo denominato `lookupInGraph`, che accetta una stringa hello da toosearch per.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="c1e8e-203">Scrivere un hello tooaccess di classe Helper API Graph</span><span class="sxs-lookup"><span data-stu-id="c1e8e-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="c1e8e-204">Si tratta di core hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-204">This is hello core of our application.</span></span> <span data-ttu-id="c1e8e-205">Mentre rest hello inserimento di codice nel modello MVC predefinito di hello da Apple, qui scrivere grafico hello tooquery del codice come utente hello tipi e restituire quindi i dati.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="c1e8e-206">Ecco il codice hello e segue una spiegazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="c1e8e-207">Creare un nuovo file di intestazione Objective C</span><span class="sxs-lookup"><span data-stu-id="c1e8e-207">Create a new Objective C header file</span></span>
<span data-ttu-id="c1e8e-208">File con nome hello `GraphAPICaller.h`e aggiungere hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="c1e8e-209">Qui è possibile osservare che si sta specificando un metodo che accetta una stringa e restituisce completionBlock.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="c1e8e-210">Questo completionBlock, come si può immaginare, aggiornerà hello tabella fornendo un oggetto con i dati inseriti in tempo reale come hello ricerche degli utenti.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="c1e8e-211">Creare un nuovo file Objective C</span><span class="sxs-lookup"><span data-stu-id="c1e8e-211">Create a new Objective C file</span></span>
<span data-ttu-id="c1e8e-212">File con nome hello `GraphAPICaller.m`e aggiungere al metodo hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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

<span data-ttu-id="c1e8e-213">Ora questo metodo verrà analizzato in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="c1e8e-214">core Hello di questo codice è in hello `NXOAuth2Request`, metodo che accetta i parametri di hello che è già stato definito nel file settings.plist hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="c1e8e-215">primo passaggio Hello è chiamata all'API Graph tooconstruct hello destra.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="c1e8e-216">Poiché si sta chiamando `/users`, si specifica che mediante l'aggiunta di risorse di API Graph toohello con versione di hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="c1e8e-217">Rende senso tooput in un file di impostazioni esterno perché questi può essere modificato con hello API evoluzione.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="c1e8e-218">Successivamente, è necessario toospecify parametri che si fornirà anche toohello chiamata all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="c1e8e-219">È *molto importante* non inserire parametri hello nell'endpoint di risorse hello perché che viene eseguita la pulitura per tutti i caratteri conforme non URI in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="c1e8e-220">Tutto il codice query debba essere fornito nei parametri hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="c1e8e-221">Come si può notare, viene chiamato un metodo `convertParamsToDictionary` che non è ancora stato scritto.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="c1e8e-222">Di seguito farlo ora alla fine di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="c1e8e-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="c1e8e-223">Successivamente, è possibile utilizzare hello `NXOAuth2Request` nuovamente i dati di tooget metodo dall'API di hello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="c1e8e-224">Infine, si esaminerà modalità di restituzione di dati di hello toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="c1e8e-225">dati Hello restituisce come serializzato e deve toobe deserializzato e caricato in un oggetto che hello MainViewController può utilizzare.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="c1e8e-226">A tale scopo, è scheletro hello un `User.m/h` file che crea un oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="c1e8e-227">Inserire l'oggetto utente con le informazioni dal grafico hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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


## <a name="run-hello-sample"></a><span data-ttu-id="c1e8e-228">Eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="c1e8e-228">Run hello sample</span></span>
<span data-ttu-id="c1e8e-229">Se è stato utilizzato scheletro hello o seguito insieme a questa procedura dettagliata hello che dovrebbe essere in esecuzione l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="c1e8e-230">Avviare il simulatore hello e fare clic su **Accedi** toouse un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="c1e8e-231">Ottenere aggiornamenti della sicurezza per il prodotto</span><span class="sxs-lookup"><span data-stu-id="c1e8e-231">Get security updates for our product</span></span>
<span data-ttu-id="c1e8e-232">Si consiglia di notifiche quando gli eventi imprevisti di protezione si verificano visitando hello tooget [Security TechCenter](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="c1e8e-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

