---
title: aaaAzure AD AngularJS introduzione | Documenti Microsoft
description: Come un'applicazione a pagina singola AngularJS toobuild che si integra con Azure AD per l'accesso e chiama le API di protetto AD Azure tramite OAuth.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Proteggere le app AngularJS a singola pagina con Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) rende semplice e diretto per si tooadd accesso, disconnessione, e chiamate all'API OAuth sicura tooyour applicazioni a pagina singola.  Consente agli utenti di tooauthenticate App con gli account di Windows Server Active Directory e utilizzare qualsiasi API Azure AD consente di proteggere, ad esempio hello API di Office 365 o hello Azure API web.

Per le applicazioni JavaScript in esecuzione in un browser, Azure Active Directory fornisce hello Active Directory Authentication Library (ADAL) o adal.js. Hello unico scopo del adal.js è toomake è più facile per i token di accesso tooget app. la semplicità è, toodemonstrate qui, verrà creata una tooDo AngularJS applicazione elenco:

* Utente di hello segni toohello App usando Azure AD come provider di identità hello.

* Consente di visualizzare alcune informazioni sull'utente hello.
* Le chiamate in modo sicuro hello tooDo dell'app API di elenco con i token di connessione da Azure AD.
* Segni di hello utente all'esterno dell'app hello.

un'applicazione toobuild hello completato, lavoro, è necessario:

1. Registrare l'app con Azure AD.
2. ADAL di installare e configurare l'applicazione a una pagina hello.
3. Utilizzare pagine protette toohelp ADAL nell'app a pagina singola hello.

tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione. Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Passaggio 1: Registrare un'applicazione hello DirectorySearcher
tooenable app tooauthenticate utenti e i token get, è necessario innanzitutto tooregister tenant in Azure AD:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Se si accede alla directory toomultiple, potrebbe essere visualizzato directory corretta hello tooensure. toodo in tal caso, nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Seguire le istruzioni di hello e creare una nuova applicazione web e/o API web:
  * **Nome** descrive toousers l'applicazione.
  * **Uri di reindirizzamento** toowhich percorso hello Azure AD restituirà i token. il percorso predefinito Hello per questo esempio è `https://localhost:44326/`.
6. Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco.  È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.
7. Adal.js Usa hello OAuth flusso implicito toocommunicate con Azure AD. Per l'applicazione, è necessario abilitare il flusso implicito hello:
  1. Fare clic su un'applicazione hello e selezionare **manifesto** editor del manifesto tooopen hello inline.
  2. Individuare hello `oauth2AllowImplicitFlow` proprietà. Impostare il relativo valore troppo`true`.
  3. Fare clic su **salvare** manifesto hello toosave.
8. Concedere le autorizzazioni nel tenant per l'applicazione. Andare troppo**impostazioni** > **proprietà** > **autorizzazioni obbligatorie**, fare clic su hello **concedere autorizzazioni**pulsante nella barra superiore hello. Fare clic su **Sì** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Passaggio 2: Installare ADAL e configurare l'applicazione a una pagina hello
Ora che si dispone di un'applicazione in Azure AD, è possibile installare adal.js e scrivere il codice relativo all'identità.

### <a name="configure-hello-javascript-client"></a>Configurare i client JavaScript hello
Inizia ad aggiungere adal.js toohello TodoSPA progetto utilizzando la Console di gestione pacchetti hello:
  1. Scaricare [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e aggiungerlo toohello `App/Scripts/` directory del progetto.
  2. Scaricare [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e aggiungerlo toohello `App/Scripts/` directory del progetto.
  3. Caricare ogni script entro hello hello `</body>` in `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Configurare i server back-end hello
Per back-end tooDo API elenco tooaccept i token dell'applicazione a pagina singola hello da browser hello, back-end hello richiede informazioni di configurazione di registrazione dell'app hello. Nel progetto TodoSPA hello aprire `web.config`. Sostituire i valori hello elementi hello in hello `<appSettings>` hello di sezione tooreflect valori hello utilizzata nel portale di Azure. Il codice farà riferimento a questi valori ogni volta che userà ADAL.
  * `ida:Tenant`è il dominio di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.
  * `ida:Audience`è l'ID client hello dell'applicazione copiata dal portale hello.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Passaggio 3: Usare ADAL toohelp sicura pagine hello a pagina singola app
Adal.js si integra con i provider di route e HTTP AngularJS e permette di proteggere visualizzazioni individuali nell'app a singola pagina.

1. In `App/Scripts/app.js`, importare il modulo di adal.js hello:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Inizializzare `adalProvider` utilizzando i valori di configurazione hello della registrazione dell'applicazione, anche in `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Guida in linea protetta hello `TodoList` Visualizza nell'app hello usando solo una riga di codice: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Riepilogo
È ora disponibile un'applicazione a pagina singola protetta che può accedere gli utenti e rilasciare l'API di back-end tooits le richieste di token di connessione protetta. Quando un utente fa clic hello **TodoList** collegamento, adal.js verrà reindirizzata automaticamente tooAzure Active Directory per l'accesso se necessario. Inoltre, adal.js collegherà automaticamente un accesso token tooany che le richieste Ajax back-end dell'app toohello inviati.  

Hello passaggi precedenti sono hello bare minimo necessario toobuild un'applicazione a singola pagina utilizzando adal.js. Tuttavia sono disponibili altre funzionalità utili nelle app a singola pagina:

* è possibile definire funzioni nei controller di che richiamano adal.js tooexplicitly emettere richieste di accesso e disconnessione.  In `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Le informazioni utente toopresent nell'interfaccia utente dell'applicazione hello. Hello ADAL servizio è già stato aggiunto toohello `userDataCtrl` controller, pertanto è possibile accedere hello `userInfo` oggetto hello associata visualizzazione `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Esistono molti scenari in cui è opportuno tooknow se hello utente è connesso o non. È inoltre possibile utilizzare hello `userInfo` oggetto toogather queste informazioni.  Ad esempio, in `index.html`, è possibile visualizzare entrambi hello **accesso** o **Logout** pulsante in base allo stato di autenticazione:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

L'app Azure a pagina singola integrata in Active Directory può autenticare gli utenti, in modo sicuro chiamare il relativo back-end tramite OAuth 2.0 e ottenere le informazioni di base utente hello. Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti. Eseguire l'app di una pagina di elenco tooDo e accedere con uno di tali utenti. Aggiungere l'elenco di attività dell'utente di attività toohello, disconnettersi e accedere di nuovo.

Adal.js rende facile tooincorporate funzionalità comuni delle identità nell'applicazione. Si occupa di tutto il lavoro dirty hello per l'utente: gestione della cache, supporto del protocollo OAuth, presentate utente hello con un'accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.

Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Passaggi successivi
È possibile procedere con tooadditional scenari. Potrebbe essere necessario tootry: [chiamare un'API web CORS da un'applicazione a pagina singola](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
