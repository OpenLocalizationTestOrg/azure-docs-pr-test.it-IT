---
title: .NET aaaAzure AD introduzione | Documenti Microsoft
description: Toobuild un'applicazione Desktop di Windows .NET che si integra con Azure AD per l'accesso di Azure AD come protetto tramite OAuth API.
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Integrare Azure AD in un'app WPF desktop di Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Se si sta sviluppando un'applicazione desktop, Azure AD rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory.  Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.

Per .NET native client che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library o ADAL.  Obiettivo esclusivo della libreria ADAL è toomake è più facile per i token di accesso tooget app.  la semplicità è, toodemonstrate qui creeremo un'applicazione elenco attività di WPF .NET che:

* Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Cerca in una directory gli utenti con un determinato alias.
* Disconnette gli utenti.

toobuild hello completo lavoro dell'applicazione, è necessario:

1. Registrare l'applicazione con Azure AD.
2. Installare e configurare ADAL.
3. Usare i token ADAL tooget da Azure AD.

tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.  Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Registrare hello DirectorySearcher applicazione
tooenable token tooget app, è prima necessario tooregister tenant in Azure AD e concedergli hello tooaccess autorizzazione API Azure AD Graph:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.
4. Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.
5. Seguire le istruzioni di hello e creare un nuovo **applicazione Client nativa**.
  * Hello **nome** di hello applicazione descriverà tooend utenti applicazione
  * Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD utilizzerà le risposte token tooreturn.  Immettere ad esempio, un'applicazione specifica tooyour valore `http://DirectorySearcher`.
6. Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.  È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla pagina dell'applicazione hello.
7. Da hello **impostazioni** pagina, scegliere **autorizzazioni obbligatorie** e scegliere **Aggiungi**. Seleziona hello **Microsoft Graph** come hello API e aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.  In questo modo hello di tooquery l'applicazione API Graph per gli utenti.

## <a name="2-install--configure-adal"></a>2. Installare e configurare ADAL
Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.  Affinché toocommunicate in grado di toobe ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.

* Inizia ad aggiungere il progetto di DirectorySearcher toohello ADAL utilizzando Console Gestione pacchetti hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Nel progetto DirectorySearcher hello aprire `app.config`.  Sostituire i valori hello elementi hello in hello `<appSettings>` hello tooreflect sezione valori di input nel portale di Azure hello.  Il codice farà riferimento a questi valori ogni volta che userà ADAL.
  * Hello `ida:Tenant` dominio hello del tenant di Azure AD, ad esempio contoso.onmicrosoft.com
  * Hello `ida:ClientId` è clientId hello dell'applicazione copiata dal portale hello.
  * Hello `ida:RedirectUri` è hello è registrato nel portale di hello url di reindirizzamento.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Usare ADAL tooGet token da Azure Active Directory
Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente `authContext.AcquireTokenAsync(...)`, e ADAL hello rest.  

* In hello `DirectorySearcher` progetto, aprire `MainWindow.xaml.cs` e individuare hello `MainWindow()` metodo.  primo passaggio Hello è tooinitialize dell'app `AuthenticationContext` -ADAL della classe primaria.  Si tratta in cui si passa ADAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Ora individuare hello `Search(...)` metodo, che verrà richiamato quando hello utente cliks hello "Ricerca" pulsante nell'interfaccia utente dell'applicazione hello.  Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.  Ma in hello tooquery ordine API Graph, è necessario tooinclude access_token in hello `Authorization` richiesta di intestazione di hello - si tratta in cui è disponibile in ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Quando l'app richiede un token chiamando `AcquireTokenAsync(...)`, ADAL tenterà tooreturn un token senza chiedere utente hello per le credenziali.  Se ADAL rileva che l'utente hello toosign in tooget un token, verrà visualizzato una finestra di dialogo account di accesso, raccogliere le credenziali dell'utente hello e restituisce un token alla riuscita dell'autenticazione.  Se la libreria ADAL è Impossibile tooreturn un token per qualsiasi motivo, verrà generata una `AdalException`.
* Si noti che hello `AuthenticationResult` oggetto contiene un `UserInfo` oggetto che può essere utilizzato toocollect informazioni dell'app potrebbe essere necessario.  In hello DirectorySearcher, `UserInfo` è l'interfaccia utente dell'applicazione hello toocustomize utilizzato con l'id dell'utente hello.
* Quando l'utente hello fa clic sul pulsante "Sign Out" hello, si vuole tooensure che hello chiamata successiva troppo`AcquireTokenAsync(...)` chiederà toosign utente hello in.  Con ADAL, non è semplice come la cancellazione della cache dei token hello:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Tuttavia, se utente hello non fa clic sul pulsante "Sign Out" hello, si desidererà toomaintain hello sessione utente per hello successiva esecuzione hello DirectorySearcher.  Quando viene avviata l'applicazione hello, è possibile controllare cache del token della libreria ADAL per un token esistente e aggiornare di conseguenza hello dell'interfaccia utente.  In hello `CheckForCachedToken()` (metodo), eseguire un'altra chiamata troppo`AcquireTokenAsync(...)`, questa volta passando hello `PromptBehavior.Never` parametro.  `PromptBehavior.Never`indicherà ADAL che hello utente non viene richiesto per l'accesso e ADAL deve invece generare un'eccezione se è Impossibile tooreturn un token.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

Congratulazioni. È ora un'applicazione WPF .NET con gli utenti di hello possibilità tooauthenticate funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.  Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.  Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.  Cercare altri utenti in base al relativo UPN.  Chiudere l'applicazione hello ed eseguirla nuovamente.  Si noti come hello sessione rimane invariata.  Disconnettersi e accedere nuovamente come un altro utente.

ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.  Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.  Ciò che occorre tooknow è una singola chiamata API, `authContext.AcquireTokenAsync(...)`.

Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  È possibile procedere con tooadditional scenari.  È opportuno tootry:

[Proteggere un'API Web .NET con Azure AD >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

