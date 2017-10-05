---
title: Introduzione alle app a pagina singola Azure AD v2.0 .NET AngularJS | Documentazione Microsoft
description: Come creare un'app a pagina singola AngularJS che consente agli utenti di accedere con un account Microsoft personale, aziendale e dell'istituto di istruzione.
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
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="6daaf-103">Aggiungere l'accesso a un'app a pagina singola AngularJS - .NET</span><span class="sxs-lookup"><span data-stu-id="6daaf-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="6daaf-104">In questo articolo verrà aggiunto l'accesso con account Microsoft a un'app AngularJS usando l'endpoint v2.0 di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6daaf-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="6daaf-105">L'endpoint v2.0 consente di eseguire una singola integrazione nell'app e di autenticare gli utenti con account sia personali che aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="6daaf-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="6daaf-106">Questo esempio è una semplice app a pagina singola To-Do List che archivia le attività in un'API REST back-end, scritta con il framework MVC .NET 4.5 e protetta con i token di connessione OAuth di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6daaf-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="6daaf-107">L'app AngularJS userà la libreria di autenticazione JavaScript open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) per gestire l'intero processo di accesso e acquisire i token per chiamare l'API REST.</span><span class="sxs-lookup"><span data-stu-id="6daaf-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="6daaf-108">Lo stesso modello può essere applicato per l'autenticazione in altre API REST, ad esempio [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6daaf-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6daaf-109">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="6daaf-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="6daaf-110">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="6daaf-111">Scaricare</span><span class="sxs-lookup"><span data-stu-id="6daaf-111">Download</span></span>
<span data-ttu-id="6daaf-112">Per iniziare, sarà necessario scaricare e installare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6daaf-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="6daaf-113">Sarà quindi possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lo scheletro di un'app:</span><span class="sxs-lookup"><span data-stu-id="6daaf-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="6daaf-114">Lo scheletro di un'app include tutto il codice boilerplate per una semplice app AngularJS, ma non tutte le parti relative all'identità.</span><span class="sxs-lookup"><span data-stu-id="6daaf-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="6daaf-115">Se non si vuole proseguire, in alternativa è possibile clonare o [scaricare](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) l'esempio completo.</span><span class="sxs-lookup"><span data-stu-id="6daaf-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="6daaf-116">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="6daaf-116">Register an app</span></span>
<span data-ttu-id="6daaf-117">Per prima cosa, creare un'app nel [portale di registrazione delle app](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) oppure seguire questa [procedura dettagliata](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="6daaf-118">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="6daaf-118">Make sure to:</span></span>

* <span data-ttu-id="6daaf-119">Aggiungere la piattaforma **Web** per l'app.</span><span class="sxs-lookup"><span data-stu-id="6daaf-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="6daaf-120">Immettere l' **URI di reindirizzamento**corretto.</span><span class="sxs-lookup"><span data-stu-id="6daaf-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="6daaf-121">Il valore predefinito per questo esempio è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="6daaf-122">Lasciare abilitata la casella di controllo **Consenti flusso implicito** .</span><span class="sxs-lookup"><span data-stu-id="6daaf-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="6daaf-123">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="6daaf-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="6daaf-124">Installare adal.js</span><span class="sxs-lookup"><span data-stu-id="6daaf-124">Install adal.js</span></span>
<span data-ttu-id="6daaf-125">Per iniziare, andare al progetto scaricato e installare adal.js.</span><span class="sxs-lookup"><span data-stu-id="6daaf-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="6daaf-126">Se [bower](http://bower.io/) è installato, è sufficiente eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="6daaf-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="6daaf-127">In caso di mancata corrispondenza delle versioni delle dipendenze, scegliere la versione superiore.</span><span class="sxs-lookup"><span data-stu-id="6daaf-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="6daaf-128">In alternativa, è possibile scaricare manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="6daaf-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="6daaf-129">Aggiungere entrambi i file alla directory `app/lib/adal-angular-experimental/dist` del progetto `TodoSPA`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="6daaf-130">Ora aprire il progetto in Visual Studio e caricare adal.js alla fine del corpo della pagina principale:</span><span class="sxs-lookup"><span data-stu-id="6daaf-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="6daaf-131">Configurare l'API REST</span><span class="sxs-lookup"><span data-stu-id="6daaf-131">Set up the REST API</span></span>
<span data-ttu-id="6daaf-132">Mentre si configurano altre impostazioni, verrà resa operativa l'API REST back-end.</span><span class="sxs-lookup"><span data-stu-id="6daaf-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="6daaf-133">Nella radice del progetto aprire `web.config` e sostituire il valore `audience`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="6daaf-134">L'API REST userà questo valore per convalidare i token ricevuti dall'app Angular nelle richieste AJAX.</span><span class="sxs-lookup"><span data-stu-id="6daaf-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="6daaf-135">Da ora in avanti non si parlerà più del funzionamento dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="6daaf-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="6daaf-136">È possibile scrivere nel codice, ma, per altre informazioni sulla protezione delle API Web con Azure AD, vedere [questo articolo](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="6daaf-137">Concedere l'accesso agli utenti</span><span class="sxs-lookup"><span data-stu-id="6daaf-137">Sign users in</span></span>
<span data-ttu-id="6daaf-138">Ora verrà scritto un codice di identità.</span><span class="sxs-lookup"><span data-stu-id="6daaf-138">Time to write some identity code.</span></span>  <span data-ttu-id="6daaf-139">Come è possibile osservare, adal.js contiene un provider AngularJS, che funziona bene con il meccanismo di routing Angular.</span><span class="sxs-lookup"><span data-stu-id="6daaf-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="6daaf-140">Iniziare aggiungendo il modulo adal all'app:</span><span class="sxs-lookup"><span data-stu-id="6daaf-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="6daaf-141">Ora è possibile inizializzare `adalProvider` con l'ID applicazione:</span><span class="sxs-lookup"><span data-stu-id="6daaf-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="6daaf-142">Ora adal.js ha tutte le informazioni necessarie per proteggere l'app e far accedere gli utenti.</span><span class="sxs-lookup"><span data-stu-id="6daaf-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="6daaf-143">Per forzare l'accesso per una particolare route nell'app, è sufficiente una riga di codice:</span><span class="sxs-lookup"><span data-stu-id="6daaf-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="6daaf-144">Ora, quando un utente fa clic sul collegamento `TodoList` , viene reindirizzato automaticamente da adal.js ad Azure AD per l'accesso, se necessario.</span><span class="sxs-lookup"><span data-stu-id="6daaf-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="6daaf-145">È anche possibile inviare in modo esplicito richieste di accesso e di disconnessione richiamando adal.js nei controller:</span><span class="sxs-lookup"><span data-stu-id="6daaf-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="6daaf-146">Visualizzare le info utente</span><span class="sxs-lookup"><span data-stu-id="6daaf-146">Display user info</span></span>
<span data-ttu-id="6daaf-147">Ora che l'utente è connesso, sarà probabilmente necessario accedere ai dati di autenticazione dell'utente connesso contenuti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6daaf-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="6daaf-148">Adal.js espone queste informazioni nell'oggetto `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="6daaf-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="6daaf-149">Per accedere a questo oggetto in una visualizzazione, aggiungere prima adal.js all'ambito radice del controller corrispondente:</span><span class="sxs-lookup"><span data-stu-id="6daaf-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="6daaf-150">Sarà quindi possibile indirizzare direttamente l'oggetto `userInfo` nella visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="6daaf-150">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="6daaf-151">È anche possibile usare l'oggetto `userInfo` per determinare se l'utente è connesso.</span><span class="sxs-lookup"><span data-stu-id="6daaf-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="6daaf-152">Chiamare l'API REST</span><span class="sxs-lookup"><span data-stu-id="6daaf-152">Call the REST API</span></span>
<span data-ttu-id="6daaf-153">Ora verranno recuperati alcuni token e verrà chiamata l'API REST per creare, leggere, aggiornare ed eliminare le attività.</span><span class="sxs-lookup"><span data-stu-id="6daaf-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="6daaf-154">La novità è che</span><span class="sxs-lookup"><span data-stu-id="6daaf-154">Well guess what?</span></span>  <span data-ttu-id="6daaf-155">non è necessario eseguire *alcuna operazione*.</span><span class="sxs-lookup"><span data-stu-id="6daaf-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="6daaf-156">Adal.js eseguirà automaticamente il recupero, la memorizzazione nella cache e l'aggiornamento dei token.</span><span class="sxs-lookup"><span data-stu-id="6daaf-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="6daaf-157">Allegherà anche questi token alle richieste AJAX in uscita inviate all'API REST.</span><span class="sxs-lookup"><span data-stu-id="6daaf-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="6daaf-158">Come funziona esattamente tutto questo?</span><span class="sxs-lookup"><span data-stu-id="6daaf-158">How exactly does this work?</span></span> <span data-ttu-id="6daaf-159">Sta tutto negli [intercettori AngularJS](https://docs.angularjs.org/api/ng/service/$http), che consentono ad adal.js di trasformare i messaggi http in uscita e in ingresso.</span><span class="sxs-lookup"><span data-stu-id="6daaf-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="6daaf-160">Adal.js presume inoltre che le richieste inviate allo stesso dominio della finestra usino i token destinati allo stesso ID applicazione dell'app AngularJS.</span><span class="sxs-lookup"><span data-stu-id="6daaf-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="6daaf-161">Infatti lo stesso ID applicazione è stato usato sia nell'app Angular che nell'API REST NodeJS.</span><span class="sxs-lookup"><span data-stu-id="6daaf-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="6daaf-162">È possibile, ovviamente, ignorare questo comportamento e comunicare ad adal.js di ottenere i token per le altre API REST, se necessario, ma per questo semplice scenario verranno usate le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="6daaf-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="6daaf-163">Ecco un frammento che mostra come sia semplice inviare richieste con i token di connessione da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6daaf-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="6daaf-164">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="6daaf-164">Congratulations!</span></span>  <span data-ttu-id="6daaf-165">A questo punto l'app a singola pagina integrata in Azure AD è completata.</span><span class="sxs-lookup"><span data-stu-id="6daaf-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="6daaf-166">Come è evidente,</span><span class="sxs-lookup"><span data-stu-id="6daaf-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="6daaf-167">può autenticare gli utenti, chiamare in modo sicuro l'API REST back-end con OpenID Connect e ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="6daaf-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="6daaf-168">Per impostazione predefinita, supporta tutti gli utenti con un account Microsoft personale o un account aziendale o dell'istituto di istruzione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6daaf-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="6daaf-169">Eseguire l'app e in un browser andare a `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="6daaf-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="6daaf-170">Accedere con un account Microsoft personale o un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="6daaf-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="6daaf-171">Aggiungere attività all'elenco attività dell'utente e disconnettersi.</span><span class="sxs-lookup"><span data-stu-id="6daaf-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="6daaf-172">Provare ad accedere con l'altro tipo di account.</span><span class="sxs-lookup"><span data-stu-id="6daaf-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="6daaf-173">Se è necessario un tenant di Azure AD per creare utenti aziendali o dell'istituto di istruzione, [qui sono disponibili informazioni per ottenerne uno](active-directory-howto-tenant.md) (è gratuito).</span><span class="sxs-lookup"><span data-stu-id="6daaf-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="6daaf-174">Per altre informazioni sull'endpoint v2.0, tornare alla [guida per sviluppatori versione 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6daaf-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="6daaf-175">Per altre risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="6daaf-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="6daaf-176">Esempi di Azure in GitHub >></span><span class="sxs-lookup"><span data-stu-id="6daaf-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="6daaf-177">Azure AD in Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="6daaf-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="6daaf-178">Documentazione di Azure AD in [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="6daaf-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6daaf-179">Ottenere aggiornamenti della sicurezza per i prodotti</span><span class="sxs-lookup"><span data-stu-id="6daaf-179">Get security updates for our products</span></span>
<span data-ttu-id="6daaf-180">È consigliabile ricevere notifiche in caso di problemi di sicurezza. A tale scopo, visitare [questa pagina](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6daaf-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

