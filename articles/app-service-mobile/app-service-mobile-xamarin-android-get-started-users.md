---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in Android di Xamarin
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Android di Xamarin attraverso una varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="e1057-103">Aggiungere app xamarin tooyour di autenticazione</span><span class="sxs-lookup"><span data-stu-id="e1057-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="e1057-104">In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="e1057-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="e1057-105">In questa esercitazione si Aggiungi progetto di avvio rapido toohello l'autenticazione utilizzando un provider di identità supportati da app mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1057-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="e1057-106">Al termine viene autenticato e autorizzato in hello App per dispositivi mobili, valore di ID utente hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e1057-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="e1057-107">Questa esercitazione è basata su hello Guida introduttiva di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e1057-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="e1057-108">È necessario anche completare Esercitazione hello [creare un'app xamarin].</span><span class="sxs-lookup"><span data-stu-id="e1057-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="e1057-109">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione.</span><span class="sxs-lookup"><span data-stu-id="e1057-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="e1057-110">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e1057-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="e1057-111"><a name="register"></a>Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="e1057-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e1057-112"><a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="e1057-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="e1057-113">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="e1057-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e1057-114">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="e1057-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="e1057-115">In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto.</span><span class="sxs-lookup"><span data-stu-id="e1057-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e1057-116">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="e1057-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e1057-117">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e1057-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="e1057-118">reindirizzamento di hello tooenable sul lato server hello:</span><span class="sxs-lookup"><span data-stu-id="e1057-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="e1057-119">In hello [portale], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="e1057-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e1057-120">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="e1057-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e1057-121">In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e1057-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e1057-122">Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e1057-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e1057-123">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="e1057-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e1057-124">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e1057-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="e1057-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1057-125">Click **OK**.</span></span>

5. <span data-ttu-id="e1057-126">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e1057-126">Click **Save**.</span></span>

## <span data-ttu-id="e1057-127"><a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="e1057-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="e1057-128">In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un dispositivo o l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="e1057-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="e1057-129">Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="e1057-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="e1057-130">Ciò accade perché l'applicazione hello tenta tooaccess back-end App per dispositivi mobili come un utente non autenticato.</span><span class="sxs-lookup"><span data-stu-id="e1057-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="e1057-131">Hello *TodoItem* tabella richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e1057-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="e1057-132">Successivamente, si aggiornerà le risorse toorequest di hello del client app dal back-end di hello App per dispositivi mobili con un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e1057-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="e1057-133"><a name="add-authentication"></a>Aggiungere app toohello authentication</span><span class="sxs-lookup"><span data-stu-id="e1057-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="e1057-134">app Hello è hello tootap di utenti aggiornati toorequire **Accedi** pulsante e l'autenticazione prima di visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e1057-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="e1057-135">Aggiungere i seguenti toohello codice hello **TodoActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="e1057-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="e1057-136">Crea un nuovo tooauthenticate metodo un utente e un gestore per un nuovo **Accedi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e1057-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="e1057-137">utente Hello nel codice di esempio hello precedente viene autenticato utilizzando un account di accesso di Facebook.</span><span class="sxs-lookup"><span data-stu-id="e1057-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="e1057-138">Una finestra di dialogo è l'ID utente utilizzato toodisplay hello dopo l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e1057-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1057-139">Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello passato troppo**LoginAsync** sopra tooone seguenti hello: *MicrosoftAccount*, *Twitter*, *Google*, o *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="e1057-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="e1057-140">In hello **OnCreate** (metodo), delete o hello commento riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e1057-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="e1057-141">Nel file hello Activity_To_Do.axml aggiungere hello seguenti *LoginUser* pulsante definizione prima hello esistente *AddItem* pulsante:</span><span class="sxs-lookup"><span data-stu-id="e1057-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="e1057-142">Aggiungere i seguenti file di risorse Strings toohello elemento hello:</span><span class="sxs-lookup"><span data-stu-id="e1057-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="e1057-143">Aprire il file AndroidManifest.xml hello, aggiungere seguente codice all'interno di hello `<application>` elemento XML:</span><span class="sxs-lookup"><span data-stu-id="e1057-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="e1057-144">In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un emulatore o il dispositivo e accedere con il provider di identità selezionato.</span><span class="sxs-lookup"><span data-stu-id="e1057-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="e1057-145">Quando si è connessi in correttamente, hello elenco delle attività, è possibile apportare aggiornamenti toohello dati hello app verrà visualizzato l'ID di accesso.</span><span class="sxs-lookup"><span data-stu-id="e1057-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[creare un'app xamarin]: app-service-mobile-xamarin-android-get-started.md