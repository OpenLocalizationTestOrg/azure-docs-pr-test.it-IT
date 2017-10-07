---
title: aaaAzure AD Xamarin introduzione | Documenti Microsoft
description: Compilare un'applicazione Xamarin che si integra con Azure AD per l'accesso e chiama le API protette da Azure AD usando OAuth.
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Integrare Azure AD in app Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Xamarin consente di scrivere app per dispositivi mobili in C# che possono essere eseguite in iOS, Android e Windows, in dispositivi mobili e PC. Se si sta creando un'app con Xamarin, Azure Active Directory (Azure AD) consente agli utenti di tooauthenticate semplice con gli account di Azure AD. applicazione Hello utilizzabile anche in modo sicuro da qualsiasi API web protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.

Per le app Xamarin che necessitano di risorse tooaccess protetto da Azure AD fornisce hello Active Directory Authentication Library (ADAL). Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget app. toodemonstrate facilmente, questo articolo viene illustrato come le app DirectorySearcher toobuild che:

* Viene eseguita in iOS, Android, Windows Desktop, Windows Phone e Windows Store.
* Utilizzare una singola classe portabile libreria (PCL) tooauthenticate utenti e di ottenere token per hello API Azure AD Graph.
* Cerca in una directory gli utenti con un determinato UPN.

## <a name="before-you-get-started"></a>Prima di iniziare
* Scaricare hello [scheletro di progetto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Ognuno è una soluzione di Visual Studio 2013.
* È inoltre necessario un tenant di Azure Active Directory in cui gli utenti toocreate e registra hello app. Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

Quando si è pronti, seguire le procedure di hello in hello quattro sezioni.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Passaggio 1: Configurare l'ambiente di sviluppo Xamarin
Dal momento che questa esercitazione include progetti per iOS, Android e Windows, sono necessari sia Visual Studio che Xamarin. ambiente necessarie toocreate hello, il processo di completamento hello in [impostare backup e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) su MSDN. istruzioni di Hello includono materiale che è possibile esaminare informazioni su Xamarin toolearn durante l'attesa per hello installazioni toobe completato.

Dopo aver completato l'installazione di hello, aprire la soluzione hello in Visual Studio. Sono presenti sei progetti: cinque progetti specifici delle piattaforme e una libreria di classi portabile, DirectorySearcher.cs, che verrà condivisa tra tutte le piattaforme.

## <a name="step-2-register-hello-directorysearcher-app"></a>Passaggio 2: Registrare hello DirectorySearcher app
i token tooenable hello app tooget, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph. Ecco come:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. Quindi, in hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. toocreate un nuovo **applicazione Client nativa**, seguire le istruzioni di hello.
  * **Nome** descrive toousers app hello.
  * **URI di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte. Immettere un valore, ad esempio http://DirectorySearcher.
6. Dopo aver completato la registrazione, Azure AD le assegna app hello un ID applicazione univoco. Copiare il valore di hello hello **applicazione** scheda, perché sarà necessaria successivamente.
7. In hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.
8. Selezionare **Microsoft Graph** come hello API. In **autorizzazioni delegate**, aggiungere hello **lettura dati Directory** autorizzazione.  
Questa azione Abilita hello tooquery hello app API Graph per gli utenti.

## <a name="step-3-install-and-configure-adal"></a>Passaggio 3: Installare e configurare ADAL
Ora che si dispone di un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità. tooenable toocommunicate ADAL con Azure AD, assegnargli alcune informazioni di registrazione dell'app hello.

1. Aggiungere il progetto di DirectorySearcher toohello ADAL tramite la Console di gestione pacchetti hello.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    Si noti che i due riferimenti alla libreria vengono aggiunti progetto tooeach: hello PCL parte ADAL e una parte specifica della piattaforma.
2. Nel progetto DirectorySearcherLib hello aprire DirectorySearcher.cs.
3. Sostituire i valori dei membri di classe hello con valori di hello immesso nel portale di Azure hello. Il codice si riferisce valori toothese ogni volta che usa ADAL.

  * Hello *tenant* hello dominio del tenant di Azure Active Directory (ad esempio, contoso.onmicrosoft.com).
  * Hello *clientId* hello client ID dell'applicazione hello, che copiato dal portale di hello.
  * Hello *returnUri* è hello reindirizzamento URI immesso nel portale di hello (ad esempio, http://DirectorySearcher).

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Passaggio 4: I token usare ADAL tooget da Azure AD
Quasi tutta la logica di autenticazione dell'applicazione hello si trova `DirectorySearcher.SearchByAlias(...)`. Tutto ciò che è necessario nei progetti specifici della piattaforma hello è toopass toohello un parametro contestuali `DirectorySearcher` PCL.

1. Aprire DirectorySearcher.cs e quindi aggiungere un nuovo toohello parametro `SearchByAlias(...)` metodo. `IPlatformParameters`è che l'autenticazione hello tooperform ADAL esigenze di oggetti parametro hello contestuali che incapsula hello specifico della piattaforma.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Inizializzare `AuthenticationContext`, ovvero hello classe principale della libreria ADAL.  
Hello ADAL di passaggi di questa azione è coordinate toocommunicate esigenze con Azure AD.
3. Chiamare `AcquireTokenAsync(...)`, che accetta hello `IPlatformParameters` dell'oggetto e richiama il flusso di autenticazione hello che è necessario tooreturn un'app toohello token.

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`primo tentativi tooreturn un token per hello richiesto risorsa (Buongiorno API Graph in questo caso) senza chiedere conferma tooenter agli utenti le proprie credenziali (tramite la memorizzazione nella cache o l'aggiornamento di un token precedente). Se necessario, viene prima di acquisire token richiesto hello utenti hello Azure AD nella pagina di accesso.
4. Collegare una richiesta all'API Graph toohello token accesso hello in hello **autorizzazione** intestazione:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Questo è tutto per hello `DirectorySearcher` codice relative alle identità PCL e hello dell'app. È comunque toocall hello `SearchByAlias(...)` metodo nelle visualizzazioni di ciascuna piattaforma e, se necessario, tooadd codice per la gestione corretta di hello del ciclo di vita dell'interfaccia utente.

### <a name="android"></a>Android
1. In Mainactivity, aggiungere una chiamata troppo`SearchByAlias(...)` nel pulsante hello gestore click:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Eseguire l'override di hello `OnActivityResult` del ciclo di vita metodo tooforward alcuna autenticazione reindirizza toohello indietro di metodo appropriato. ADAL fornisce un apposito metodo helper in Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Desktop di Windows
In MainWindow.xaml.cs, effettuare una chiamata troppo`SearchByAlias(...)` passando un `WindowInteropHelper` in desktop hello `PlatformParameters` oggetto:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` oggetto assume un toohello riferimento View Controller:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
In Windows universale, Apri il file MainPage.xaml.cs e quindi implementare hello `Search` metodo. Questo metodo Usa un metodo di supporto in un progetto condiviso tooupdate dell'interfaccia utente, in base alle esigenze.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Passaggi successivi
È stata compilata un'app Xamarin funzionante che può autenticare gli utenti e chiamare in modo sicuro le API Web usando OAuth 2.0 in cinque diverse piattaforme.

Se non sono stati già popolato il tenant con gli utenti, è pertanto toodo ora hello.

1. Eseguire l'app DirectorySearcher e quindi accedere con uno degli utenti hello.
2. Cercare altri utenti in base al relativo UPN.

ADAL lo rende facile tooincorporate funzionalità comuni delle identità applicazione hello. Si occupa di tutto il lavoro dirty hello, quali la gestione della cache, supporto del protocollo OAuth, presentate utente hello con interfaccia utente, un account di accesso e aggiornamento scaduto token. È necessario tooknow solo una singola API chiamata, `authContext.AcquireToken*(…)`.

Per riferimento, scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (senza i valori di configurazione).

È possibile procedere in scenari con identità tooadditional. Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
