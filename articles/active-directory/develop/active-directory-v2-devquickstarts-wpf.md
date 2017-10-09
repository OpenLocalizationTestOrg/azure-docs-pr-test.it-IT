---
title: versione 2.0 di Active Directory aaaAzure .NET Native App | Documenti Microsoft
description: Come toobuild un'applicazione nativa .NET che esegue l'accesso agli utenti con entrambi Account Microsoft personale e gli account aziendali o dell'istituto di istruzione.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Aggiungere app per Windows Desktop Accedi tooa
Con l'endpoint di hello hello v 2.0 è possibile aggiungere rapidamente applicazioni desktop per l'autenticazione tooyour con supporto per entrambi gli account Microsoft personali e gli account aziendali o dell'istituto di istruzione.  È anche Abilita toosecurely l'app di comunicare con un back-end web api, nonché [hello Microsoft Graph](https://graph.microsoft.io) e alcuni di hello [Unified API di Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory (AD) sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

Per [app .NET native eseguite in un dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), Azure Active Directory fornisce hello libreria di autenticazione di Microsoft Identity o MSAL.  Unico scopo del MSAL vita è toomake è più facile per l'app tooget token per chiamare i servizi web.  la semplicità è, toodemonstrate qui creeremo un'app di elenco attività di WPF .NET che:

* Segni di hello utente nel & ottiene accesso token usando hello [protocollo di autenticazione OAuth 2.0](active-directory-v2-protocols.md).
* Chiama in modo sicuro un servizio Web To Do List di back-end, anch'esso protetto da OAuth 2.0.
* Utente di hello segni out.

## <a name="download-sample-code"></a>Scaricare il codice di esempio
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) o scheletro hello clone:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

app Hello completato è disponibile alla fine hello anche in questa esercitazione.

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app in [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).  Verificare di:

* Copia verso il basso hello **Id applicazione** assegnato tooyour app, è necessario prima.
* Aggiungere hello **Mobile** piattaforma per l'app.

## <a name="install--configure-msal"></a>Installare e configurare MSAL
A questo punto si ha un'app registrata in Microsoft ed è possibile installare MSAL e trascrivere il codice correlato all'identità.  Per l'endpoint MSAL toobe toocommunicate in grado di hello v 2.0, è necessario tooprovide con alcune informazioni la registrazione dell'app.

* Iniziare aggiungendo MSAL toohello TodoListClient progetto utilizzando la Console di gestione pacchetti hello.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* Nel progetto TodoListClient hello aprire `app.config`.  Sostituire i valori hello elementi hello in hello `<appSettings>` hello tooreflect sezione valori di input nel portale di registrazione applicazione hello.  Il codice farà riferimento a questi valori ogni volta che userà MSAL.
  
  * Hello `ida:ClientId` è hello **Id applicazione** dell'app dal portale hello copiato.
* Nel progetto hello servizio elenco attività, aprire `web.config` nella directory radice del progetto hello hello.  
  
  * Sostituire hello `ida:Audience` stesso valore con hello **Id applicazione** dal portale hello.

## <a name="use-msal-tooget-tokens"></a>Utilizzare i token tooget MSAL
Hello principio fondamentale dietro MSAL è che ogni volta che è necessario un token di accesso dell'app, è sufficiente chiamare `app.AcquireToken(...)`, e MSAL hello rest.  

* In hello `TodoListClient` progetto, aprire `MainWindow.xaml.cs` e individuare hello `OnInitialized(...)` metodo.  innanzitutto Hello è tooinitialize dell'app `PublicClientApplication` -classe del MSAL principale che rappresenta le applicazioni native.  Si tratta in cui si passa MSAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* All'avvio dell'applicazione hello, si desidera toocheck e vedere se l'utente hello è già connesso in app hello.  Tuttavia, non vogliamo tooinvoke un'interfaccia utente Accedi ancora - ci accerteremo utente hello fare clic su "Accedi" toodo così.  Anche in hello `OnInitialized(...)` metodo:

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Se hello utente non è registrato e si fa clic pulsante "Accedi" hello, si desidera tooinvoke un account di accesso dell'interfaccia utente di utente hello immettere le proprie credenziali.  Implementare il gestore del pulsante hello Accedi:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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


}
```

* Se hello correttamente accesso dell'utente, MSAL riceverà e memorizzare nella cache un token per l'utente, ed è possibile procedere hello toocall `GetTodoList()` metodo con confidenza.  Tutto ciò che ha lasciato tooget attività dell'utente è hello tooimplement `GetTodoList()` metodo.

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Esegui
Congratulazioni. Ora disponibile un'applicazione WPF .NET con gli utenti di hello possibilità tooauthenticate funzionante & in modo sicuro chiamare le API Web mediante OAuth 2.0.  Eseguire entrambi i progetti e accedere con un account Microsoft personale oppure con un account aziendale o dell'istituto di istruzione.  Aggiungere l'elenco di attività dell'utente toothat di attività.  Disconnettersi e accedere di nuovo come un altro utente tooview proprio elenco di attività da eseguire.  Chiudere l'applicazione hello ed eseguirla nuovamente.  Si noti come hello sessione rimane invariata, perché l'applicazione hello memorizza nella cache i token in un file locale.

MSAL rende facile tooincorporate funzionalità comuni delle identità nell'app, tramite gli account personali e aziendali.  Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.  Ciò che occorre tooknow è una singola chiamata API, `app.AcquireTokenAsync(...)`.

Per riferimento, hello completata esempio (senza i valori di configurazione) [viene fornito come un file ZIP qui](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), oppure duplicarlo da GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Passaggi successivi
Ora è possibile passare ad argomenti più avanzati.  È opportuno tootry:

* [Protezione hello TodoListService Web API con endpoint v 2.0 hello](active-directory-v2-devquickstarts-dotnet-api.md)

Per altre risorse, vedere:  

* [Guida per sviluppatori v 2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow: tag "msal" &gt;&gt;](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

