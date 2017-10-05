---
title: Introduzione all'autenticazione per app per dispositivi mobili in Xamarin iOS
description: "Informazioni su come usare le app per dispositivi mobili per autenticare gli utenti dell'app Xamarin iOS tramite vari provider di identità, tra cui AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="79d9b-103">Aggiungere l'autenticazione all'app per Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="79d9b-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="79d9b-104">Questo argomento descrive come autenticare gli utenti di un'app mobile del servizio app dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="79d9b-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="79d9b-105">In questa esercitazione verrà aggiunta l'autenticazione al progetto di guida introduttiva Xamarin.iOS tramite un provider di identità supportato dal servizio app.</span><span class="sxs-lookup"><span data-stu-id="79d9b-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="79d9b-106">In seguito all'autenticazione e all'autorizzazione da parte dell'app per dispositivi mobili, viene visualizzato il valore dell'ID utente e si sarà in grado di accedere ai dati della tabella con restrizioni.</span><span class="sxs-lookup"><span data-stu-id="79d9b-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="79d9b-107">È necessario completare prima l'esercitazione [Creare un'app per Xamarin iOS].</span><span class="sxs-lookup"><span data-stu-id="79d9b-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="79d9b-108">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere il pacchetto di estensione di autenticazione al progetto.</span><span class="sxs-lookup"><span data-stu-id="79d9b-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="79d9b-109">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo relativo all' [utilizzo dell'SDK del server back-end .NET per app per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="79d9b-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="79d9b-110">Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="79d9b-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="79d9b-111">Aggiungere l'app agli URL di reindirizzamento esterni consentiti</span><span class="sxs-lookup"><span data-stu-id="79d9b-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="79d9b-112">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="79d9b-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="79d9b-113">In questo modo il sistema di autenticazione reindirizza all'app al termine del processo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="79d9b-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="79d9b-114">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="79d9b-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="79d9b-115">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="79d9b-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="79d9b-116">Lo schema deve essere univoco per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="79d9b-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="79d9b-117">Per abilitare il reindirizzamento sul lato server:</span><span class="sxs-lookup"><span data-stu-id="79d9b-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="79d9b-118">Nel [portale di Azure] selezionare il servizio app.</span><span class="sxs-lookup"><span data-stu-id="79d9b-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="79d9b-119">Fare clic sull'opzione di menu **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="79d9b-120">In **URL di reindirizzamento esterni consentiti** specificare `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="79d9b-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="79d9b-121">Il valore **url_scheme_of_your_app** in questa stringa è lo schema URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="79d9b-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="79d9b-122">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="79d9b-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="79d9b-123">È opportuno prendere nota della stringa scelta perché sarà necessario modificare il codice dell'applicazione per dispositivi mobili con lo schema URL in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="79d9b-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="79d9b-124">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-124">Click **OK**.</span></span>

5. <span data-ttu-id="79d9b-125">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="79d9b-126">Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="79d9b-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="79d9b-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="79d9b-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="79d9b-128">In Visual Studio o Xamarin Studio, eseguire il progetto client su un dispositivo o un emulatore.</span><span class="sxs-lookup"><span data-stu-id="79d9b-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="79d9b-129">Verificare che dopo l'avvio dell'app venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="79d9b-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="79d9b-130">L'errore viene registrato nella console del debugger.</span><span class="sxs-lookup"><span data-stu-id="79d9b-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="79d9b-131">In Visual Studio l'errore dovrebbe quindi essere visualizzato nella finestra di output.</span><span class="sxs-lookup"><span data-stu-id="79d9b-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="79d9b-132">&nbsp;&nbsp;Questo errore non autorizzato viene generato perché l'app prova ad accedere al back-end dell'app per dispositivi mobili come utente non autenticato.</span><span class="sxs-lookup"><span data-stu-id="79d9b-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="79d9b-133">La tabella *TodoItem* richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="79d9b-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="79d9b-134">Si aggiornerà quindi l'app client per richiedere le risorse dal back-end dell'app per dispositivi mobili con un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="79d9b-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="79d9b-135">Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="79d9b-135">Add authentication to the app</span></span>
<span data-ttu-id="79d9b-136">In questa sezione si procederà alla modifica dell'app in modo da visualizzare una schermata di accesso prima dei dati.</span><span class="sxs-lookup"><span data-stu-id="79d9b-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="79d9b-137">All'avvio, l'app non si connetterà al servizio app e non sarà visualizzato alcun dato.</span><span class="sxs-lookup"><span data-stu-id="79d9b-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="79d9b-138">Dopo la prima volta che l'utente esegue il movimento di aggiornamento verrà visualizzata la schermata di accesso. Dopo aver eseguito correttamente l'accesso, verrà visualizzato un elenco di elementi ToDo.</span><span class="sxs-lookup"><span data-stu-id="79d9b-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="79d9b-139">Nel progetto client aprire il file **QSTodoService.cs** e aggiungere quanto segue tramite l'istruzione `MobileServiceUser` con la funzione di accesso alla classe QSTodoService:</span><span class="sxs-lookup"><span data-stu-id="79d9b-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="79d9b-140">Aggiungere un nuovo metodo denominato **Authenticate** a **QSTodoService** con la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="79d9b-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="79d9b-141">Se si usa un provider di identità diverso da Google, sostituire il valore passato a **LoginAsync** riportato in precedenza con uno dei seguenti: _MicrosoftAccount_, _Twitter_, _Google_ o _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="79d9b-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="79d9b-142">Aprire **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="79d9b-143">Modificare la definizione del metodo di **ViewDidLoad** rimuovendo la chiamata a **RefreshAsync()** verso la fine:</span><span class="sxs-lookup"><span data-stu-id="79d9b-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="79d9b-144">Modificare il metodo **RefreshAsync** per autenticare e visualizzare una schermata di accesso se la proprietà **User** è Null.</span><span class="sxs-lookup"><span data-stu-id="79d9b-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="79d9b-145">Aggiungere il codice seguente nella parte superiore della definizione del metodo:</span><span class="sxs-lookup"><span data-stu-id="79d9b-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="79d9b-146">Aprire **AppDelegate.cs** e aggiungere il seguente metodo:</span><span class="sxs-lookup"><span data-stu-id="79d9b-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="79d9b-147">Aprire il file **Info.plist** e passare a **Tipi di URL** nella sezione **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="79d9b-148">Configurare ora l'**identificatore** e gli **schemi URL** del tipo di URL e fare clic su **Aggiungi tipo di URL**.</span><span class="sxs-lookup"><span data-stu-id="79d9b-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="79d9b-149">Gli **schemi URL** devono essere gli stessi del valore {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="79d9b-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="79d9b-150">In Visual Studio o Xamarin Studio connesso all'host di compilazione Xamarin sul Mac eseguire il progetto client destinato a un dispositivo o un emulatore.</span><span class="sxs-lookup"><span data-stu-id="79d9b-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="79d9b-151">Verificare che nell'app non siano visualizzati dati.</span><span class="sxs-lookup"><span data-stu-id="79d9b-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="79d9b-152">Eseguire il movimento di aggiornamento spostando verso il basso l'elenco di elementi, in modo da visualizzare la schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="79d9b-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="79d9b-153">Dopo aver correttamente immesso le credenziali valide, verrà visualizzato l'elenco di elementi ToDo e sarà possibile aggiornare i dati nell'app.</span><span class="sxs-lookup"><span data-stu-id="79d9b-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="79d9b-154">[Creare un'app per Xamarin iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="79d9b-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>