---
title: Azure Active Directory B2C | Documentazione Microsoft
description: "Come creare un'applicazione desktop di Windows con funzionalità di gestione dell'iscrizione, dell'accesso e del profilo utente usando Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="4a2d7-103">Azure AD B2C: creare un'app desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="4a2d7-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="4a2d7-104">Azure Active Directory (Azure AD) B2C consente di aggiungere funzionalità avanzate di gestione delle identità self-service all'app desktop in pochi brevi passaggi.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="4a2d7-105">Questo articolo descrive come creare un'app Windows Presentation Foundation (WPF) .NET "To do list" con funzionalità di gestione dell'iscrizione, dell'accesso e del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="4a2d7-106">L'app includerà il supporto per l'iscrizione e l'accesso tramite un nome utente o un indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="4a2d7-107">L'app includerà anche il supporto per l'iscrizione e l'accesso tramite account di social networking quali Facebook e Google.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="4a2d7-108">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4a2d7-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="4a2d7-109">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="4a2d7-110">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="4a2d7-111">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="4a2d7-112">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a2d7-112">Create an application</span></span>
<span data-ttu-id="4a2d7-113">Successivamente, è necessario creare un'app nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="4a2d7-114">In questo modo Azure AD acquisisce le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="4a2d7-115">Per creare un'app, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="4a2d7-116">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-116">Be sure to:</span></span>

* <span data-ttu-id="4a2d7-117">Includere un **client nativo** nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="4a2d7-118">Copiare l'**URI di reindirizzamento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="4a2d7-119">Si tratta dell'URL predefinito per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="4a2d7-120">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="4a2d7-121">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="4a2d7-122">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="4a2d7-122">Create your policies</span></span>
<span data-ttu-id="4a2d7-123">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4a2d7-124">Questo esempio di codice contiene tre esperienze di identità: iscrizione, accesso e modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="4a2d7-125">È necessario creare i criteri per ogni tipo, come descritto nell' [articolo di riferimento sui criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="4a2d7-126">Durante la creazione dei tre criteri, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="4a2d7-127">Scegliere **Iscrizione ID utente** o **Iscrizione posta elettronica** nel pannello dei provider di identità.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="4a2d7-128">Scegliere **Nome visualizzato** e altri attributi nei criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="4a2d7-129">Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="4a2d7-130">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="4a2d7-131">Copiare il **Nome** di ogni criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="4a2d7-132">Dovrebbero mostrare il prefisso `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="4a2d7-133">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="4a2d7-134">Dopo aver creato i tre criteri, è possibile passare alla compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="4a2d7-135">Scaricare il codice</span><span class="sxs-lookup"><span data-stu-id="4a2d7-135">Download the code</span></span>
<span data-ttu-id="4a2d7-136">Il codice per questa esercitazione è [disponibile in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="4a2d7-137">Per compilare l'esempio passo dopo passo, è possibile [scaricare un progetto bozza come file ZIP](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="4a2d7-138">È anche possibile clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="4a2d7-139">L'app completata è anche [disponibile come file ZIP](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o nel ramo `complete` dello stesso repository.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="4a2d7-140">Dopo aver scaricato il codice di esempio, aprire il file SLN di Visual Studio per iniziare.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="4a2d7-141">Il progetto `TaskClient` è l'applicazione desktop WPF con cui interagisce l'utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="4a2d7-142">Ai fini di questa esercitazione, chiama un'API Web dell'attività back-end, ospitata in Azure, che archivia l'elenco attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="4a2d7-143">Non è necessario compilare l'API Web, perché ne è già in esecuzione una.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="4a2d7-144">Per informazioni sull'autenticazione sicura delle richieste da parte di un'API Web con Azure AD B2C, vedere l' [articolo di introduzione all'API Web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="4a2d7-145">Eseguire i criteri</span><span class="sxs-lookup"><span data-stu-id="4a2d7-145">Execute policies</span></span>
<span data-ttu-id="4a2d7-146">L'app comunica con Azure AD B2C inviando messaggi di autenticazione che specificano i criteri che devono essere eseguiti come parte della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="4a2d7-147">Per le applicazioni desktop .NET, è possibile usare l'anteprima di Microsoft Authentication Library (MSAL) per inviare messaggi di autenticazione OAuth 2.0, eseguire i criteri e ottenere token per chiamare le API Web.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="4a2d7-148">Installare MSAL</span><span class="sxs-lookup"><span data-stu-id="4a2d7-148">Install MSAL</span></span>
<span data-ttu-id="4a2d7-149">Aggiungere MSAL al progetto `TaskClient` usando la console di Gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="4a2d7-150">Immettere le informazioni B2C</span><span class="sxs-lookup"><span data-stu-id="4a2d7-150">Enter your B2C details</span></span>
<span data-ttu-id="4a2d7-151">Aprire il file `Globals.cs` e sostituire i valori della proprietà con i propri.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="4a2d7-152">Questa classe viene usata in tutto il progetto `TaskClient` per fare riferimento ai valori usati comunemente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="4a2d7-153">Creare PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="4a2d7-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="4a2d7-154">La classe primaria di MSAL è `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="4a2d7-155">Questa classe rappresenta l'applicazione nel sistema Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="4a2d7-156">All'avvio dell'app, creare un'istanza di `PublicClientApplication` in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="4a2d7-157">Questa istanza può essere usata in tutta la finestra.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="4a2d7-158">Avvia un flusso di registrazione</span><span class="sxs-lookup"><span data-stu-id="4a2d7-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="4a2d7-159">Quando l'utente sceglie di iscriversi, avviare un flusso di iscrizione che usa i criteri di iscrizione creati.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="4a2d7-160">Con MSAL è sufficiente chiamare `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="4a2d7-161">I parametri passati a `AcquireTokenAsync(...)` determinano quale token si riceve, i criteri usati nella richiesta di autenticazione e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="4a2d7-162">Avvia un flusso di accesso</span><span class="sxs-lookup"><span data-stu-id="4a2d7-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="4a2d7-163">È possibile avviare un flusso di accesso allo stesso modo in cui si avvia un flusso di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="4a2d7-164">Quando l'utente accede, eseguire la stessa chiamata a MSAL, questa volta usando i propri criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="4a2d7-165">Avviare un flusso di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="4a2d7-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="4a2d7-166">Anche in questo caso è possibile eseguire i criteri di modifica del profilo in modo analogo:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="4a2d7-167">In tutti questi casi, MSAL restituisce un token in `AuthenticationResult` oppure genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="4a2d7-168">Ogni volta che si ottiene un token da MSAL, è possibile usare l'oggetto `AuthenticationResult.User` per aggiornare i dati utente nell'app, ad esempio l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="4a2d7-169">ADAL inoltre memorizza nella cache il token per l'uso in altre parti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="4a2d7-170">Verificare la presenza di token all'avvio dell'app</span><span class="sxs-lookup"><span data-stu-id="4a2d7-170">Check for tokens on app start</span></span>
<span data-ttu-id="4a2d7-171">È possibile usare MSAL anche per tenere traccia dello stato di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="4a2d7-172">In questa app si vuole che l'utente rimanga connesso anche dopo che ha chiuso e riaperto l'app.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="4a2d7-173">Nuovamente all'interno dell'override `OnInitialized`, usare il metodo `AcquireTokenSilent` di MSAL per verificare la disponibilità di token memorizzati nella cache:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-the-task-api"></a><span data-ttu-id="4a2d7-174">Chiamare l'API delle attività</span><span class="sxs-lookup"><span data-stu-id="4a2d7-174">Call the task API</span></span>
<span data-ttu-id="4a2d7-175">Finora si è usato MSAL per eseguire i criteri e ottenere i token.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="4a2d7-176">Quando si vuole usare uno di questi token per chiamare l'API dell'attività, è possibile usare di nuovo il metodo `AcquireTokenSilent` di MSAL per verificare la disponibilità di token memorizzati nella cache:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

<span data-ttu-id="4a2d7-177">Quando la chiamata a `AcquireTokenSilentAsync(...)` riesce e viene trovato un token nella cache, è possibile aggiungerlo all'intestazione `Authorization` della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="4a2d7-178">L'API Web dell'attività userà questa intestazione per autenticare la richiesta di lettura dell'elenco attività dell'utente:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="4a2d7-179">Disconnettere l'utente dall'app</span><span class="sxs-lookup"><span data-stu-id="4a2d7-179">Sign the user out</span></span>
<span data-ttu-id="4a2d7-180">Infine, è possibile usare la libreria MSAL per terminare la sessione dell'utente nell'app quando l'utente seleziona **Esci**.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="4a2d7-181">Quando si usa MSAL, questa operazione viene eseguita cancellando tutti i token dalla relativa cache:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="4a2d7-182">Eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="4a2d7-182">Run the sample app</span></span>
<span data-ttu-id="4a2d7-183">Infine, compilare ed eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="4a2d7-184">Effettuare l'iscrizione all'app usando un indirizzo di posta elettronica o un nome utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="4a2d7-185">Disconnettersi e accedere nuovamente con lo stesso account utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="4a2d7-186">Modificare il profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-186">Edit that user's profile.</span></span> <span data-ttu-id="4a2d7-187">Disconnettersi ed eseguire l'iscrizione usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="4a2d7-188">Aggiungere i provider di identità per i social network</span><span class="sxs-lookup"><span data-stu-id="4a2d7-188">Add social IDPs</span></span>
<span data-ttu-id="4a2d7-189">L'app supporta attualmente solo l'iscrizione e l'accesso dell'utente con **account locali**.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="4a2d7-190">Si tratta di account archiviati nella directory B2C che usano un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="4a2d7-191">Usando Azure AD B2C, è possibile aggiungere il supporto per altri provider di identità (IDP) senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="4a2d7-192">Per aggiungere provider di identità per i social media all'applicazione, seguire le istruzioni dettagliate fornite in questi articoli.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="4a2d7-193">Per ogni provider di identità che si vuole supportare, è necessario registrare un'applicazione nel relativo sistema e ottenere un ID client.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="4a2d7-194">Configurare Facebook come provider di identità</span><span class="sxs-lookup"><span data-stu-id="4a2d7-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="4a2d7-195">Configurare Google come provider di identità</span><span class="sxs-lookup"><span data-stu-id="4a2d7-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="4a2d7-196">Configurare Amazon come provider di identità</span><span class="sxs-lookup"><span data-stu-id="4a2d7-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="4a2d7-197">Configurare LinkedIn come provider di identità</span><span class="sxs-lookup"><span data-stu-id="4a2d7-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="4a2d7-198">Dopo aver aggiunto i provider di identità alla directory B2C, è necessario modificare ognuno dei tre criteri per includere i nuovi provider di identità, come descritto nell' [articolo di riferimento sui criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4a2d7-199">Dopo aver salvato i criteri, eseguire nuovamente l'app.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="4a2d7-200">I nuovi provider di identità dovrebbero essere stati aggiunti tra le opzioni di accesso e iscrizione in ognuna delle esperienze per l'identità.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="4a2d7-201">Provare a usare i criteri e osservare gli effetti sull'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="4a2d7-202">Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="4a2d7-203">Fare alcune prove fino a quando non risulta chiaro in che modo sono collegati i criteri, le richieste di autenticazione e MSAL.</span><span class="sxs-lookup"><span data-stu-id="4a2d7-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="4a2d7-204">Come riferimento, l'esempio completo [è disponibile come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4a2d7-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="4a2d7-205">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="4a2d7-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
