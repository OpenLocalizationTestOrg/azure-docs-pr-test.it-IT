---
title: Introduzione all'autenticazione per app per dispositivi mobili in Xamarin Android
description: "Informazioni su come usare le app per dispositivi mobili per autenticare gli utenti dell'app per Xamarin Android tramite vari provider di identità, tra cui AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="04580-103">Aggiungere l'autenticazione all'app per Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="04580-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="04580-104">Questo argomento descrive come autenticare gli utenti di un'app per dispositivi mobili dall'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="04580-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="04580-105">In questa esercitazione si aggiungerà l'autenticazione al progetto di guida introduttiva tramite un provider di identità supportato dal servizio App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="04580-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="04580-106">Una volta completate l'autenticazione e l'autorizzazione nell'app per dispositivi mobili, verrà visualizzato il valore dell'ID utente.</span><span class="sxs-lookup"><span data-stu-id="04580-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="04580-107">Questa esercitazione è basata sulla guida introduttiva dell'app mobile.</span><span class="sxs-lookup"><span data-stu-id="04580-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="04580-108">È anche necessario completare prima l'esercitazione [Creare un'app per Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="04580-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="04580-109">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere il pacchetto di estensione di autenticazione al progetto.</span><span class="sxs-lookup"><span data-stu-id="04580-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="04580-110">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo relativo all' [utilizzo dell'SDK del server back-end .NET per app per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="04580-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="04580-111"><a name="register"></a>Registrare l'app per l'autenticazione e configurare i servizi app</span><span class="sxs-lookup"><span data-stu-id="04580-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="04580-112"><a name="redirecturl"></a>Aggiungere l'app agli URL di reindirizzamento esterni consentiti</span><span class="sxs-lookup"><span data-stu-id="04580-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="04580-113">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="04580-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="04580-114">In questo modo il sistema di autenticazione reindirizza all'app al termine del processo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="04580-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="04580-115">In questa esercitazione si usa lo schema URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="04580-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="04580-116">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="04580-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="04580-117">Lo schema deve essere univoco per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="04580-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="04580-118">Per abilitare il reindirizzamento sul lato server:</span><span class="sxs-lookup"><span data-stu-id="04580-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="04580-119">Nel [portale di Azure] selezionare il servizio app.</span><span class="sxs-lookup"><span data-stu-id="04580-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="04580-120">Fare clic sull'opzione di menu **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="04580-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="04580-121">In **URL di reindirizzamento esterni consentiti** specificare `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="04580-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="04580-122">Il valore **url_scheme_of_your_app** in questa stringa è lo schema URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="04580-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="04580-123">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="04580-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="04580-124">È opportuno prendere nota della stringa scelta perché sarà necessario modificare il codice dell'applicazione per dispositivi mobili con lo schema URL in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="04580-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="04580-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="04580-125">Click **OK**.</span></span>

5. <span data-ttu-id="04580-126">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="04580-126">Click **Save**.</span></span>

## <span data-ttu-id="04580-127"><a name="permissions"></a>Limitare le autorizzazioni agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="04580-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="04580-128">In Visual Studio o Xamarin Studio, eseguire il progetto client su un dispositivo o un emulatore.</span><span class="sxs-lookup"><span data-stu-id="04580-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="04580-129">Verificare che dopo l'avvio dell'app venga generata un'eccezione non gestita con codice di stato 401 (Non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="04580-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="04580-130">L'eccezione non gestita viene generata perché l'app prova ad accedere al back-end dell'app per dispositivi mobili come utente non autenticato.</span><span class="sxs-lookup"><span data-stu-id="04580-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="04580-131">La tabella *TodoItem* richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="04580-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="04580-132">Si aggiornerà quindi l'app client per richiedere le risorse dal back-end dell'app per dispositivi mobili con un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="04580-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="04580-133"><a name="add-authentication"></a>Aggiungere l'autenticazione all'app</span><span class="sxs-lookup"><span data-stu-id="04580-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="04580-134">L'applicazione viene aggiornata per richiedere agli utenti di toccare il pulsante **Accedi** ed eseguire l'autenticazione prima della visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="04580-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="04580-135">Aggiungere il codice seguente alla classe **TodoActivity** :</span><span class="sxs-lookup"><span data-stu-id="04580-135">Add the following code to the **TodoActivity** class:</span></span>
   
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
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="04580-136">Verrà creato un nuovo metodo per autenticare un utente e un gestore del metodo per un nuovo pulsante **Accedi** .</span><span class="sxs-lookup"><span data-stu-id="04580-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="04580-137">Nell'esempio di codice precedente, l'utente viene autenticato tramite un account di accesso di Facebook.</span><span class="sxs-lookup"><span data-stu-id="04580-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="04580-138">Viene usata una finestra di dialogo per visualizzare l'ID utente una volta completata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="04580-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="04580-139">Se si usa un provider di identità diverso da Google, sostituire il valore passato a **LoginAsync** riportato in precedenza con uno dei seguenti: *MicrosoftAccount*, *Twitter*, *Google* o *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="04580-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="04580-140">Nel metodo **OnCreate** , eliminare o impostare come commento la riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="04580-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="04580-141">Nel file Activity_To_Do.axml aggiungere la definizione del pulsante *LoginUser* prima del pulsante *AddItem* esistente:</span><span class="sxs-lookup"><span data-stu-id="04580-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="04580-142">Aggiungere l'elemento seguente al file di risorse Strings.xml:</span><span class="sxs-lookup"><span data-stu-id="04580-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="04580-143">Aprire il file AndroidManifest.xml, aggiungere il codice seguente all'interno dell'elemento XML `<application>`:</span><span class="sxs-lookup"><span data-stu-id="04580-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="04580-144">In Visual Studio o Xamarin Studio eseguire il progetto client in un dispositivo o un emulatore ed eseguire l'accesso tramite il provider di identità scelto.</span><span class="sxs-lookup"><span data-stu-id="04580-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="04580-145">Dopo aver eseguito l'accesso, verranno visualizzati l'ID di accesso l'elenco di elementi ToDo e sarà possibile aggiornare i dati nell'app.</span><span class="sxs-lookup"><span data-stu-id="04580-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="04580-146">[Creare un'app per Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="04580-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>