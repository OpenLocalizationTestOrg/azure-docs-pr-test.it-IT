---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'applicazione desktop di Windows che include l'accesso, per l'abbonamento e profilo di gestione tramite Azure Active Directory B2C.
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="5049c-103">Azure AD B2C: creare un'app desktop di Windows</span><span class="sxs-lookup"><span data-stu-id="5049c-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="5049c-104">Tramite Azure Active Directory (Azure AD) B2C, è possibile aggiungere app desktop tooyour funzionalità Gestione identità self-service potenti in pochi passaggi brevi.</span><span class="sxs-lookup"><span data-stu-id="5049c-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="5049c-105">In questo articolo viene illustrato come toocreate un'app .NET Windows Presentation Foundation (WPF) "elenco" che include l'utente per l'abbonamento, accesso e la gestione dei profili.</span><span class="sxs-lookup"><span data-stu-id="5049c-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="5049c-106">Hello app verrà incluso il supporto per l'iscrizione e Accedi con un nome utente o un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5049c-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="5049c-107">L'app includerà anche il supporto per l'iscrizione e l'accesso tramite account di social networking quali Facebook e Google.</span><span class="sxs-lookup"><span data-stu-id="5049c-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="5049c-108">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5049c-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="5049c-109">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="5049c-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="5049c-110">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="5049c-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="5049c-111">Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.</span><span class="sxs-lookup"><span data-stu-id="5049c-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="5049c-112">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="5049c-112">Create an application</span></span>
<span data-ttu-id="5049c-113">Successivamente, è necessario toocreate un'app nel servizio directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5049c-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="5049c-114">In questo modo le informazioni di Azure AD che è necessario toosecurely a comunicare con l'app.</span><span class="sxs-lookup"><span data-stu-id="5049c-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="5049c-115">toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5049c-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="5049c-116">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="5049c-116">Be sure to:</span></span>

* <span data-ttu-id="5049c-117">Includere un **native client** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="5049c-118">Hello copia **URI di reindirizzamento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="5049c-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="5049c-119">È l'URL predefinito hello per questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="5049c-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="5049c-120">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="5049c-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="5049c-121">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="5049c-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="5049c-122">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="5049c-122">Create your policies</span></span>
<span data-ttu-id="5049c-123">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="5049c-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5049c-124">Questo esempio di codice contiene tre esperienze di identità: iscrizione, accesso e modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="5049c-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="5049c-125">È necessario toocreate un criterio per ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="5049c-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="5049c-126">Quando si creano tre criteri hello, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="5049c-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="5049c-127">Scegliere **ID utente per l'abbonamento** o **posta elettronica per l'abbonamento** nel Pannello di provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="5049c-128">Scegliere **Nome visualizzato** e altri attributi nei criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="5049c-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="5049c-129">Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="5049c-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="5049c-130">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="5049c-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="5049c-131">Hello copia **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="5049c-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="5049c-132">Devono contenere il prefisso hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="5049c-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="5049c-133">I nomi dei criteri saranno necessari in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5049c-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="5049c-134">Dopo avere creato hello tre criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="5049c-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="5049c-135">Scaricare codice hello</span><span class="sxs-lookup"><span data-stu-id="5049c-135">Download hello code</span></span>
<span data-ttu-id="5049c-136">Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="5049c-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="5049c-137">esempio hello toobuild come si go, è possibile [scaricare un progetto di base come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="5049c-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="5049c-138">È anche possibile clonare scheletro hello:</span><span class="sxs-lookup"><span data-stu-id="5049c-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="5049c-139">è anche l'applicazione Hello completato [disponibile come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o hello `complete` ramo di hello stesso repository.</span><span class="sxs-lookup"><span data-stu-id="5049c-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="5049c-140">Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5049c-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="5049c-141">Hello `TaskClient` progetto è hello applicazione desktop WPF con hello utente interagisce con.</span><span class="sxs-lookup"><span data-stu-id="5049c-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="5049c-142">Ai fini di hello di questa esercitazione, chiama un'attività di back-end API web, ospitato in Azure, che archivia l'elenco di attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="5049c-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="5049c-143">Non è necessario toobuild hello web API, abbiamo già in esecuzione per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5049c-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="5049c-144">toolearn come un'API web in modo sicuro per eseguire l'autenticazione delle richieste tramite Azure Active Directory B2C, vedere il [articolo Introduzione di API web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5049c-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="5049c-145">Eseguire i criteri</span><span class="sxs-lookup"><span data-stu-id="5049c-145">Execute policies</span></span>
<span data-ttu-id="5049c-146">L'app comunica con Azure Active Directory B2C inviando messaggi di autenticazione che specificano i criteri di hello desiderano tooexecute come parte della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="5049c-147">Per le applicazioni desktop .NET, è possibile utilizzare hello visualizzare in anteprima i messaggi di autenticazione OAuth 2.0 toosend libreria di autenticazione di Microsoft (MSAL), eseguire i criteri e ottenere i token che chiamano API web.</span><span class="sxs-lookup"><span data-stu-id="5049c-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="5049c-148">Installare MSAL</span><span class="sxs-lookup"><span data-stu-id="5049c-148">Install MSAL</span></span>
<span data-ttu-id="5049c-149">Aggiungere MSAL toohello `TaskClient` progetto tramite la Console di gestione di pacchetti di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="5049c-150">Immettere le informazioni B2C</span><span class="sxs-lookup"><span data-stu-id="5049c-150">Enter your B2C details</span></span>
<span data-ttu-id="5049c-151">File aperti hello `Globals.cs` e sostituire ogni hello valori delle proprietà con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="5049c-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="5049c-152">Questa classe viene utilizzata in tutta `TaskClient` valori tooreference comunemente utilizzati.</span><span class="sxs-lookup"><span data-stu-id="5049c-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="5049c-153">Creare hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="5049c-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="5049c-154">è la classe primaria Hello di MSAL `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="5049c-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="5049c-155">Questa classe rappresenta l'applicazione nel sistema di hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5049c-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="5049c-156">Quando hello Inizializza app, crea un'istanza di `PublicClientApplication` in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="5049c-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="5049c-157">Questo può essere utilizzato per la finestra hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="5049c-158">Avvia un flusso di registrazione</span><span class="sxs-lookup"><span data-stu-id="5049c-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="5049c-159">Quando un utente opts toosigns backup, è opportuno tooinitiate un flusso di sottoscrizione che utilizza i criteri di iscrizione hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="5049c-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="5049c-160">Con MSAL è sufficiente chiamare `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="5049c-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="5049c-161">parametri passati troppo Hello`AcquireTokenAsync(...)` determinare quale token viene visualizzato, il criterio di hello utilizzato nella richiesta di autenticazione hello e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="5049c-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="5049c-162">Avvia un flusso di accesso</span><span class="sxs-lookup"><span data-stu-id="5049c-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="5049c-163">È possibile avviare un flusso di accesso in hello allo stesso modo che si avvia un flusso di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="5049c-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="5049c-164">Quando un utente accede, rendere hello stesso chiamare tooMSAL, questa volta utilizzando i criteri di accesso:</span><span class="sxs-lookup"><span data-stu-id="5049c-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="5049c-165">Avviare un flusso di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="5049c-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="5049c-166">Nuovamente, è possibile eseguire un criterio di modifica profilo hello allo stesso modo:</span><span class="sxs-lookup"><span data-stu-id="5049c-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="5049c-167">In tutti questi casi, MSAL restituisce un token in `AuthenticationResult` oppure genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="5049c-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="5049c-168">Ogni volta che si ottiene un token da MSAL, è possibile utilizzare hello `AuthenticationResult.User` tooupdate hello dati utente contenuti nelle app hello, ad esempio hello dell'interfaccia utente dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5049c-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="5049c-169">ADAL anche cache hello token per l'uso in altre parti dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="5049c-170">Verificare la presenza di token all'avvio dell'app</span><span class="sxs-lookup"><span data-stu-id="5049c-170">Check for tokens on app start</span></span>
<span data-ttu-id="5049c-171">È anche possibile utilizzare traccia tookeep MSAL dello stato di accesso dell'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="5049c-172">In questa app, è necessario tooremain utente hello effettuato l'accesso anche dopo che Chiudi applicazione hello e aprirlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="5049c-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="5049c-173">Torna all'interno di hello `OnInitialized` sostituire, usare del MSAL `AcquireTokenSilent` toocheck metodo per i token memorizzati nella cache:</span><span class="sxs-lookup"><span data-stu-id="5049c-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="5049c-174">Chiamare l'API di attività hello</span><span class="sxs-lookup"><span data-stu-id="5049c-174">Call hello task API</span></span>
<span data-ttu-id="5049c-175">È ora utilizzato criteri tooexecute MSAL e ottenere i token.</span><span class="sxs-lookup"><span data-stu-id="5049c-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="5049c-176">Quando si desidera toouse una di queste API di token toocall hello attività, è possibile utilizzare nuovamente del MSAL `AcquireTokenSilent` toocheck metodo per i token memorizzati nella cache:</span><span class="sxs-lookup"><span data-stu-id="5049c-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="5049c-177">Quando hello troppo chiamata`AcquireTokenSilentAsync(...)` ha esito positivo e un token è presente nella cache di hello, è possibile aggiungere hello token toohello `Authorization` intestazione della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="5049c-178">API web di attività Hello utilizzerà l'elenco di attività dell'utente questa intestazione tooauthenticate hello richiesta tooread hello:</span><span class="sxs-lookup"><span data-stu-id="5049c-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="5049c-179">Utente hello Sign out</span><span class="sxs-lookup"><span data-stu-id="5049c-179">Sign hello user out</span></span>
<span data-ttu-id="5049c-180">Infine, è possibile utilizzare MSAL tooend una sessione dell'utente con l'applicazione hello quando Seleziona utente hello **Disconnetti**.  Quando si utilizza MSAL, questa operazione viene eseguita la cancellazione di tutti i token hello dalla cache dei token hello:</span><span class="sxs-lookup"><span data-stu-id="5049c-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="5049c-181">Eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="5049c-181">Run hello sample app</span></span>
<span data-ttu-id="5049c-182">Infine, compilare ed eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5049c-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="5049c-183">Iscriversi per l'applicazione hello tramite un nome utente o indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5049c-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="5049c-184">Disconnettersi e accedere di nuovo come hello stesso utente.</span><span class="sxs-lookup"><span data-stu-id="5049c-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="5049c-185">Modificare il profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5049c-185">Edit that user's profile.</span></span> <span data-ttu-id="5049c-186">Disconnettersi ed eseguire l'iscrizione usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="5049c-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="5049c-187">Aggiungere i provider di identità per i social network</span><span class="sxs-lookup"><span data-stu-id="5049c-187">Add social IDPs</span></span>
<span data-ttu-id="5049c-188">Attualmente, app hello supporta solo utente per l'abbonamento e Accedi che utilizzano **gli account locali**.</span><span class="sxs-lookup"><span data-stu-id="5049c-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="5049c-189">Si tratta di account archiviati nella directory B2C che usano un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="5049c-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="5049c-190">Usando Azure AD B2C, è possibile aggiungere il supporto per altri provider di identità (IDP) senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="5049c-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="5049c-191">tooadd social IDPs tooyour app, iniziare eseguendo hello dettagliate negli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="5049c-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="5049c-192">Per ogni provider di identità toosupport, è necessario tooregister un'applicazione in tale sistema e ottenere un ID client.</span><span class="sxs-lookup"><span data-stu-id="5049c-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="5049c-193">Configurare Facebook come provider di identità</span><span class="sxs-lookup"><span data-stu-id="5049c-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="5049c-194">Configurare Google come provider di identità</span><span class="sxs-lookup"><span data-stu-id="5049c-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="5049c-195">Configurare Amazon come provider di identità</span><span class="sxs-lookup"><span data-stu-id="5049c-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="5049c-196">Configurare LinkedIn come provider di identità</span><span class="sxs-lookup"><span data-stu-id="5049c-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="5049c-197">Dopo aver aggiunto una directory B2C tooyour i provider di identità hello, è necessario tooedit ognuno dei criteri di tre tooinclude hello IDPs nuovo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5049c-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5049c-198">Dopo aver salvato i criteri, eseguire l'applicazione hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="5049c-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="5049c-199">Dovrebbe essere hello che idps nuovo aggiunto come opzioni di accesso ed effettuare l'iscrizione in ognuna delle proprie esperienze di identità.</span><span class="sxs-lookup"><span data-stu-id="5049c-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="5049c-200">È possibile sperimentare i criteri e osservare gli effetti di hello nella tua app dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="5049c-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="5049c-201">Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="5049c-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="5049c-202">Fare alcune prove fino a quando non risulta chiaro in che modo sono collegati i criteri, le richieste di autenticazione e MSAL.</span><span class="sxs-lookup"><span data-stu-id="5049c-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="5049c-203">Per riferimento, hello completata esempio [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5049c-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="5049c-204">È anche possibile clonarlo da GitHub:</span><span class="sxs-lookup"><span data-stu-id="5049c-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
