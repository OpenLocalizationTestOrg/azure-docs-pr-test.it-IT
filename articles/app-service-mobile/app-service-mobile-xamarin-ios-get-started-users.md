---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in Xamarin iOS
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Xamarin iOS tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="e55a4-103">Aggiungere app xamarin tooyour di autenticazione</span><span class="sxs-lookup"><span data-stu-id="e55a4-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="e55a4-104">In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile di servizio App dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="e55a4-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="e55a4-105">In questa esercitazione, si aggiunge l'autenticazione toohello xamarin delle Guide rapide progetto usando un provider di identità che è supportato dal servizio App.</span><span class="sxs-lookup"><span data-stu-id="e55a4-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="e55a4-106">Dopo che viene correttamente autenticato e autorizzato dall'App Mobile, valore di ID utente hello viene visualizzato e sarà in grado di tooaccess limitato dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="e55a4-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="e55a4-107">È necessario completare prima esercitazione hello [creare un'app xamarin].</span><span class="sxs-lookup"><span data-stu-id="e55a4-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="e55a4-108">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione.</span><span class="sxs-lookup"><span data-stu-id="e55a4-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="e55a4-109">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e55a4-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="e55a4-110">Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="e55a4-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="e55a4-111">Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="e55a4-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="e55a4-112">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="e55a4-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e55a4-113">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="e55a4-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="e55a4-114">In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto.</span><span class="sxs-lookup"><span data-stu-id="e55a4-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e55a4-115">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="e55a4-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e55a4-116">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e55a4-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="e55a4-117">reindirizzamento di hello tooenable sul lato server hello:</span><span class="sxs-lookup"><span data-stu-id="e55a4-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="e55a4-118">In hello [portale], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="e55a4-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e55a4-119">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="e55a4-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e55a4-120">In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e55a4-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e55a4-121">Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e55a4-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e55a4-122">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="e55a4-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e55a4-123">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e55a4-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="e55a4-124">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e55a4-124">Click **OK**.</span></span>

5. <span data-ttu-id="e55a4-125">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e55a4-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="e55a4-126">Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="e55a4-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="e55a4-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="e55a4-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="e55a4-128">In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un dispositivo o l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="e55a4-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="e55a4-129">Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="e55a4-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="e55a4-130">Errore Hello è connesso toohello console del debugger hello.</span><span class="sxs-lookup"><span data-stu-id="e55a4-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="e55a4-131">In Visual Studio, pertanto, verrà visualizzato errore hello nella finestra di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e55a4-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="e55a4-132">&nbsp;&nbsp;Questo errore non autorizzato si verifica perché l'applicazione hello tenta tooaccess back-end App per dispositivi mobili come un utente non autenticato.</span><span class="sxs-lookup"><span data-stu-id="e55a4-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="e55a4-133">Hello *TodoItem* tabella richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e55a4-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="e55a4-134">Successivamente, si aggiornerà le risorse toorequest di hello del client app dal back-end di hello App per dispositivi mobili con un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e55a4-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="e55a4-135">Aggiungere app toohello authentication</span><span class="sxs-lookup"><span data-stu-id="e55a4-135">Add authentication toohello app</span></span>
<span data-ttu-id="e55a4-136">In questa sezione si modificherà hello app toodisplay una schermata di accesso prima di visualizzare dati.</span><span class="sxs-lookup"><span data-stu-id="e55a4-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="e55a4-137">Quando viene avviata l'applicazione hello, non non si connetteranno tooyour servizio App e non verrà visualizzati tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="e55a4-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="e55a4-138">Dopo la prima volta hello hello eseguite dall'utente hello movimenti di aggiornamento, viene visualizzata la finestra hello; Dopo che verrà visualizzato l'elenco di accesso con esito positivo hello delle attività.</span><span class="sxs-lookup"><span data-stu-id="e55a4-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="e55a4-139">Nel progetto client hello, aprire il file hello **QSTodoService.cs** e aggiungere hello seguente istruzione using e `MobileServiceUser` con funzione di accesso toohello QSTodoService classe:</span><span class="sxs-lookup"><span data-stu-id="e55a4-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="e55a4-140">Aggiungi nuovo metodo denominato **Authenticate** troppo**QSTodoService** con hello seguente definizione:</span><span class="sxs-lookup"><span data-stu-id="e55a4-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="e55a4-141">Se si utilizza un provider di identità diverso da un Facebook, modificare il valore di hello passato troppo**LoginAsync** sopra tooone seguenti hello: _MicrosoftAccount_, _Twitter_, _Google_, o _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="e55a4-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="e55a4-142">Aprire **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="e55a4-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="e55a4-143">Modificare la definizione di metodo hello di **ViewDidLoad** rimozione chiamata hello troppo**RefreshAsync()** verso la fine hello:</span><span class="sxs-lookup"><span data-stu-id="e55a4-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="e55a4-144">Modificare il metodo hello **RefreshAsync** tooauthenticate se hello **utente** proprietà è null.</span><span class="sxs-lookup"><span data-stu-id="e55a4-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="e55a4-145">Aggiungere hello codice nella parte superiore di hello hello della definizione di metodo seguenti:</span><span class="sxs-lookup"><span data-stu-id="e55a4-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="e55a4-146">Aprire **appdelegate. cs**, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="e55a4-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="e55a4-147">Aprire **Info. plist** file, passare troppo**URL tipi** in hello **avanzate** sezione.</span><span class="sxs-lookup"><span data-stu-id="e55a4-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="e55a4-148">Configurare ora hello **identificatore** hello e **schemi URL** del tipo di URL e fare clic su **Aggiungi tipo URL**.</span><span class="sxs-lookup"><span data-stu-id="e55a4-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="e55a4-149">**Gli schemi URL** deve essere hello stesso come il {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="e55a4-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="e55a4-150">In Visual Studio o Xamarin Studio connessa tooyour Xamarin Host di compilazione nel Mac, eseguire il progetto di client hello destinato a un dispositivo o un emulatore.</span><span class="sxs-lookup"><span data-stu-id="e55a4-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="e55a4-151">Verificare che app hello non visualizza alcun dato.</span><span class="sxs-lookup"><span data-stu-id="e55a4-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="e55a4-152">Eseguire l'operazione di aggiornamento di hello trascinando verso il basso hello elenco di elementi, che provoca il tooappear schermata di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="e55a4-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="e55a4-153">Dopo che sono state immesse credenziali valide, hello app verrà visualizzato l'elenco hello delle attività, mentre è possibile apportare aggiornamenti toohello dati.</span><span class="sxs-lookup"><span data-stu-id="e55a4-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[creare un'app xamarin]: app-service-mobile-xamarin-ios-get-started.md