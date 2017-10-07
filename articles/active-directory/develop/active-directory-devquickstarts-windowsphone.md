---
title: Guida introduttiva di Windows Phone AD aaaAzure | Documenti Microsoft
description: Toobuild un'applicazione Windows Phone che si integra con Azure AD per l'accesso di Azure AD come protetto tramite OAuth API.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Integrare Azure AD con un'app di Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> I progetti Windows Phone 8.1 e versioni precedenti non sono supportati in Visual Studio 2017.  Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Se si sta sviluppando un'app di Windows Phone 8.1, Azure AD rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory.  Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.

> [!NOTE]
> Questo esempio di codice usa ADAL versione 2.0.  Per la tecnologia più recente di hello, è possibile provare a tooinstead nostri [esercitazione di Windows universale usando v 3.0 ADAL](active-directory-devquickstarts-windowsstore.md).  Se si tratta effettivamente di un'app per Windows Phone 8.1, è giusto hello.  ADAL v 2.0 è ancora completamente supportata e hello modo consigliato di agianst lo sviluppo di App Windows Phone 8.1 Usa Azure AD.
> 
> 

Per .NET native client che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library o ADAL.  Obiettivo esclusivo della libreria ADAL è toomake è più facile per i token di accesso tooget app.  la semplicità è, toodemonstrate qui, verrà creata una "ricerca di Directory" app di Windows Phone 8.1:

* Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Cerca in una directory gli utenti con un determinato UPN.
* Disconnette gli utenti.

toobuild hello completo lavoro dell'applicazione, è necessario:

1. Registrare l'applicazione con Azure AD.
2. Installare e configurare ADAL.
3. Usare i token ADAL tooget da Azure AD.

tooget avviato, [scaricare un progetto di base](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Ognuno è una soluzione di Visual Studio 2013.  Sarà necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.  Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Registrare l'applicazione di funzione di ricerca di Directory hello
tooenable token tooget app, è prima necessario tooregister tenant in Azure AD e concedergli hello tooaccess autorizzazione API Azure AD Graph:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.
4. Fare clic su **App registrations (Registrazioni app)** e scegliere **Aggiungi**.
5. Seguire le istruzioni di hello e creare un nuovo **applicazione Client nativa**.
  * Hello **nome** di hello applicazione descriverà tooend utenti applicazione
  * Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD utilizzerà le risposte token tooreturn.  Per ora immettere un valore segnaposto, ad esempio `http://DirectorySearcher`.  Questo valore verrà sostituito in un secondo momento.
6. Dopo avere completato la registrazione, AAD assegnerà all'app un ID app univoco.  È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.
7. Da hello **impostazioni** pagina, scegliere **autorizzazioni obbligatorie** e scegliere **Aggiungi**. Seleziona hello **Microsoft Graph** come hello API e aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.  In questo modo hello di tooquery l'applicazione API Graph per gli utenti.

## <a name="2-install--configure-adal"></a>2. Installare e configurare ADAL
Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.  Affinché toocommunicate in grado di toobe ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.

* Inizia ad aggiungere il progetto di DirectorySearcher toohello ADAL utilizzando Console Gestione pacchetti hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Nel progetto DirectorySearcher hello aprire `MainPage.xaml.cs`.  Sostituire i valori hello in hello `Config Values` hello tooreflect area valori input in hello portale di Azure.  Il codice farà riferimento a questi valori ogni volta che userà ADAL.
  * Hello `tenant` dominio hello del tenant di Azure AD, ad esempio contoso.onmicrosoft.com
  * Hello `clientId` è clientId hello dell'applicazione copiata dal portale hello.
* Uri di callback toodiscover hello è ora necessario per l'app di Windows Phone.  Impostare un punto di interruzione in questa riga hello `MainPage` metodo:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Eseguire app hello e copiare riservato valore hello `redirectUri` quando hello punto di interruzione.  Dovrebbe essere simile a

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* In hello **configura** scheda dell'applicazione nel portale di gestione di Azure, hello sostituire il valore di hello di hello **RedirectUri** con questo valore.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Usare ADAL tooGet token da Azure Active Directory
Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente `authContext.AcquireToken(…)`, e ADAL hello rest.  

* primo passaggio Hello è tooinitialize dell'app `AuthenticationContext` -ADAL della classe primaria.  Si tratta in cui si passa ADAL hello coordinate necessarie toocommunicate con Azure AD e specificare la modalità token toocache.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Ora individuare hello `Search(...)` metodo, che verrà richiamato quando hello utente cliks hello "Ricerca" pulsante nell'interfaccia utente dell'applicazione hello.  Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.  Ma in hello tooquery ordine API Graph, è necessario tooinclude access_token in hello `Authorization` richiesta di intestazione di hello - si tratta in cui è disponibile in ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Se è necessaria l'autenticazione interattiva, ADAL utilizzerà Web l'autenticazione di Service Broker (Rubrica di Windows Phone) e [modello continuazione](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD nella pagina di accesso.  Quando l'accesso dell'utente hello, l'app deve risultati hello ADAL toopass di interazione della Rubrica di Windows hello.  Questo è semplice come l'implementazione di hello `ContinueWebAuthentication` interfaccia:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Ora è hello toouse ora `AuthenticationResult` che ADAL restituito tooyour app.  In hello `QueryGraph(...)` callback, collegare access_token hello è stato acquistato toohello GET richiesta nell'intestazione di autorizzazione hello:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* È inoltre possibile utilizzare hello `AuthenticationResult` toodisplay informazioni utente hello nell'app dell'oggetto. In hello `QueryGraph(...)` metodo, utilizzare hello risultato tooshow hello l'id dell'utente nella pagina hello:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Infine, è possibile utilizzare utente hello toosign ADAL fuori anche dall'applicazione.  Quando l'utente hello fa clic sul pulsante "Sign Out" hello, si vuole tooensure che hello chiamata successiva troppo`AcquireTokenSilentAsync(...)` avrà esito negativo.  Con ADAL, non è semplice come la cancellazione della cache dei token hello:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Congratulazioni. È ora un'app di Windows Phone con gli utenti di hello possibilità tooauthenticate funzionante, in modo sicuro chiamare le API Web mediante OAuth 2.0 e ottenere le informazioni di base utente hello.  Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.  Eseguire l'app DirectorySearcher e accedere con uno di tali utenti.  Cercare altri utenti in base al relativo UPN.  Chiudere l'applicazione hello ed eseguirla nuovamente.  Si noti come hello sessione rimane invariata.  Disconnettersi e accedere nuovamente come un altro utente.

ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.  Si occupa di tutto il lavoro dirty hello automaticamente - gestione della cache, supporto del protocollo OAuth, presentate utente hello con un account di accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.  Ciò che occorre tooknow è una singola chiamata API, `authContext.AcquireToken*(…)`.

Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) [qui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  È possibile procedere in scenari con identità tooadditional.  È opportuno tootry:

[Proteggere un'API Web .NET con Azure AD >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

