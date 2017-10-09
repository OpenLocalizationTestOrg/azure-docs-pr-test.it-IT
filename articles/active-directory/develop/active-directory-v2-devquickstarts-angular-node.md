---
title: v 2.0 aaaAzure AD app a singola pagina NodeJS AngularJS introduzione | Documenti Microsoft
description: Come toobuild un'app angolare JS singola pagina che esegue l'accesso agli utenti con entrambi personale Microsoft account e di lavoro o scuola.
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="79687-103">Aggiungere app a singola pagina AngularJS Accedi tooan - NodeJS</span><span class="sxs-lookup"><span data-stu-id="79687-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="79687-104">In questo articolo verrà aggiunto accedere con app AngularJS tooan account Microsoft con tecnologia utilizzando hello Azure Active Directory v 2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="79687-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="79687-105">endpoint di Hello v 2.0 consentono tooperform un'integrazione singola nell'app e autenticare gli utenti con account personali e di lavoro o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="79687-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="79687-106">Questo esempio è una semplice app a pagina singola To-Do List che archivia le attività in un'API REST back-end, scritta in NodeJS e protetta con i token di connessione OAuth di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79687-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="79687-107">Hello app AngularJS utilizzerà la libreria di autenticazione JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello l'intero processo di accesso e acquisire i token per hello chiamata API REST.</span><span class="sxs-lookup"><span data-stu-id="79687-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="79687-108">Hello stesso modello può essere applicati tooauthenticate tooother le API REST, ad esempio hello [Microsoft Graph](https://graph.microsoft.com) o hello le API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="79687-109">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="79687-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="79687-110">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="79687-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="79687-111">Scaricare</span><span class="sxs-lookup"><span data-stu-id="79687-111">Download</span></span>
<span data-ttu-id="79687-112">tooget avviato, è necessario toodownload & installazione [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="79687-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="79687-113">Sarà quindi possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) lo scheletro di un'app:</span><span class="sxs-lookup"><span data-stu-id="79687-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="79687-114">app scheletro Hello include tutto il codice boilerplate hello per un'app AngularJS semplice, ma mancano le parti relative alle identità hello.</span><span class="sxs-lookup"><span data-stu-id="79687-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="79687-115">Se non si desidera toofollow lungo, è possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) : esempio hello completata.</span><span class="sxs-lookup"><span data-stu-id="79687-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="79687-116">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="79687-116">Register an app</span></span>
<span data-ttu-id="79687-117">Innanzitutto, creare un'app in hello [il portale di registrazione di App](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o attenersi alla seguente [passaggi dettagliati](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="79687-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="79687-118">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="79687-118">Make sure to:</span></span>

* <span data-ttu-id="79687-119">Aggiungere hello **Web** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="79687-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="79687-120">Immettere hello corretto **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="79687-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="79687-121">valore predefinito di Hello per questo esempio è `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="79687-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="79687-122">Lasciare hello **consentire flusso implicito** casella di controllo abilitato.</span><span class="sxs-lookup"><span data-stu-id="79687-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="79687-123">Copia verso il basso hello **ID applicazione** app tooyour assegnato, sarà necessario immetterla a breve.</span><span class="sxs-lookup"><span data-stu-id="79687-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="79687-124">Installare adal.js</span><span class="sxs-lookup"><span data-stu-id="79687-124">Install adal.js</span></span>
<span data-ttu-id="79687-125">toostart, passare tooproject è stato scaricato e installato adal.js.</span><span class="sxs-lookup"><span data-stu-id="79687-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="79687-126">Se [bower](http://bower.io/) è installato, è sufficiente eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="79687-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="79687-127">Per eventuali differenze tra le versioni di dipendenza, è sufficiente scegliere una versione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="79687-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="79687-128">In alternativa, è possibile scaricare manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="79687-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="79687-129">Aggiungere entrambi i file toohello `app/lib/adal-angular-experimental/dist` directory.</span><span class="sxs-lookup"><span data-stu-id="79687-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="79687-130">Ora aprire progetto hello in un editor di testo e caricare adal.js alla fine di hello del corpo della pagina hello:</span><span class="sxs-lookup"><span data-stu-id="79687-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="79687-131">Impostare hello API REST</span><span class="sxs-lookup"><span data-stu-id="79687-131">Set up hello REST API</span></span>
<span data-ttu-id="79687-132">Mentre si configurazione in corso, consente di utilizzo di API REST get hello back-end.</span><span class="sxs-lookup"><span data-stu-id="79687-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="79687-133">In un prompt dei comandi, installare tutti i pacchetti necessari hello eseguendo (assicurarsi di essere nella directory di primo livello di progetto hello hello):</span><span class="sxs-lookup"><span data-stu-id="79687-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="79687-134">Aprire quindi `config.js` e sostituire hello `audience` valore:</span><span class="sxs-lookup"><span data-stu-id="79687-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="79687-135">API REST Hello verrà utilizzato questo token toovalidate valore riceve da app angolare hello per le richieste AJAX.</span><span class="sxs-lookup"><span data-stu-id="79687-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="79687-136">Si noti che questa API REST semplice archivia dati in memoria, pertanto, ogni server hello toostop di tempo, si perderanno tutte le attività create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="79687-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="79687-137">Questo è tutto il tempo di hello Daremo toospend che illustrano il funzionamento hello API REST.</span><span class="sxs-lookup"><span data-stu-id="79687-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="79687-138">È gratuito toopoke nel codice hello, ma se si desidera toolearn ulteriori informazioni sulla protezione di web API con Azure AD, vedere [questo articolo](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="79687-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="79687-139">Concedere l'accesso agli utenti</span><span class="sxs-lookup"><span data-stu-id="79687-139">Sign users in</span></span>
<span data-ttu-id="79687-140">Tempo toowrite del codice di identità.</span><span class="sxs-lookup"><span data-stu-id="79687-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="79687-141">Come è possibile osservare, adal.js contiene un provider AngularJS, che funziona bene con il meccanismo di routing Angular.</span><span class="sxs-lookup"><span data-stu-id="79687-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="79687-142">Per iniziare, aggiungere hello modulo adal toohello app:</span><span class="sxs-lookup"><span data-stu-id="79687-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="79687-143">È ora possibile inizializzare hello `adalProvider` con l'ID applicazione:</span><span class="sxs-lookup"><span data-stu-id="79687-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="79687-144">Grande, ora adal.js tutte le informazioni di hello deve toosecure gli utenti nell'applicazione e accedere.</span><span class="sxs-lookup"><span data-stu-id="79687-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="79687-145">accesso tooforce per una route specifica nell'app hello, tutto ciò che serve è una riga di codice:</span><span class="sxs-lookup"><span data-stu-id="79687-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="79687-146">Ora quando un utente fa clic hello `TodoList` collegamento, adal.js verrà reindirizzata automaticamente tooAzure Active Directory per l'accesso se necessario.</span><span class="sxs-lookup"><span data-stu-id="79687-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="79687-147">È anche possibile inviare in modo esplicito richieste di accesso e di disconnessione richiamando adal.js nei controller:</span><span class="sxs-lookup"><span data-stu-id="79687-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="79687-148">Visualizzare le info utente</span><span class="sxs-lookup"><span data-stu-id="79687-148">Display user info</span></span>
<span data-ttu-id="79687-149">Ora che hello utente è connesso, è necessario probabilmente i dati di autenticazione tooaccess hello eseguito l'accesso dell'utente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="79687-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="79687-150">Adal.js espone queste informazioni in hello `userInfo` oggetto.</span><span class="sxs-lookup"><span data-stu-id="79687-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="79687-151">tooaccess questo oggetto in una vista, aggiungere prima adal.js toohello di ambito di primo livello del controller corrispondente hello:</span><span class="sxs-lookup"><span data-stu-id="79687-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="79687-152">Quindi è possibile gestire direttamente hello `userInfo` oggetto nella visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="79687-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="79687-153">È inoltre possibile utilizzare hello `userInfo` oggetto toodetermine se hello utente è connesso o non.</span><span class="sxs-lookup"><span data-stu-id="79687-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="79687-154">Hello chiamata API REST</span><span class="sxs-lookup"><span data-stu-id="79687-154">Call hello REST API</span></span>
<span data-ttu-id="79687-155">Infine, è ora tooget alcuni token e chiamare hello toocreate API REST, leggere, aggiornare ed eliminare le attività.</span><span class="sxs-lookup"><span data-stu-id="79687-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="79687-156">La novità è che</span><span class="sxs-lookup"><span data-stu-id="79687-156">Well guess what?</span></span>  <span data-ttu-id="79687-157">Non è toodo *una cosa*.</span><span class="sxs-lookup"><span data-stu-id="79687-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="79687-158">Adal.js eseguirà automaticamente il recupero, la memorizzazione nella cache e l'aggiornamento dei token.</span><span class="sxs-lookup"><span data-stu-id="79687-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="79687-159">Inoltre occuperà di associare tali token che toooutgoing AJAX richiede che si invia toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="79687-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="79687-160">Come funziona esattamente tutto questo?</span><span class="sxs-lookup"><span data-stu-id="79687-160">How exactly does this work?</span></span> <span data-ttu-id="79687-161">È tutto grazie toohello sorprendente [AngularJS intercettori](https://docs.angularjs.org/api/ng/service/$http), che consente di adal.js tootransform messaggi http in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="79687-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="79687-162">Inoltre, adal.js si presuppone che tutte le richieste di invio toohello nello stesso dominio come finestra hello debba utilizzare i token destinati hello stesso ID applicazione come hello app AngularJS.</span><span class="sxs-lookup"><span data-stu-id="79687-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="79687-163">Ecco perché è stato usato hello stesso ID applicazione entrambi app angolare hello e hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="79687-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="79687-164">Naturalmente, è possibile eseguire l'override di questo comportamento e indicare i token tooget adal.js per altre API REST, se necessario, ma per hello questo semplice scenario eseguirà le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="79687-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="79687-165">Di seguito è riportato un frammento di codice che illustra come è facile richieste toosend con i token di connessione da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="79687-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="79687-166">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="79687-166">Congratulations!</span></span>  <span data-ttu-id="79687-167">A questo punto l'app a singola pagina integrata in Azure AD è completata.</span><span class="sxs-lookup"><span data-stu-id="79687-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="79687-168">Come è evidente,</span><span class="sxs-lookup"><span data-stu-id="79687-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="79687-169">È possibile autenticare gli utenti, in modo sicuro chiamare il relativo back-end API REST tramite OpenID Connect e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="79687-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="79687-170">Viene fornita, hello supporta tutti gli utenti con un Account Microsoft personale o di un account di lavoro o dell'istituto di istruzione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79687-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="79687-171">Provare app hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="79687-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="79687-172">In un browser passare troppo`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="79687-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="79687-173">Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="79687-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="79687-174">Aggiungere l'elenco di attività dell'utente di attività toohello e disconnettersi.  Provare ad accedere con hello altro tipo di account.</span><span class="sxs-lookup"><span data-stu-id="79687-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="79687-175">Se è necessario un utenti di lavoro o dell'istituto di istruzione toocreate tenant di Azure AD, [informazioni su come una qui tooget](active-directory-howto-tenant.md) (è disponibile).</span><span class="sxs-lookup"><span data-stu-id="79687-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="79687-176">apprendendo hello toocontinue hello v 2.0 endpoint, head tooour Indietro [Guida per sviluppatori v 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79687-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="79687-177">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="79687-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="79687-178">Esempi di Azure in GitHub &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="79687-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="79687-179">Azure AD in Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="79687-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="79687-180">Documentazione di Azure AD in [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="79687-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="79687-181">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="79687-181">Get security updates for our products</span></span>
<span data-ttu-id="79687-182">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="79687-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

