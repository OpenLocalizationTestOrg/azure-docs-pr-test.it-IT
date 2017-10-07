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
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a><span data-ttu-id="120e0-103">Aggiungere app a singola pagina AngularJS Accedi tooan - .NET</span><span class="sxs-lookup"><span data-stu-id="120e0-103">Add sign-in tooan AngularJS single page app - .NET</span></span>
<span data-ttu-id="120e0-104">In questo articolo verrà aggiunto accedere con app AngularJS tooan account Microsoft con tecnologia utilizzando hello Azure Active Directory v 2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="120e0-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="120e0-105">endpoint v 2.0 Hello permette tooperform un'integrazione singola nell'app e autenticare gli utenti con account personali e di lavoro o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="120e0-105">hello v2.0 endpoint enables you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="120e0-106">Questo esempio è una semplice app singola pagina di elenco che contiene le attività in un back-end API REST, scritto utilizzando hello MVC 4.5 di .NET framework e protetto tramite OAuth i token di connessione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="120e0-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using hello .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="120e0-107">Hello app AngularJS utilizzerà la libreria di autenticazione JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello l'intero processo di accesso e acquisire i token per hello chiamata API REST.</span><span class="sxs-lookup"><span data-stu-id="120e0-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="120e0-108">Hello stesso modello può essere applicati tooauthenticate tooother le API REST, ad esempio hello [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="120e0-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="120e0-109">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="120e0-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="120e0-110">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="120e0-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="120e0-111">Scaricare</span><span class="sxs-lookup"><span data-stu-id="120e0-111">Download</span></span>
<span data-ttu-id="120e0-112">tooget avviato, si sarà necessario toodownload & installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="120e0-112">tooget started, you'll need toodownload & install Visual Studio.</span></span>  <span data-ttu-id="120e0-113">Sarà quindi possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lo scheletro di un'app:</span><span class="sxs-lookup"><span data-stu-id="120e0-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="120e0-114">app scheletro Hello include tutto il codice boilerplate hello per un'app AngularJS semplice, ma mancano le parti relative alle identità hello.</span><span class="sxs-lookup"><span data-stu-id="120e0-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="120e0-115">Se non si desidera toofollow lungo, è possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) : esempio hello completata.</span><span class="sxs-lookup"><span data-stu-id="120e0-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="120e0-116">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="120e0-116">Register an app</span></span>
<span data-ttu-id="120e0-117">Innanzitutto, creare un'app in hello [il portale di registrazione di App](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o attenersi alla seguente [passaggi dettagliati](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="120e0-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="120e0-118">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="120e0-118">Make sure to:</span></span>

* <span data-ttu-id="120e0-119">Aggiungere hello **Web** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="120e0-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="120e0-120">Immettere hello corretto **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="120e0-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="120e0-121">valore predefinito di Hello per questo esempio è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="120e0-121">hello default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="120e0-122">Lasciare hello **consentire flusso implicito** casella di controllo abilitato.</span><span class="sxs-lookup"><span data-stu-id="120e0-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="120e0-123">Copia verso il basso hello **ID applicazione** app tooyour assegnato, sarà necessario immetterla a breve.</span><span class="sxs-lookup"><span data-stu-id="120e0-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="120e0-124">Installare adal.js</span><span class="sxs-lookup"><span data-stu-id="120e0-124">Install adal.js</span></span>
<span data-ttu-id="120e0-125">toostart, passare tooproject è stato scaricato e installato adal.js.</span><span class="sxs-lookup"><span data-stu-id="120e0-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="120e0-126">Se [bower](http://bower.io/) è installato, è sufficiente eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="120e0-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="120e0-127">Per eventuali differenze tra le versioni di dipendenza, è sufficiente scegliere una versione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="120e0-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="120e0-128">In alternativa, è possibile scaricare manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="120e0-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="120e0-129">Aggiungere entrambi i file toohello `app/lib/adal-angular-experimental/dist` directory di hello `TodoSPA` progetto.</span><span class="sxs-lookup"><span data-stu-id="120e0-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory of hello `TodoSPA` project.</span></span>

<span data-ttu-id="120e0-130">Ora aprire hello progetto in Visual Studio e caricare adal.js alla fine di hello del corpo della pagina principale hello:</span><span class="sxs-lookup"><span data-stu-id="120e0-130">Now open hello project in Visual Studio, and load adal.js at hello end of hello main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="120e0-131">Impostare hello API REST</span><span class="sxs-lookup"><span data-stu-id="120e0-131">Set up hello REST API</span></span>
<span data-ttu-id="120e0-132">Mentre si configurazione in corso, iniziamo lavoro API REST di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="120e0-132">While we're setting things up, let's get hello backend REST API working.</span></span>  <span data-ttu-id="120e0-133">Nella radice del progetto hello hello aprire `web.config` e sostituire hello `audience` valore.</span><span class="sxs-lookup"><span data-stu-id="120e0-133">In hello root of hello project, open `web.config` and replace hello `audience` value.</span></span>  <span data-ttu-id="120e0-134">API REST Hello verrà utilizzato questo token toovalidate valore riceve da app angolare hello per le richieste AJAX.</span><span class="sxs-lookup"><span data-stu-id="120e0-134">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="120e0-135">Questo è tutto il tempo di hello Daremo toospend che illustrano il funzionamento hello API REST.</span><span class="sxs-lookup"><span data-stu-id="120e0-135">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="120e0-136">È gratuito toopoke nel codice hello, ma se si desidera toolearn ulteriori informazioni sulla protezione di web API con Azure AD, vedere [questo articolo](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="120e0-136">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="120e0-137">Concedere l'accesso agli utenti</span><span class="sxs-lookup"><span data-stu-id="120e0-137">Sign users in</span></span>
<span data-ttu-id="120e0-138">Tempo toowrite del codice di identità.</span><span class="sxs-lookup"><span data-stu-id="120e0-138">Time toowrite some identity code.</span></span>  <span data-ttu-id="120e0-139">Come è possibile osservare, adal.js contiene un provider AngularJS, che funziona bene con il meccanismo di routing Angular.</span><span class="sxs-lookup"><span data-stu-id="120e0-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="120e0-140">Per iniziare, aggiungere hello modulo adal toohello app:</span><span class="sxs-lookup"><span data-stu-id="120e0-140">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="120e0-141">È ora possibile inizializzare hello `adalProvider` con l'ID applicazione:</span><span class="sxs-lookup"><span data-stu-id="120e0-141">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="120e0-142">Grande, ora adal.js tutte le informazioni di hello deve toosecure gli utenti nell'applicazione e accedere.</span><span class="sxs-lookup"><span data-stu-id="120e0-142">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="120e0-143">accesso tooforce per una route specifica nell'app hello, tutto ciò che serve è una riga di codice:</span><span class="sxs-lookup"><span data-stu-id="120e0-143">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="120e0-144">Ora quando un utente fa clic hello `TodoList` collegamento, adal.js verrà reindirizzata automaticamente tooAzure Active Directory per l'accesso se necessario.</span><span class="sxs-lookup"><span data-stu-id="120e0-144">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="120e0-145">È anche possibile inviare in modo esplicito richieste di accesso e di disconnessione richiamando adal.js nei controller:</span><span class="sxs-lookup"><span data-stu-id="120e0-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="120e0-146">Visualizzare le info utente</span><span class="sxs-lookup"><span data-stu-id="120e0-146">Display user info</span></span>
<span data-ttu-id="120e0-147">Ora che hello utente è connesso, è necessario probabilmente i dati di autenticazione tooaccess hello eseguito l'accesso dell'utente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="120e0-147">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="120e0-148">Adal.js espone queste informazioni in hello `userInfo` oggetto.</span><span class="sxs-lookup"><span data-stu-id="120e0-148">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="120e0-149">tooaccess questo oggetto in una vista, aggiungere prima adal.js toohello di ambito di primo livello del controller corrispondente hello:</span><span class="sxs-lookup"><span data-stu-id="120e0-149">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="120e0-150">Quindi è possibile gestire direttamente hello `userInfo` oggetto nella visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="120e0-150">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="120e0-151">È inoltre possibile utilizzare hello `userInfo` oggetto toodetermine se hello utente è connesso o non.</span><span class="sxs-lookup"><span data-stu-id="120e0-151">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="120e0-152">Hello chiamata API REST</span><span class="sxs-lookup"><span data-stu-id="120e0-152">Call hello REST API</span></span>
<span data-ttu-id="120e0-153">Infine, è ora tooget alcuni token e chiamare hello toocreate API REST, leggere, aggiornare ed eliminare le attività.</span><span class="sxs-lookup"><span data-stu-id="120e0-153">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="120e0-154">La novità è che</span><span class="sxs-lookup"><span data-stu-id="120e0-154">Well guess what?</span></span>  <span data-ttu-id="120e0-155">Non è toodo *una cosa*.</span><span class="sxs-lookup"><span data-stu-id="120e0-155">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="120e0-156">Adal.js eseguirà automaticamente il recupero, la memorizzazione nella cache e l'aggiornamento dei token.</span><span class="sxs-lookup"><span data-stu-id="120e0-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="120e0-157">Inoltre occuperà di associare tali token che toooutgoing AJAX richiede che si invia toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="120e0-157">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="120e0-158">Come funziona esattamente tutto questo?</span><span class="sxs-lookup"><span data-stu-id="120e0-158">How exactly does this work?</span></span> <span data-ttu-id="120e0-159">È tutto grazie toohello sorprendente [AngularJS intercettori](https://docs.angularjs.org/api/ng/service/$http), che consente di adal.js tootransform messaggi http in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="120e0-159">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="120e0-160">Inoltre, adal.js si presuppone che tutte le richieste di invio toohello nello stesso dominio come finestra hello debba utilizzare i token destinati hello stesso ID applicazione come hello app AngularJS.</span><span class="sxs-lookup"><span data-stu-id="120e0-160">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="120e0-161">Ecco perché è stato usato hello stesso ID applicazione entrambi app angolare hello e hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="120e0-161">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="120e0-162">Naturalmente, è possibile eseguire l'override di questo comportamento e indicare i token tooget adal.js per altre API REST, se necessario, ma per hello questo semplice scenario eseguirà le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="120e0-162">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="120e0-163">Di seguito è riportato un frammento di codice che illustra come è facile richieste toosend con i token di connessione da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="120e0-163">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="120e0-164">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="120e0-164">Congratulations!</span></span>  <span data-ttu-id="120e0-165">A questo punto l'app a singola pagina integrata in Azure AD è completata.</span><span class="sxs-lookup"><span data-stu-id="120e0-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="120e0-166">Come è evidente,</span><span class="sxs-lookup"><span data-stu-id="120e0-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="120e0-167">È possibile autenticare gli utenti, in modo sicuro chiamare il relativo back-end API REST tramite OpenID Connect e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="120e0-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="120e0-168">Viene fornita, hello supporta tutti gli utenti con un Account Microsoft personale o di un account di lavoro o dell'istituto di istruzione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="120e0-168">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="120e0-169">Eseguire app hello e in un browser passare troppo`https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="120e0-169">Run hello app, and in a browser navigate too`https://localhost:44326/`.</span></span>  <span data-ttu-id="120e0-170">Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="120e0-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="120e0-171">Aggiungere l'elenco di attività dell'utente di attività toohello e disconnettersi.  Provare ad accedere con hello altro tipo di account.</span><span class="sxs-lookup"><span data-stu-id="120e0-171">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="120e0-172">Se è necessario un utenti di lavoro o dell'istituto di istruzione toocreate tenant di Azure AD, [informazioni su come una qui tooget](active-directory-howto-tenant.md) (è disponibile).</span><span class="sxs-lookup"><span data-stu-id="120e0-172">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="120e0-173">apprendendo endpoint v 2.0 hello, head tooour indietro toocontinue [Guida per sviluppatori v 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="120e0-173">toocontinue learning about hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="120e0-174">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="120e0-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="120e0-175">Esempi di Azure in GitHub &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="120e0-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="120e0-176">Azure AD in Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="120e0-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="120e0-177">Documentazione di Azure AD in [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="120e0-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="120e0-178">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="120e0-178">Get security updates for our products</span></span>
<span data-ttu-id="120e0-179">Si consiglia di generazione di eventi di sicurezza, visitare il sito di notifica tooget [questa pagina](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="120e0-179">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

