---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in app Xamarin Forms | Documenti Microsoft
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Xamarin form tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="fb2c1-103">Aggiungere app Xamarin Forms tooyour di autenticazione</span><span class="sxs-lookup"><span data-stu-id="fb2c1-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="fb2c1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fb2c1-104">Overview</span></span>
<span data-ttu-id="fb2c1-105">In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile di servizio App dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="fb2c1-106">In questa esercitazione, si aggiunge l'autenticazione a progetto di avvio rapido Xamarin Forms hello utilizzando un provider di identità che è supportato dal servizio App.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="fb2c1-107">Una volta viene correttamente autenticato e autorizzato dall'App Mobile, valore di ID utente hello viene visualizzato e sarà in grado di tooaccess limitato dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb2c1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fb2c1-108">Prerequisites</span></span>
<span data-ttu-id="fb2c1-109">Per ottenere risultati migliori hello in questa esercitazione, è consigliabile completare prima hello [creare un'app Xamarin Forms] [ 1] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="fb2c1-110">Al termine di questa esercitazione, sarà disponibile un progetto Xamarin.Forms che corrisponde a un'app TodoList multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="fb2c1-111">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="fb2c1-112">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="fb2c1-113">Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="fb2c1-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="fb2c1-114"><a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="fb2c1-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="fb2c1-115">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="fb2c1-116">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="fb2c1-117">In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="fb2c1-118">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="fb2c1-119">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="fb2c1-120">reindirizzamento di hello tooenable sul lato server hello:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="fb2c1-121">In hello [portale], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="fb2c1-122">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="fb2c1-123">In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="fb2c1-124">Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="fb2c1-125">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="fb2c1-126">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="fb2c1-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-127">Click **OK**.</span></span>

5. <span data-ttu-id="fb2c1-128">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="fb2c1-129">Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="fb2c1-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="fb2c1-130">Aggiungi libreria di classi portabile toohello autenticazione</span><span class="sxs-lookup"><span data-stu-id="fb2c1-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="fb2c1-131">App per dispositivi mobili Usa hello [LoginAsync] [ 3] metodo di estensione su hello [MobileServiceClient] [ 4] toosign in un utente con il servizio App autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="fb2c1-132">Questo esempio utilizza un flusso di autenticazione server gestito che consente di visualizzare hello interfaccia del provider Accedi nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="fb2c1-133">Per altre informazioni, vedere [Autenticazione gestita dal server][5].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="fb2c1-134">Per offrire un'esperienza utente migliore nell'app di produzione, è consigliabile prendere invece in considerazione l'uso dell'[autenticazione gestita dal client][6].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="fb2c1-135">tooauthenticate con un progetto Xamarin form, definire un **IAuthenticate** interfaccia hello libreria di classi portabile per app hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="fb2c1-136">Aggiungere quindi una **Accedi** interfaccia utente di toohello pulsante definito nella libreria di classi portabile, in cui si fa clic su hello toostart autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="fb2c1-137">Al termine dell'autenticazione, i dati vengono caricati dal back-end dell'app mobile hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="fb2c1-138">Hello implementare **IAuthenticate** interfaccia per ogni piattaforma supportata dall'app.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="fb2c1-139">In Visual Studio o Xamarin Studio, aprire l'app. cs dal progetto di hello con **portabile** in nome hello, che è il progetto libreria di classi portabile, aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="fb2c1-140">In App. cs, aggiungere hello seguente `IAuthenticate` interfaccia definizione immediatamente prima di hello `App` definizione di classe.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="fb2c1-141">interfaccia hello tooinitialize con un'implementazione specifica della piattaforma, aggiungere hello segue i membri statici toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="fb2c1-142">Aprire TodoList.xaml dal progetto di libreria di classi portabile hello, aggiungere il seguente hello **pulsante** elemento hello *buttonsPanel* elemento di layout, dopo pulsante esistente hello:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="fb2c1-143">Questo pulsante attiva l'autenticazione gestita dal server con il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="fb2c1-144">Aprire TodoList.xaml.cs dal progetto di libreria di classi portabile hello, quindi aggiungere hello seguente campo toohello `TodoList` classe:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="fb2c1-145">Sostituire hello **OnAppearing** metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="fb2c1-146">Questo codice garantisce che i dati solo aggiornati dal servizio hello dopo l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="fb2c1-147">Aggiungere hello seguente gestore per hello **selezionato** evento toohello **TodoList** classe:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="fb2c1-148">Salvare le modifiche e ricompilare il progetto di libreria di classi portabile hello non verifica errori.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="fb2c1-149">Aggiungere app per Android toohello autenticazione</span><span class="sxs-lookup"><span data-stu-id="fb2c1-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="fb2c1-150">Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nel progetto di app Android hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="fb2c1-151">Se i dispositivi Android non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="fb2c1-152">In Visual Studio o Xamarin Studio, fare doppio clic su hello **droid** del progetto, quindi **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="fb2c1-153">Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che, dopo l'avvio dell'applicazione, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="fb2c1-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="fb2c1-154">Poiché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized, viene generato codice 401 Hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="fb2c1-155">Aprire Mainactivity nel progetto Android hello e aggiungere il seguente hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="fb2c1-156">Hello aggiornamento **MainActivity** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="fb2c1-157">Hello aggiornamento **MainActivity** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate**  interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="fb2c1-158">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="fb2c1-159">Aggiungere seguente codice all'interno di hello <application> nodo di AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="fb2c1-160">Aggiungere i seguenti toohello codice hello **OnCreate** metodo hello **MainActivity** classe prima chiamata hello troppo`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="fb2c1-161">Questo codice garantisce l'autenticatore hello viene inizializzata prima carica app hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="fb2c1-162">Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="fb2c1-163">Aggiungere app per iOS toohello autenticazione</span><span class="sxs-lookup"><span data-stu-id="fb2c1-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="fb2c1-164">Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nel progetto di app iOS hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="fb2c1-165">Se i dispositivi iOS non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="fb2c1-166">In Visual Studio o Xamarin Studio, fare doppio clic su hello **iOS** del progetto, quindi **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="fb2c1-167">Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che viene generata un'eccezione non gestita con un codice di stato di 401 (Unauthorized) dopo l'avvio dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="fb2c1-168">risposta 401 Hello viene prodotta perché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="fb2c1-169">Aprire appdelegate. cs nel progetto iOS hello e aggiungere il seguente hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="fb2c1-170">Hello aggiornamento **AppDelegate** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="fb2c1-171">Hello aggiornamento **AppDelegate** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate**  interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="fb2c1-172">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="fb2c1-173">Aggiornare classe AppDelegate hello aggiungendo l'overload del metodo OpenUrl (opzioni NSDictionary di app, url NSUrl, UIApplication)</span><span class="sxs-lookup"><span data-stu-id="fb2c1-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="fb2c1-174">Aggiungere hello successiva riga di codice toohello **FinishedLaunching** chiamata del metodo prima di hello troppo`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="fb2c1-175">Questo codice garantisce l'autenticatore hello viene inizializzata prima che venga caricata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="fb2c1-176">Aggiungere **{url_scheme_of_your_app}** tooURL schemi in Info. plist.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="fb2c1-177">Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="fb2c1-178">Aggiungere l'autenticazione tooWindows 10 (incluso Phone) progetti di app</span><span class="sxs-lookup"><span data-stu-id="fb2c1-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="fb2c1-179">Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nei progetti di app di Windows 10 hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="fb2c1-180">Hello stessi passaggi sono validi per i progetti di piattaforma UWP (Universal Windows), ma utilizzando hello **UWP** progetto (con le modifiche indicate).</span><span class="sxs-lookup"><span data-stu-id="fb2c1-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="fb2c1-181">Se i dispositivi Windows non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="fb2c1-182">"In Visual Studio, fare doppio clic su uno hello **UWP** del progetto, quindi **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="fb2c1-183">Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che viene generata un'eccezione non gestita con un codice di stato di 401 (Unauthorized) dopo l'avvio dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="fb2c1-184">risposta 401 Hello si verifica poiché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="fb2c1-185">Apri il file MainPage.xaml.cs del progetto di app di Windows hello e aggiungere il seguente hello `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="fb2c1-186">Sostituire `<your_Portable_Class_Library_namespace>` con hello dello spazio dei nomi per la libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="fb2c1-187">Hello aggiornamento **MainPage** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="fb2c1-188">Hello aggiornamento **MainPage** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate** interfaccia, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="fb2c1-189">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="fb2c1-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="fb2c1-190">Aggiungere hello successiva riga di codice nel costruttore hello per hello **MainPage** classe prima chiamata hello troppo`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="fb2c1-191">Sostituire `<your_Portable_Class_Library_namespace>` con hello dello spazio dei nomi per la libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="fb2c1-192">Se si utilizza **UWP**, aggiungere il seguente hello **OnActivated** toohello l'override del metodo **App** classe:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="fb2c1-193">Quando l'override del metodo hello esiste già, aggiungere il codice condizionale hello da hello precedente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="fb2c1-194">Questo codice non è necessario per i progetti Universal Windows.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="fb2c1-195">Aggiungere **{schema_url_app}** in Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="fb2c1-196">Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb2c1-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb2c1-197">Next steps</span></span>
<span data-ttu-id="fb2c1-198">Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="fb2c1-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="fb2c1-199">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="fb2c1-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="fb2c1-200">Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="fb2c1-201">Abilitare la sincronizzazione offline per l'app</span><span class="sxs-lookup"><span data-stu-id="fb2c1-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="fb2c1-202">Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="fb2c1-203">Sincronizzazione non in linea consente toointeract gli utenti finali con un'app per dispositivi mobili - visualizzazione, aggiunta o modifica dei dati, anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="fb2c1-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
