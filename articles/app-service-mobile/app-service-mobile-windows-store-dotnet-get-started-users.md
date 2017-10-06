---
title: app di Windows della piattaforma UWP (Universal) aaaAdd authentication tooyour | Documenti Microsoft
description: "Informazioni su come gli utenti tooauthenticate di App mobili di Azure App Service toouse dell'app Universal Windows Platform (UWP) utilizzando una varietà di provider di identità, tra cui: AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="fb44d-103">Aggiungere app di Windows authentication tooyour</span><span class="sxs-lookup"><span data-stu-id="fb44d-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="fb44d-104">In questo argomento illustra come app per dispositivi mobili tooyour tooadd l'autenticazione basata su cloud.</span><span class="sxs-lookup"><span data-stu-id="fb44d-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="fb44d-105">In questa esercitazione è aggiungere progetto di avvio rapido di autenticazione toohello piattaforma UWP (Universal Windows) per App per dispositivi mobili utilizzando un provider di identità che è supportato dal servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb44d-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="fb44d-106">Al termine viene autenticato e autorizzato dall'App Mobile back-end, valore di ID utente hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="fb44d-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="fb44d-107">Questa esercitazione è basata su hello avvio rapido di applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb44d-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="fb44d-108">È necessario completare prima esercitazione hello [introduzione App per dispositivi mobili](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb44d-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="fb44d-109"><a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App</span><span class="sxs-lookup"><span data-stu-id="fb44d-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="fb44d-110"><a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="fb44d-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="fb44d-111">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="fb44d-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="fb44d-112">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb44d-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="fb44d-113">In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto.</span><span class="sxs-lookup"><span data-stu-id="fb44d-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="fb44d-114">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="fb44d-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="fb44d-115">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb44d-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="fb44d-116">reindirizzamento di hello tooenable sul lato server hello:</span><span class="sxs-lookup"><span data-stu-id="fb44d-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="fb44d-117">In hello [portale], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="fb44d-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="fb44d-118">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="fb44d-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="fb44d-119">In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="fb44d-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="fb44d-120">Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb44d-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="fb44d-121">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="fb44d-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="fb44d-122">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="fb44d-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="fb44d-123">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb44d-123">Click **OK**.</span></span>

5. <span data-ttu-id="fb44d-124">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fb44d-124">Click **Save**.</span></span>

## <span data-ttu-id="fb44d-125"><a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="fb44d-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="fb44d-126">A questo punto, è possibile verificare che tale back-end tooyour l'accesso anonimo è stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="fb44d-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="fb44d-127">I progetti di app UWP hello imposta come progetto di avvio hello, distribuire ed eseguire app di hello; Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="fb44d-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="fb44d-128">Ciò accade perché l'applicazione hello tenta tooaccess codice dell'App Mobile come un utente non autenticato, ma hello *TodoItem* tabella richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fb44d-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="fb44d-129">Successivamente, si aggiornerà gli utenti di hello app tooauthenticate prima di richiedere risorse di servizio App.</span><span class="sxs-lookup"><span data-stu-id="fb44d-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="fb44d-130"><a name="add-authentication"></a>Aggiungere app toohello authentication</span><span class="sxs-lookup"><span data-stu-id="fb44d-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="fb44d-131">Nel progetto di app UWP hello file MainPage.xaml.cs e aggiungere hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fb44d-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="fb44d-132">Questo codice esegue l'autenticazione utente hello con un account di accesso di Facebook.</span><span class="sxs-lookup"><span data-stu-id="fb44d-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="fb44d-133">Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello di **MobileServiceAuthenticationProvider** sopra toohello valore per il provider.</span><span class="sxs-lookup"><span data-stu-id="fb44d-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="fb44d-134">Sostituire hello **OnNavigatedTo ()** metodo MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="fb44d-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="fb44d-135">Successivamente, si aggiungerà un **Accedi** app toohello pulsante che attiva l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fb44d-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="fb44d-136">Aggiungere hello seguente frammento di codice toohello MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="fb44d-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="fb44d-137">Aprire il file di progetto hello MainPage. XAML, individuare l'elemento hello che definisce hello **salvare** pulsante e sostituirlo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="fb44d-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="fb44d-138">Aggiungere hello seguente frammento di codice toohello App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="fb44d-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="fb44d-139">Aprire il file package. appxmanifest, passare troppo**dichiarazioni**nella **dichiarazioni disponibili** elenco a discesa, seleziona **protocollo** e fare clic su **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fb44d-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="fb44d-140">Configurare ora hello **proprietà** di hello **protocollo** dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="fb44d-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="fb44d-141">In **nome visualizzato**, aggiungere il nome di hello desiderato toousers toodisplay dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fb44d-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="fb44d-142">In **Nome** aggiungere il valore {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="fb44d-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="fb44d-143">Premere hello F5 toorun chiave hello app, fare clic su hello **Accedi** pulsante e sign in app hello con il provider di identità selezionato.</span><span class="sxs-lookup"><span data-stu-id="fb44d-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="fb44d-144">Dopo l'accesso ha esito positivo, hello app viene eseguita senza errori e si tooquery in grado di back-end e apportare aggiornamenti toodata.</span><span class="sxs-lookup"><span data-stu-id="fb44d-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="fb44d-145"><a name="tokens"></a>Archiviare i token di autenticazione hello client hello</span><span class="sxs-lookup"><span data-stu-id="fb44d-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="fb44d-146">Hello esempio precedente ha mostrato uno standard sign-in, che richiede hello client toocontact sia provider di identità hello e hello servizio App ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb44d-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="fb44d-147">Non solo è inefficiente, è possibile eseguire questo metodo in utilizzo-si riferisce problemi molti clienti tentare toostart app in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="fb44d-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="fb44d-148">Un approccio migliore è token di autorizzazione hello toocache restituito dal servizio App e riprovare toouse questo prima di utilizzare un provider basato su Accedi.</span><span class="sxs-lookup"><span data-stu-id="fb44d-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="fb44d-149">È possibile memorizzare nella cache token hello rilasciati da servizi di App, indipendentemente dal fatto se si utilizza l'autenticazione gestita da client o servizio.</span><span class="sxs-lookup"><span data-stu-id="fb44d-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="fb44d-150">In questa esercitazione viene usata l'autenticazione gestita dal servizio.</span><span class="sxs-lookup"><span data-stu-id="fb44d-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="fb44d-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb44d-151">Next steps</span></span>
<span data-ttu-id="fb44d-152">Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="fb44d-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="fb44d-153">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="fb44d-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="fb44d-154">Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb44d-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="fb44d-155">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="fb44d-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="fb44d-156">Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="fb44d-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="fb44d-157">Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="fb44d-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
