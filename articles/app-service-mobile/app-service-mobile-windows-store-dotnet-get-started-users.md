---
title: Aggiungere l'autenticazione all'app UWP (Universal Windows Platform) | Documentazione Microsoft
description: "Informazioni su come usare le app per dispositivi mobili del servizio app di Azure per autenticare gli utenti dell'app UWP (Universal Windows Platform) tramite vari provider di identità, tra cui AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="10e1e-103">Aggiungere l'autenticazione all'app Windows</span><span class="sxs-lookup"><span data-stu-id="10e1e-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="10e1e-104">In questo argomento viene illustrato come aggiungere l'autenticazione basata su cloud all’app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="10e1e-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="10e1e-105">In questa esercitazione si aggiungerà l'autenticazione al progetto di guida introduttiva UWP (Universal Windows Platform) per App per dispositivi mobili tramite un provider di identità supportato dal Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="10e1e-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="10e1e-106">In seguito all'autenticazione e all'autorizzazione da parte dell'app per dispositivi mobili, viene visualizzato il valore dell'ID utente.</span><span class="sxs-lookup"><span data-stu-id="10e1e-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="10e1e-107">Questa esercitazione è basata sulla guida introduttiva di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="10e1e-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="10e1e-108">È necessario completare prima l'esercitazione relativa alla [creazione di un'app per dispositivi mobili](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="10e1e-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="10e1e-109"><a name="register"></a>Registrare l'app per l'autenticazione e configurare il servizio app</span><span class="sxs-lookup"><span data-stu-id="10e1e-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="10e1e-110"><a name="redirecturl"></a>Aggiungere l'app agli URL di reindirizzamento esterni consentiti</span><span class="sxs-lookup"><span data-stu-id="10e1e-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="10e1e-111">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="10e1e-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="10e1e-112">In questo modo il sistema di autenticazione reindirizza all'app al termine del processo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="10e1e-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="10e1e-113">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="10e1e-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="10e1e-114">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="10e1e-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="10e1e-115">Lo schema deve essere univoco per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="10e1e-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="10e1e-116">Per abilitare il reindirizzamento sul lato server:</span><span class="sxs-lookup"><span data-stu-id="10e1e-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="10e1e-117">Nel [portale di Azure] selezionare il servizio app.</span><span class="sxs-lookup"><span data-stu-id="10e1e-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="10e1e-118">Fare clic sull'opzione di menu **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="10e1e-119">In **URL di reindirizzamento esterni consentiti** specificare `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="10e1e-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="10e1e-120">Il valore **url_scheme_of_your_app** in questa stringa è lo schema URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="10e1e-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="10e1e-121">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="10e1e-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="10e1e-122">È opportuno prendere nota della stringa scelta perché sarà necessario modificare il codice dell'applicazione per dispositivi mobili con lo schema URL in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="10e1e-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="10e1e-123">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-123">Click **OK**.</span></span>

5. <span data-ttu-id="10e1e-124">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-124">Click **Save**.</span></span>

## <span data-ttu-id="10e1e-125"><a name="permissions"></a>Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="10e1e-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="10e1e-126">A questo punto, è possibile verificare che l'accesso anonimo al back-end è stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="10e1e-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="10e1e-127">Dopo aver impostato il progetto di app UWP come progetto di avvio, distribuire ed eseguire l'app. Verificare che dopo l'avvio dell'app venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="10e1e-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="10e1e-128">L'eccezione non gestita viene generata perché l'app prova ad accedere al codice dell'app per dispositivi mobili come utente non autenticato, mentre la tabella *TodoItem* richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="10e1e-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="10e1e-129">A questo punto, si aggiornerà l'app in modo che autentichi gli utenti prima di richiedere risorse al servizio mobile.</span><span class="sxs-lookup"><span data-stu-id="10e1e-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="10e1e-130"><a name="add-authentication"></a>Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="10e1e-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="10e1e-131">Nel file del progetto dell'app UWP MainPage.xaml.cs aggiungere il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="10e1e-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="10e1e-132">L'utente viene autenticato nel codice tramite un account di accesso di Facebook.</span><span class="sxs-lookup"><span data-stu-id="10e1e-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="10e1e-133">Se si usa un provider di identità diverso da Facebook, sostituire il valore di **MobileServiceAuthenticationProvider** con il nome del provider.</span><span class="sxs-lookup"><span data-stu-id="10e1e-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="10e1e-134">Sostituire il metodo **OnNavigatedTo()** in MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="10e1e-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="10e1e-135">A questo punto aggiungere un pulsante di **accesso** all'app che attiva l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="10e1e-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="10e1e-136">Aggiungere il seguente frammento di codice a MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="10e1e-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="10e1e-137">Aprire il file di progetto MainPage.xaml, individuare l'elemento che definisce il pulsante **Save** e sostituirlo con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="10e1e-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="10e1e-138">Aggiungere il seguente frammento di codice ad App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="10e1e-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="10e1e-139">Aprire il file Package.appxmanifest, passare a **Dichiarazioni** nell'elenco a discesa **Dichiarazioni disponibili**, selezionare **Protocollo** e fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="10e1e-140">Configurare ora le **Proprietà** della dichiarazione **Protocollo**.</span><span class="sxs-lookup"><span data-stu-id="10e1e-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="10e1e-141">In **Nome visualizzato** aggiungere il nome da mostrare agli utenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10e1e-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="10e1e-142">In **Nome** aggiungere il valore {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="10e1e-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="10e1e-143">Premere il tasto F5 per eseguire l'app, fare clic sul pulsante **Sign in** e accedere all'app con il provider di identità scelto.</span><span class="sxs-lookup"><span data-stu-id="10e1e-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="10e1e-144">Dopo che l'accesso è stato completato, l'app funziona senza errori ed è possibile eseguire query nel back-end e aggiornare i dati.</span><span class="sxs-lookup"><span data-stu-id="10e1e-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="10e1e-145"><a name="tokens"></a>Archiviare il token di autenticazione sul client</span><span class="sxs-lookup"><span data-stu-id="10e1e-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="10e1e-146">Nell'esempio precedente è stato illustrato un accesso standard, che richiede al client di contattare sia il provider di identità sia il servizio app ogni volta che l'app viene avviata.</span><span class="sxs-lookup"><span data-stu-id="10e1e-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="10e1e-147">Non solo questo metodo è inefficiente, ma si potrebbero riscontrare problemi relativi all'uso qualora molti clienti provassero ad avviare l'app contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="10e1e-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="10e1e-148">Un miglior approccio consiste nel memorizzare nella cache il token di autorizzazione restituito dal servizio app e provare a usare questo prima di usare un accesso basato su provider.</span><span class="sxs-lookup"><span data-stu-id="10e1e-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="10e1e-149">È possibile memorizzare nella cache il token rilasciato dai Servizi app indipendentemente dal fatto che si usi l'autenticazione gestita dal client o gestita dal servizio.</span><span class="sxs-lookup"><span data-stu-id="10e1e-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="10e1e-150">In questa esercitazione viene usata l'autenticazione gestita dal servizio.</span><span class="sxs-lookup"><span data-stu-id="10e1e-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="10e1e-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10e1e-151">Next steps</span></span>
<span data-ttu-id="10e1e-152">Dopo aver completato questa esercitazione sull'autenticazione di base, provare a continuare fino a una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="10e1e-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="10e1e-153">Aggiungere notifiche push all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="10e1e-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="10e1e-154">: informazioni su come aggiungere il supporto per le notifiche push all'app e configurare il back-end dell'app per dispositivi mobili per usare Hub di notifica di Azure per l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="10e1e-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="10e1e-155">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="10e1e-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="10e1e-156">: informazioni su come aggiungere il supporto offline all'app usando il back-end di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="10e1e-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="10e1e-157">La sincronizzazione offline consente agli utenti finali di interagire con un'app&mdash;visualizzando, aggiungendo e modificando i dati&mdash;anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="10e1e-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
