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
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: creare un'app desktop di Windows
Tramite Azure Active Directory (Azure AD) B2C, è possibile aggiungere app desktop tooyour funzionalità Gestione identità self-service potenti in pochi passaggi brevi. In questo articolo viene illustrato come toocreate un'app .NET Windows Presentation Foundation (WPF) "elenco" che include l'utente per l'abbonamento, accesso e la gestione dei profili. Hello app verrà incluso il supporto per l'iscrizione e Accedi con un nome utente o un messaggio di posta elettronica. L'app includerà anche il supporto per l'iscrizione e l'accesso tramite account di social networking quali Facebook e Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Ottenere una directory di Azure AD B2C
Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.  Una directory è un contenitore per utenti, app, gruppi e così via. Se non è già stato fatto, [creare una directory B2C](active-directory-b2c-get-started.md) prima di proseguire con questa guida.

## <a name="create-an-application"></a>Creare un'applicazione
Successivamente, è necessario toocreate un'app nel servizio directory B2C. In questo modo le informazioni di Azure AD che è necessario toosecurely a comunicare con l'app. toocreate un'app, seguire [queste istruzioni](active-directory-b2c-app-registration.md).  Assicurarsi di:

* Includere un **native client** in un'applicazione hello.
* Hello copia **URI di reindirizzamento** `urn:ietf:wg:oauth:2.0:oob`. È l'URL predefinito hello per questo esempio di codice.
* Hello copia **ID applicazione** ovvero tooyour assegnato app. Sarà necessario più avanti.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri
In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questo esempio di codice contiene tre esperienze di identità: iscrizione, accesso e modifica del profilo. È necessario toocreate un criterio per ogni tipo, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando si creano tre criteri hello, assicurarsi di:

* Scegliere **ID utente per l'abbonamento** o **posta elettronica per l'abbonamento** nel Pannello di provider di identità hello.
* Scegliere **Nome visualizzato** e altri attributi nei criteri di iscrizione.
* Scegliere le attestazioni **Nome visualizzato** e **ID oggetto** come attestazioni dell'applicazione in tutti i criteri. È consentito scegliere anche altre attestazioni.
* Hello copia **nome** dei criteri dopo averlo creato. Devono contenere il prefisso hello `b2c_1_`.  I nomi dei criteri saranno necessari in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo avere creato hello tre criteri, si è pronti toobuild l'app.

## <a name="download-hello-code"></a>Scaricare codice hello
Hello codice per questa esercitazione [viene mantenuta in GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). esempio hello toobuild come si go, è possibile [scaricare un progetto di base come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). È anche possibile clonare scheletro hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

è anche l'applicazione Hello completato [disponibile come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o hello `complete` ramo di hello stesso repository.

Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio. Hello `TaskClient` progetto è hello applicazione desktop WPF con hello utente interagisce con. Ai fini di hello di questa esercitazione, chiama un'attività di back-end API web, ospitato in Azure, che archivia l'elenco di attività di ogni utente.  Non è necessario toobuild hello web API, abbiamo già in esecuzione per l'utente.

toolearn come un'API web in modo sicuro per eseguire l'autenticazione delle richieste tramite Azure Active Directory B2C, vedere il [articolo Introduzione di API web](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Eseguire i criteri
L'app comunica con Azure Active Directory B2C inviando messaggi di autenticazione che specificano i criteri di hello desiderano tooexecute come parte della richiesta HTTP hello. Per le applicazioni desktop .NET, è possibile utilizzare hello visualizzare in anteprima i messaggi di autenticazione OAuth 2.0 toosend libreria di autenticazione di Microsoft (MSAL), eseguire i criteri e ottenere i token che chiamano API web.

### <a name="install-msal"></a>Installare MSAL
Aggiungere MSAL toohello `TaskClient` progetto tramite la Console di gestione di pacchetti di Visual Studio hello.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Immettere le informazioni B2C
File aperti hello `Globals.cs` e sostituire ogni hello valori delle proprietà con valori personalizzati. Questa classe viene utilizzata in tutta `TaskClient` valori tooreference comunemente utilizzati.

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

### <a name="create-hello-publicclientapplication"></a>Creare hello PublicClientApplication
è la classe primaria Hello di MSAL `PublicClientApplication`. Questa classe rappresenta l'applicazione nel sistema di hello Azure Active Directory B2C. Quando hello Inizializza app, crea un'istanza di `PublicClientApplication` in `MainWindow.xaml.cs`. Questo può essere utilizzato per la finestra hello.

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

### <a name="initiate-a-sign-up-flow"></a>Avvia un flusso di registrazione
Quando un utente opts toosigns backup, è opportuno tooinitiate un flusso di sottoscrizione che utilizza i criteri di iscrizione hello che è stato creato. Con MSAL è sufficiente chiamare `pca.AcquireTokenAsync(...)`. parametri passati troppo Hello`AcquireTokenAsync(...)` determinare quale token viene visualizzato, il criterio di hello utilizzato nella richiesta di autenticazione hello e altro ancora.

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

### <a name="initiate-a-sign-in-flow"></a>Avvia un flusso di accesso
È possibile avviare un flusso di accesso in hello allo stesso modo che si avvia un flusso di iscrizione. Quando un utente accede, rendere hello stesso chiamare tooMSAL, questa volta utilizzando i criteri di accesso:

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

### <a name="initiate-an-edit-profile-flow"></a>Avviare un flusso di modifica del profilo
Nuovamente, è possibile eseguire un criterio di modifica profilo hello allo stesso modo:

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

In tutti questi casi, MSAL restituisce un token in `AuthenticationResult` oppure genera un'eccezione. Ogni volta che si ottiene un token da MSAL, è possibile utilizzare hello `AuthenticationResult.User` tooupdate hello dati utente contenuti nelle app hello, ad esempio hello dell'interfaccia utente dell'oggetto. ADAL anche cache hello token per l'uso in altre parti dell'applicazione hello.

### <a name="check-for-tokens-on-app-start"></a>Verificare la presenza di token all'avvio dell'app
È anche possibile utilizzare traccia tookeep MSAL dello stato di accesso dell'utente di hello.  In questa app, è necessario tooremain utente hello effettuato l'accesso anche dopo che Chiudi applicazione hello e aprirlo nuovamente.  Torna all'interno di hello `OnInitialized` sostituire, usare del MSAL `AcquireTokenSilent` toocheck metodo per i token memorizzati nella cache:

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

## <a name="call-hello-task-api"></a>Chiamare l'API di attività hello
È ora utilizzato criteri tooexecute MSAL e ottenere i token.  Quando si desidera toouse una di queste API di token toocall hello attività, è possibile utilizzare nuovamente del MSAL `AcquireTokenSilent` toocheck metodo per i token memorizzati nella cache:

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

Quando hello troppo chiamata`AcquireTokenSilentAsync(...)` ha esito positivo e un token è presente nella cache di hello, è possibile aggiungere hello token toohello `Authorization` intestazione della richiesta HTTP hello. API web di attività Hello utilizzerà l'elenco di attività dell'utente questa intestazione tooauthenticate hello richiesta tooread hello:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Utente hello Sign out
Infine, è possibile utilizzare MSAL tooend una sessione dell'utente con l'applicazione hello quando Seleziona utente hello **Disconnetti**.  Quando si utilizza MSAL, questa operazione viene eseguita la cancellazione di tutti i token hello dalla cache dei token hello:

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

## <a name="run-hello-sample-app"></a>Eseguire app di esempio hello
Infine, compilare ed eseguire l'esempio hello.  Iscriversi per l'applicazione hello tramite un nome utente o indirizzo di posta elettronica. Disconnettersi e accedere di nuovo come hello stesso utente. Modificare il profilo dell'utente. Disconnettersi ed eseguire l'iscrizione usando un account utente diverso.

## <a name="add-social-idps"></a>Aggiungere i provider di identità per i social network
Attualmente, app hello supporta solo utente per l'abbonamento e Accedi che utilizzano **gli account locali**. Si tratta di account archiviati nella directory B2C che usano un nome utente e una password. Usando Azure AD B2C, è possibile aggiungere il supporto per altri provider di identità (IDP) senza modificare il codice.

tooadd social IDPs tooyour app, iniziare eseguendo hello dettagliate negli articoli seguenti. Per ogni provider di identità toosupport, è necessario tooregister un'applicazione in tale sistema e ottenere un ID client.

* [Configurare Facebook come provider di identità](active-directory-b2c-setup-fb-app.md)
* [Configurare Google come provider di identità](active-directory-b2c-setup-goog-app.md)
* [Configurare Amazon come provider di identità](active-directory-b2c-setup-amzn-app.md)
* [Configurare LinkedIn come provider di identità](active-directory-b2c-setup-li-app.md)

Dopo aver aggiunto una directory B2C tooyour i provider di identità hello, è necessario tooedit ognuno dei criteri di tre tooinclude hello IDPs nuovo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md). Dopo aver salvato i criteri, eseguire l'applicazione hello nuovamente. Dovrebbe essere hello che idps nuovo aggiunto come opzioni di accesso ed effettuare l'iscrizione in ognuna delle proprie esperienze di identità.

È possibile sperimentare i criteri e osservare gli effetti di hello nella tua app dell'esempio. Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione. Fare alcune prove fino a quando non risulta chiaro in che modo sono collegati i criteri, le richieste di autenticazione e MSAL.

Per riferimento, hello completata esempio [viene fornito come un file con estensione zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). È anche possibile clonarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
