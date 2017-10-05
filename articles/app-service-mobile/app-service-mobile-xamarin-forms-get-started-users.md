---
title: Introduzione all'autenticazione per app per dispositivi mobili nell'app Xamarin.Forms | Documentazione Microsoft
description: "Informazioni su come usare le app per dispositivi mobili per autenticare gli utenti dell'app Xamarin Forms tramite vari provider di identità, tra cui AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="e629a-103">Aggiungere l'autenticazione all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="e629a-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="e629a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e629a-104">Overview</span></span>
<span data-ttu-id="e629a-105">Questo argomento descrive come autenticare gli utenti di un'app mobile del servizio app dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="e629a-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="e629a-106">In questa esercitazione verrà aggiunta l'autenticazione al progetto di guida introduttiva Xamarin.Forms tramite un provider di identità supportato dal servizio app.</span><span class="sxs-lookup"><span data-stu-id="e629a-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="e629a-107">Dopo l'autenticazione e l'autorizzazione da parte dell'app per dispositivi mobili, viene visualizzato il valore dell'ID utente e si potrà accedere ai dati della tabella con restrizioni.</span><span class="sxs-lookup"><span data-stu-id="e629a-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e629a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e629a-108">Prerequisites</span></span>
<span data-ttu-id="e629a-109">Per ottenere risultati ottimali con questa esercitazione, è consigliabile completare prima di tutto l'esercitazione [Creare un'app Xamarin.Forms][1].</span><span class="sxs-lookup"><span data-stu-id="e629a-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="e629a-110">Al termine di questa esercitazione, sarà disponibile un progetto Xamarin.Forms che corrisponde a un'app TodoList multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="e629a-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="e629a-111">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere il pacchetto di estensione di autenticazione al progetto.</span><span class="sxs-lookup"><span data-stu-id="e629a-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="e629a-112">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e629a-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="e629a-113">Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="e629a-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e629a-114"><a name="redirecturl"></a>Aggiungere l'app agli URL di reindirizzamento esterni consentiti</span><span class="sxs-lookup"><span data-stu-id="e629a-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="e629a-115">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e629a-116">In questo modo il sistema di autenticazione reindirizza all'app al termine del processo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e629a-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="e629a-117">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="e629a-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e629a-118">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="e629a-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e629a-119">Lo schema deve essere univoco per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e629a-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="e629a-120">Per abilitare il reindirizzamento sul lato server:</span><span class="sxs-lookup"><span data-stu-id="e629a-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="e629a-121">Nel [portale di Azure] selezionare il servizio app.</span><span class="sxs-lookup"><span data-stu-id="e629a-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e629a-122">Fare clic sull'opzione di menu **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="e629a-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e629a-123">In **URL di reindirizzamento esterni consentiti** specificare `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e629a-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e629a-124">Il valore **url_scheme_of_your_app** in questa stringa è lo schema URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e629a-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e629a-125">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="e629a-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e629a-126">È opportuno prendere nota della stringa scelta perché sarà necessario modificare il codice dell'applicazione per dispositivi mobili con lo schema URL in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="e629a-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="e629a-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e629a-127">Click **OK**.</span></span>

5. <span data-ttu-id="e629a-128">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e629a-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="e629a-129">Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="e629a-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="e629a-130">Aggiungere l'autenticazione alla libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="e629a-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="e629a-131">L'app per dispositivi mobili usa il metodo di estensione [LoginAsync][3] in [MobileServiceClient][4] per eseguire l'accesso di un utente con l'autenticazione del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e629a-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="e629a-132">Questo esempio usa un flusso di autenticazione gestito dal server che mostra l'interfaccia di accesso del provider nell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="e629a-133">Per altre informazioni, vedere [Autenticazione gestita dal server][5].</span><span class="sxs-lookup"><span data-stu-id="e629a-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="e629a-134">Per offrire un'esperienza utente migliore nell'app di produzione, è consigliabile prendere invece in considerazione l'uso dell'[autenticazione gestita dal client][6].</span><span class="sxs-lookup"><span data-stu-id="e629a-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="e629a-135">Per eseguire l'autenticazione con un progetto Xamarin.Forms, definire un'interfaccia **IAuthenticate** nella libreria di classi portabile per l'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="e629a-136">Aggiungere quindi un pulsante di **accesso** all'interfaccia utente definita nella libreria di classi portabile, su cui fare clic per avviare l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e629a-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="e629a-137">Al completamento dell'autenticazione, i dati vengono caricati dal back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e629a-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="e629a-138">Implementare l'interfaccia **IAuthenticate** per ogni piattaforma supportata dall'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="e629a-139">In Visual Studio o Xamarin Studio aprire il file App.cs dal progetto che include **Portable** nel nome, che corrisponde al progetto di libreria di classi portabile, quindi aggiungere l'istruzione `using` seguente:</span><span class="sxs-lookup"><span data-stu-id="e629a-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="e629a-140">In App.cs aggiungere la definizione dell'interfaccia `IAuthenticate` seguente immediatamente prima della definizione della classe `App`.</span><span class="sxs-lookup"><span data-stu-id="e629a-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="e629a-141">Per inizializzare l'interfaccia con un'implementazione specifica per la piattaforma, aggiungere i membri statici seguenti alla classe **App**.</span><span class="sxs-lookup"><span data-stu-id="e629a-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="e629a-142">Aprire il file TodoList.xaml dal progetto della libreria di classi portabile, aggiungere l'elemento **Button** seguente nell'elemento di layout *buttonsPanel* , dopo il pulsante esistente:</span><span class="sxs-lookup"><span data-stu-id="e629a-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="e629a-143">Questo pulsante attiva l'autenticazione gestita dal server con il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e629a-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="e629a-144">Aprire il file TodoList.xaml.cs dal progetto della libreria di classi portabile, quindi aggiungere il campo seguente alla classe `TodoList` :</span><span class="sxs-lookup"><span data-stu-id="e629a-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="e629a-145">Sostituire il metodo **OnAppearing** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e629a-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="e629a-146">Questo codice fa in modo che i dati vengano aggiornati dal servizio solo dopo l'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e629a-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="e629a-147">Aggiungere il gestore seguente per l'evento **Clicked** alla classe **TodoList**:</span><span class="sxs-lookup"><span data-stu-id="e629a-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="e629a-148">Salvare le modifiche e ricompilare il progetto della libreria di classi portabile, senza che si verifichino errori.</span><span class="sxs-lookup"><span data-stu-id="e629a-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="e629a-149">Aggiungere l'autenticazione all'app Android</span><span class="sxs-lookup"><span data-stu-id="e629a-149">Add authentication to the Android app</span></span>
<span data-ttu-id="e629a-150">Questa sezione illustra come implementare l'interfaccia **IAuthenticate** nel progetto di app Android.</span><span class="sxs-lookup"><span data-stu-id="e629a-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="e629a-151">Se i dispositivi Android non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e629a-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="e629a-152">In Visual Studio o Xamarin Studio fare clic con il pulsante destro del mouse sul progetto **droid**, quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="e629a-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e629a-153">Premere F5 per avviare il progetto nel debugger, quindi verificare che venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato) dopo l'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e629a-154">La risposta 401 viene generata perché l'accesso al back-end è limitato solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="e629a-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e629a-155">Aprire il file MainActivity.cs nel progetto Android e aggiungere le istruzioni `using` seguenti:</span><span class="sxs-lookup"><span data-stu-id="e629a-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="e629a-156">Aggiornare la classe **MainActivity** per implementare l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="e629a-157">Aggiornare la classe **MainActivity** aggiungendo un campo **MobileServiceUser** e un metodo **Authenticate**, necessario per l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="e629a-158">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="e629a-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="e629a-159">Aggiungere il codice seguente all'interno del nodo <application> del file AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="e629a-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="e629a-160">Aggiungere il codice seguente al metodo **OnCreate** della classe **MainActivity** prima della chiamata a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="e629a-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="e629a-161">Questo codice fa in modo che l'autenticatore venga inizializzato prima del caricamento dell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="e629a-162">Ricompilare l'app, eseguirla, quindi accedere con il provider di autenticazione selezionato e verificare se è possibile accedere ai dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e629a-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="e629a-163">Aggiungere l'autenticazione all'app iOS</span><span class="sxs-lookup"><span data-stu-id="e629a-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="e629a-164">Questa sezione illustra come implementare l'interfaccia **IAuthenticate** nel progetto di app iOS.</span><span class="sxs-lookup"><span data-stu-id="e629a-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="e629a-165">Se i dispositivi iOS non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e629a-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="e629a-166">In Visual Studio o Xamarin Studio fare clic con il pulsante destro del mouse sul progetto **iOS**, quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="e629a-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e629a-167">Premere F5 per avviare il progetto nel debugger, quindi verificare che venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato) dopo l'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e629a-168">La risposta 401 viene generata perché l'accesso al back-end è limitato solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="e629a-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e629a-169">Aprire il file AppDelegate.cs nel progetto iOS e aggiungere le istruzioni `using` seguenti:</span><span class="sxs-lookup"><span data-stu-id="e629a-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="e629a-170">Aggiornare la classe **AppDelegate** per implementare l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="e629a-171">Aggiornare la classe **AppDelegate** aggiungendo un campo **MobileServiceUser** e un metodo **Authenticate**, necessario per l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="e629a-172">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="e629a-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="e629a-173">Aggiornare la classe AppDelegate aggiungendo l'overload del metodo OpenUrl(UIApplication app, NSUrl url, NSDictionary options)</span><span class="sxs-lookup"><span data-stu-id="e629a-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="e629a-174">Aggiungere la riga di codice seguente al metodo **FinishedLaunching** prima della chiamata a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="e629a-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="e629a-175">Questo codice fa in modo che l'autenticatore venga inizializzato prima del caricamento dell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="e629a-176">Aggiungere **{schema_url_app}** agli schemi URL in Info.plist.</span><span class="sxs-lookup"><span data-stu-id="e629a-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="e629a-177">Ricompilare l'app, eseguirla, quindi accedere con il provider di autenticazione selezionato e verificare se è possibile accedere ai dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e629a-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="e629a-178">Aggiungere l'autenticazione a progetti di app Windows 10 (Windows Phone incluso)</span><span class="sxs-lookup"><span data-stu-id="e629a-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="e629a-179">Questa sezione illustra come implementare l'interfaccia **IAuthenticate** nei progetti di app Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e629a-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="e629a-180">La stessa procedura si applica ai progetti piattaforma UWP (Universal Windows Platform), ma usando il progetto **UWP** con le modifiche indicate.</span><span class="sxs-lookup"><span data-stu-id="e629a-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="e629a-181">Se i dispositivi Windows non sono supportati, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e629a-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="e629a-182">"In Visual Studio fare clic con il pulsante destro del mouse sul progetto **UWP** e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="e629a-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="e629a-183">Premere F5 per avviare il progetto nel debugger, quindi verificare che venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato) dopo l'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="e629a-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e629a-184">La risposta 401 viene generata perché l'accesso al back-end è limitato solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="e629a-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="e629a-185">Aprire il file MainPage.xaml.cs per il progetto di app Windows, quindi aggiungere le istruzioni `using` seguenti:</span><span class="sxs-lookup"><span data-stu-id="e629a-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="e629a-186">Sostituire `<your_Portable_Class_Library_namespace>` con lo spazio dei nomi per la libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="e629a-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="e629a-187">Aggiornare la classe **MainPage** per implementare l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="e629a-188">Aggiornare la classe **MainPage** aggiungendo un campo **MobileServiceUser** e un metodo **Authenticate**, necessario per l'interfaccia **IAuthenticate**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e629a-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="e629a-189">Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="e629a-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="e629a-190">Aggiungere la riga di codice seguente nel costruttore per la classe **MainPage** prima della chiamata a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="e629a-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="e629a-191">Sostituire `<your_Portable_Class_Library_namespace>` con lo spazio dei nomi per la libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="e629a-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="e629a-192">Se si usa **UWP**, aggiungere l'override del metodo **OnActivated** seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="e629a-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="e629a-193">Se l'override del metodo esiste già, aggiungere il codice condizionale del frammento di codice precedente.</span><span class="sxs-lookup"><span data-stu-id="e629a-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="e629a-194">Questo codice non è necessario per i progetti Universal Windows.</span><span class="sxs-lookup"><span data-stu-id="e629a-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="e629a-195">Aggiungere **{schema_url_app}** in Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="e629a-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="e629a-196">Ricompilare l'app, eseguirla, quindi accedere con il provider di autenticazione selezionato e verificare se è possibile accedere ai dati come utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e629a-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e629a-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e629a-197">Next steps</span></span>
<span data-ttu-id="e629a-198">Dopo aver completato questa esercitazione sull'autenticazione di base, provare a continuare fino a una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e629a-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="e629a-199">Aggiungere notifiche push all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="e629a-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="e629a-200">: informazioni su come aggiungere il supporto per le notifiche push all'app e configurare il back-end dell'app per dispositivi mobili per usare Hub di notifica di Azure per l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="e629a-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="e629a-201">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="e629a-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="e629a-202">Informazioni su come aggiungere il supporto offline all'app usando il back-end di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e629a-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="e629a-203">La sincronizzazione offline consente agli utenti finali di interagire con un'app, visualizzando, aggiungendo e modificando i dati, anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="e629a-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
