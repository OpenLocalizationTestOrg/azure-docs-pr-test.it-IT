---
title: aaaAzure AD per Windows Store introduzione | Documenti Microsoft
description: Compilare app di Windows Store che si integrano con Azure AD per la registrazione e per chiamare le API protette di Azure AD tramite il protocollo OAuth.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Integrare Azure AD con le app di Windows Store
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> I progetti di Windows Store 8.1 e della versione precedente non sono supportati in Visual Studio 2017.  Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Se si sviluppa App per Windows Store hello, Azure Active Directory (Azure AD) rende tooauthenticate semplici e diretti agli utenti con gli account di Active Directory. Grazie all'integrazione con Azure AD, un'app utilizzabile in modo sicuro da qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.

Per applicazioni desktop Windows Store che richiedono risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library (ADAL). Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget hello app. toodemonstrate facilmente, questo articolo illustra come toobuild un DirectorySearcher di Windows Store app che:

* Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Cerca in una directory gli utenti con un determinato nome dell'entità utente (UPN).
* Disconnette gli utenti.

## <a name="before-you-get-started"></a>Prima di iniziare
* Scaricare hello [scheletro di progetto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), o scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Ognuno è una soluzione di Visual Studio 2015.
* È inoltre necessario un tenant di Azure Active Directory in cui gli utenti toocreate e registra hello app. Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

Quando si è pronti, seguire le procedure di hello in hello prossime tre sezioni.

## <a name="step-1-register-hello-directorysearcher-app"></a>Passaggio 1: Registrare hello DirectorySearcher app
i token tooenable hello app tooget, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph. Ecco come:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. Quindi, in hello **Directory** elenco, in cui si desidera tooregister hello app tenant di Active Directory selezionare hello.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Seguire hello richieste toocreate un **applicazione Client nativa**.
  * **Nome** descrive toousers app hello.
  * **URI di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte. Immettere per ora un valore segnaposto, ad esempio **http://DirectorySearcher**. Il valore di hello verranno sostituiti in un secondo momento.
6. Dopo aver completato la registrazione di hello, Azure AD le assegna app hello un ID applicazione univoco. Copiare il valore di hello in hello **applicazione** scheda, perché sarà necessaria successivamente.
7. In hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.
8. Per hello **Azure Active Directory** app, selezionare **Microsoft Graph** come hello API.
9. In **autorizzazioni delegate**, aggiungere hello **directory hello accesso come utente connesso di hello** autorizzazione. In questo modo consente hello tooquery hello app API Graph per gli utenti.

## <a name="step-2-install-and-configure-adal"></a>Passaggio 2. Installare e configurare ADAL
Ora che si dispone di un'app in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità. tooenable toocommunicate ADAL con Azure AD, assegnargli alcune informazioni di registrazione dell'app hello.

1. Aggiungere il progetto di DirectorySearcher toohello ADAL tramite la Console di gestione pacchetti hello.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. Nel progetto DirectorySearcher hello, Apri il file MainPage.xaml.cs.
3. Sostituire i valori hello in hello **valori di configurazione** area con i valori hello immesso nel portale di Azure hello. Il codice si riferisce valori toothese ogni volta che usa ADAL.
  * Hello *tenant* hello dominio del tenant di Azure Active Directory (ad esempio, contoso.onmicrosoft.com).
  * Hello *clientId* hello client ID dell'applicazione hello, che copiato dal portale di hello.
4. URI di callback hello toodiscover è ora necessario per l'app di Windows Store. Impostare un punto di interruzione in questa riga hello `MainPage` metodo:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Compilare la soluzione hello, assicurarsi che vengano ripristinati tutti i riferimenti del pacchetto. Se tutti i pacchetti sono mancanti, aprire Gestione pacchetti NuGet hello e ripristinarli.
6. Eseguire app hello e copiare il valore di hello di `redirectUri` quando hello punto di interruzione. il valore di Hello dovrebbe essere simile alla seguente hello:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. In hello **impostazioni** scheda dell'app hello in hello portale di Azure, aggiungere un **RedirectUri** con hello valore precedente.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Passaggio 3: I token usare ADAL tooget da Azure AD
Hello principio fondamentale dietro ADAL è che ogni volta che l'applicazione hello necessita di un token di accesso, chiama semplicemente `authContext.AcquireToken(…)`, e ADAL hello rest.  

1. Inizializzazione dell'applicazione hello `AuthenticationContext`, ovvero hello classe principale della libreria ADAL. Questa azione passa coordinate hello ADAL necessarie toocommunicate con Azure AD e indicare come token toocache.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Individuare hello `Search(...)` metodo, che viene richiamato quando gli utenti fanno clic hello **ricerca** pulsante nell'interfaccia utente dell'applicazione hello. Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta get per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato. hello tooquery API Graph, includere un token di accesso nella richiesta di hello **autorizzazione** intestazione. È qui che entra in gioco ADAL.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Quando richiede un token di app hello chiamando `AcquireTokenAsync(...)`, ADAL tenta tooreturn un token senza chiedere utente hello per le credenziali. Se ADAL rileva che l'utente hello toosign in tooget un token, visualizza una finestra di dialogo di accesso, raccoglie le credenziali dell'utente hello e restituisce un token dopo l'autenticazione ha esito positivo. Se la libreria ADAL è Impossibile tooreturn un token per qualsiasi motivo, hello *AuthenticationResult* lo stato è un errore.
3. È ora token di accesso di tempo toouse hello acquisita. Anche in hello `Search(...)` (metodo), collegare toohello di hello token API Graph richiesta di recupero in hello **autorizzazione** intestazione:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. È possibile utilizzare hello `AuthenticationResult` toodisplay informazioni utente hello in app hello, ad esempio hello ID utente dell'oggetto:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. È anche possibile utilizzare toosign ADAL utenti all'esterno dell'app hello. Quando hello scelto hello **Sign Out** , verificare che chiamano Avanti hello troppo`AcquireTokenAsync(...)` viene illustrata una visualizzazione di accesso. Con ADAL, questa azione è semplice come la cancellazione della cache dei token hello:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Passaggi successivi
È ora disponibile un'app di Windows Store che può autenticare gli utenti, in modo sicuro chiamare web API mediante OAuth 2.0 e ottenere le informazioni di base utente hello funzionante.

Se non sono stati già popolato il tenant con gli utenti, è pertanto toodo ora hello.
1. Eseguire l'app DirectorySearcher e quindi accedere con uno degli utenti hello.
2. Cercare altri utenti in base al relativo UPN.
3. Chiudere l'applicazione hello ed eseguirla di nuovo. Si noti come hello sessione rimane invariata.
4. Disconnessione facendo toodisplay hello barra inferiore e quindi eseguire nuovamente l'accesso con un altro utente.

ADAL rende facile tooincorporate tutte queste funzionalità di identità comuni in app hello. Si occupa di tutto il lavoro dirty hello, quali la gestione della cache, supporto del protocollo OAuth, presentate utente hello con interfaccia utente, un account di accesso e aggiornamento scaduto token. È necessario tooknow solo una singola API chiamata, `authContext.AcquireToken*(…)`.

Per riferimento, scaricare hello [esempio completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (senza i valori di configurazione).

È possibile procedere in scenari con identità tooadditional. Provare ad esempio [Proteggere un'API Web .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
