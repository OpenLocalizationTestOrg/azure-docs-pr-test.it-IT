---
title: aaaAzure AD app a singola pagina AngularJS .NET v 2.0 introduzione | Documenti Microsoft
description: Come toobuild un'app angolare JS singola pagina che esegue l'accesso agli utenti con entrambi personale Microsoft account e di lavoro o scuola.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>Aggiungere app a singola pagina AngularJS Accedi tooan - .NET
In questo articolo verrà aggiunto accedere con app AngularJS tooan account Microsoft con tecnologia utilizzando hello Azure Active Directory v 2.0 endpoint.  endpoint v 2.0 Hello permette tooperform un'integrazione singola nell'app e autenticare gli utenti con account personali e di lavoro o dell'istituto di istruzione.

Questo esempio è una semplice app singola pagina di elenco che contiene le attività in un back-end API REST, scritto utilizzando hello MVC 4.5 di .NET framework e protetto tramite OAuth i token di connessione da Azure AD.  Hello app AngularJS utilizzerà la libreria di autenticazione JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello l'intero processo di accesso e acquisire i token per hello chiamata API REST.  Hello stesso modello può essere applicati tooauthenticate tooother le API REST, ad esempio hello [Microsoft Graph](https://graph.microsoft.com).

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Scaricare
tooget avviato, si sarà necessario toodownload & installazione di Visual Studio.  Sarà quindi possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lo scheletro di un'app:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

app scheletro Hello include tutto il codice boilerplate hello per un'app AngularJS semplice, ma mancano le parti relative alle identità hello.  Se non si desidera toofollow lungo, è possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) : esempio hello completata.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>Registrare un'app
Innanzitutto, creare un'app in hello [il portale di registrazione di App](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o attenersi alla seguente [passaggi dettagliati](active-directory-v2-app-registration.md).  Verificare di:

* Aggiungere hello **Web** piattaforma per l'app.
* Immettere hello corretto **URI di reindirizzamento**. valore predefinito di Hello per questo esempio è `https://localhost:44326/`.
* Lasciare hello **consentire flusso implicito** casella di controllo abilitato. 

Copia verso il basso hello **ID applicazione** app tooyour assegnato, sarà necessario immetterla a breve. 

## <a name="install-adaljs"></a>Installare adal.js
toostart, passare tooproject è stato scaricato e installato adal.js.  Se [bower](http://bower.io/) è installato, è sufficiente eseguire questo comando.  Per eventuali differenze tra le versioni di dipendenza, è sufficiente scegliere una versione successiva hello.

```
bower install adal-angular#experimental
```

In alternativa, è possibile scaricare manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Aggiungere entrambi i file toohello `app/lib/adal-angular-experimental/dist` directory di hello `TodoSPA` progetto.

Ora aprire hello progetto in Visual Studio e caricare adal.js alla fine di hello del corpo della pagina principale hello:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Impostare hello API REST
Mentre si configurazione in corso, iniziamo lavoro API REST di hello back-end.  Nella radice del progetto hello hello aprire `web.config` e sostituire hello `audience` valore.  API REST Hello verrà utilizzato questo token toovalidate valore riceve da app angolare hello per le richieste AJAX.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

Questo è tutto il tempo di hello Daremo toospend che illustrano il funzionamento hello API REST.  È gratuito toopoke nel codice hello, ma se si desidera toolearn ulteriori informazioni sulla protezione di web API con Azure AD, vedere [questo articolo](active-directory-v2-devquickstarts-dotnet-api.md). 

## <a name="sign-users-in"></a>Concedere l'accesso agli utenti
Tempo toowrite del codice di identità.  Come è possibile osservare, adal.js contiene un provider AngularJS, che funziona bene con il meccanismo di routing Angular.  Per iniziare, aggiungere hello modulo adal toohello app:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

È ora possibile inizializzare hello `adalProvider` con l'ID applicazione:

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

Grande, ora adal.js tutte le informazioni di hello deve toosecure gli utenti nell'applicazione e accedere.  accesso tooforce per una route specifica nell'app hello, tutto ciò che serve è una riga di codice:

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

Ora quando un utente fa clic hello `TodoList` collegamento, adal.js verrà reindirizzata automaticamente tooAzure Active Directory per l'accesso se necessario.  È anche possibile inviare in modo esplicito richieste di accesso e di disconnessione richiamando adal.js nei controller:

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a>Visualizzare le info utente
Ora che hello utente è connesso, è necessario probabilmente i dati di autenticazione tooaccess hello eseguito l'accesso dell'utente nell'applicazione.  Adal.js espone queste informazioni in hello `userInfo` oggetto.  tooaccess questo oggetto in una vista, aggiungere prima adal.js toohello di ambito di primo livello del controller corrispondente hello:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Quindi è possibile gestire direttamente hello `userInfo` oggetto nella visualizzazione: 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

È inoltre possibile utilizzare hello `userInfo` oggetto toodetermine se hello utente è connesso o non.

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a>Hello chiamata API REST
Infine, è ora tooget alcuni token e chiamare hello toocreate API REST, leggere, aggiornare ed eliminare le attività.  La novità è che  Non è toodo *una cosa*.  Adal.js eseguirà automaticamente il recupero, la memorizzazione nella cache e l'aggiornamento dei token.  Inoltre occuperà di associare tali token che toooutgoing AJAX richiede che si invia toohello API REST.  

Come funziona esattamente tutto questo? È tutto grazie toohello sorprendente [AngularJS intercettori](https://docs.angularjs.org/api/ng/service/$http), che consente di adal.js tootransform messaggi http in ingresso e in uscita.  Inoltre, adal.js si presuppone che tutte le richieste di invio toohello nello stesso dominio come finestra hello debba utilizzare i token destinati hello stesso ID applicazione come hello app AngularJS.  Ecco perché è stato usato hello stesso ID applicazione entrambi app angolare hello e hello NodeJS REST API.  Naturalmente, è possibile eseguire l'override di questo comportamento e indicare i token tooget adal.js per altre API REST, se necessario, ma per hello questo semplice scenario eseguirà le impostazioni predefinite.

Di seguito è riportato un frammento di codice che illustra come è facile richieste toosend con i token di connessione da Azure AD:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Congratulazioni.  A questo punto l'app a singola pagina integrata in Azure AD è completata.  Come è evidente,  È possibile autenticare gli utenti, in modo sicuro chiamare il relativo back-end API REST tramite OpenID Connect e ottenere le informazioni di base utente hello.  Viene fornita, hello supporta tutti gli utenti con un Account Microsoft personale o di un account di lavoro o dell'istituto di istruzione da Azure AD.  Eseguire app hello e in un browser passare troppo`https://localhost:44326/`.  Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione.  Aggiungere l'elenco di attività dell'utente di attività toohello e disconnettersi.  Provare ad accedere con hello altro tipo di account. Se è necessario un utenti di lavoro o dell'istituto di istruzione toocreate tenant di Azure AD, [informazioni su come una qui tooget](active-directory-howto-tenant.md) (è disponibile).

apprendendo endpoint v 2.0 hello, head tooour indietro toocontinue [Guida per sviluppatori v 2.0](active-directory-appmodel-v2-overview.md).  Per altre risorse, vedere:

* [Esempi di Azure in GitHub &gt;&gt;](https://github.com/Azure-Samples)
* [Azure AD in Stack Overflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Documentazione di Azure AD in [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Ottenere aggiornamenti della sicurezza per i prodotti
Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

