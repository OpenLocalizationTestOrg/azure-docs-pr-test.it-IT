---
title: Introduzione ad AngularJS per Azure AD | Microsoft Docs
description: Come compilare un'applicazione Angular JS a singola pagina che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="7f00c-103">Proteggere le app AngularJS a singola pagina con Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f00c-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7f00c-104">Azure Active Directory (Azure AD) rende semplice e pratico aggiungere accesso, disconnessione e protezione delle chiamate API OAuth alle app a singola pagina.</span><span class="sxs-lookup"><span data-stu-id="7f00c-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="7f00c-105">Consente alle app di autenticare gli utenti con gli account Windows Server Active Directory e di utilizzare qualsiasi API Web protetta da Azure AD, ad esempio le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f00c-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="7f00c-106">Per le applicazioni JavaScript in esecuzione in un browser, Azure AD fornisce Active Directory Authentication Library (ADAL) o adal.js.</span><span class="sxs-lookup"><span data-stu-id="7f00c-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="7f00c-107">La funzione esclusiva di adal.js è permettere all'app di ottenere facilmente i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="7f00c-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="7f00c-108">Per far capire quanto è semplice, verrà compilata un'applicazione AngularJS To-Do List che:</span><span class="sxs-lookup"><span data-stu-id="7f00c-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="7f00c-109">Fa accedere gli utenti all'app usando Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="7f00c-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="7f00c-110">Visualizza alcune informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="7f00c-110">Displays some information about the user.</span></span>
* <span data-ttu-id="7f00c-111">Chiama in modo sicuro l'API To Do List dell'app usando token di connessione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f00c-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="7f00c-112">Disconnette l'utente dall'app.</span><span class="sxs-lookup"><span data-stu-id="7f00c-112">Signs the user out of the app.</span></span>

<span data-ttu-id="7f00c-113">Per compilare l'applicazione funzionante completa, è necessario:</span><span class="sxs-lookup"><span data-stu-id="7f00c-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="7f00c-114">Registrare l'app con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f00c-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="7f00c-115">Installare ADAL e configurare l'app a singola pagina.</span><span class="sxs-lookup"><span data-stu-id="7f00c-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="7f00c-116">Usare ADAL per proteggere le pagine nell'app a singola pagina.</span><span class="sxs-lookup"><span data-stu-id="7f00c-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="7f00c-117">Per iniziare, [scaricare la struttura dell'app](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7f00c-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="7f00c-118">È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="7f00c-119">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7f00c-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="7f00c-120">Passaggio 1: Registrare l'applicazione DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="7f00c-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="7f00c-121">Per consentire all'app di autenticare gli utenti e ottenere i token, è innanzitutto necessario registrarla nel tenant di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="7f00c-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="7f00c-122">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f00c-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f00c-123">Se è stato eseguito l'accesso a più directory, potrebbe essere necessario assicurarsi di visualizzare la directory corretta.</span><span class="sxs-lookup"><span data-stu-id="7f00c-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="7f00c-124">A tale scopo, nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="7f00c-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="7f00c-125">Nell'elenco **Directory** scegliere il tenant di Azure AD in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="7f00c-126">Fare clic su **More Services** (Altri servizi) nel riquadro a sinistra e scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f00c-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7f00c-127">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7f00c-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7f00c-128">Seguire le istruzioni e creare una nuova applicazione Web e/o API Web:</span><span class="sxs-lookup"><span data-stu-id="7f00c-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="7f00c-129">Il **nome** descrive l'applicazione agli utenti.</span><span class="sxs-lookup"><span data-stu-id="7f00c-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="7f00c-130">L'**URI di reindirizzamento** è il percorso in cui Azure AD restituirà i token.</span><span class="sxs-lookup"><span data-stu-id="7f00c-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="7f00c-131">Il percorso predefinito per questo esempio è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="7f00c-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="7f00c-132">Dopo aver completato la registrazione, Azure AD assegna all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="7f00c-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="7f00c-133">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla scheda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="7f00c-134">Adal.js usa il flusso implicito di OAuth per comunicare con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f00c-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="7f00c-135">È necessario abilitare il flusso implicito per l'applicazione eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f00c-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="7f00c-136">Fare clic sull'applicazione e scegliere **Manifesto** per aprire l'editor manifesto incorporato.</span><span class="sxs-lookup"><span data-stu-id="7f00c-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="7f00c-137">Individuare la proprietà `oauth2AllowImplicitFlow`.</span><span class="sxs-lookup"><span data-stu-id="7f00c-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="7f00c-138">Impostare il relativo valore su `true`.</span><span class="sxs-lookup"><span data-stu-id="7f00c-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="7f00c-139">Fare clic su **Salva** per salvare il manifesto.</span><span class="sxs-lookup"><span data-stu-id="7f00c-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="7f00c-140">Concedere le autorizzazioni nel tenant per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="7f00c-141">Andare in **Impostazioni** > **Proprietà** > **Autorizzazioni necessarie** e fare clic sul pulsante **Concedi autorizzazioni** nella barra superiore.</span><span class="sxs-lookup"><span data-stu-id="7f00c-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="7f00c-142">Fare clic su **Yes** per confermare.</span><span class="sxs-lookup"><span data-stu-id="7f00c-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="7f00c-143">Passaggio 2: Installare ADAL e configurare l'app a singola pagina</span><span class="sxs-lookup"><span data-stu-id="7f00c-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="7f00c-144">Ora che si dispone di un'applicazione in Azure AD, è possibile installare adal.js e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="7f00c-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="7f00c-145">Configurare il client JavaScript</span><span class="sxs-lookup"><span data-stu-id="7f00c-145">Configure the JavaScript client</span></span>
<span data-ttu-id="7f00c-146">Iniziare aggiungendo adal.js al progetto TodoSPA tramite la console di Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="7f00c-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="7f00c-147">Scaricare [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e aggiungerlo alla `App/Scripts/`directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="7f00c-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="7f00c-148">Scaricare [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e aggiungerlo alla `App/Scripts/` directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="7f00c-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="7f00c-149">Caricare ogni script prima della fine di `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="7f00c-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="7f00c-150">Configurare il server back-end</span><span class="sxs-lookup"><span data-stu-id="7f00c-150">Configure the back end server</span></span>
<span data-ttu-id="7f00c-151">Per fare in modo che l'API To Do List del back-end dell'app a singola pagina accetti i token dal browser, il back-end ha bisogno delle informazioni di configurazione relative alla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f00c-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="7f00c-152">Nel progetto TodoSPA aprire il file `web.config`.</span><span class="sxs-lookup"><span data-stu-id="7f00c-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="7f00c-153">Sostituire i valori degli elementi nella sezione `<appSettings>` in modo che corrispondano ai valori usati nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f00c-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="7f00c-154">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="7f00c-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="7f00c-155">`ida:Tenant` è il dominio del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7f00c-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="7f00c-156">`ida:Audience` è l'ID client dell'applicazione copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="7f00c-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="7f00c-157">Passaggio 3: Usare ADAL per proteggere le pagine nell'app a singola pagina</span><span class="sxs-lookup"><span data-stu-id="7f00c-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="7f00c-158">Adal.js si integra con i provider di route e HTTP AngularJS e permette di proteggere visualizzazioni individuali nell'app a singola pagina.</span><span class="sxs-lookup"><span data-stu-id="7f00c-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="7f00c-159">Importare il modulo adal.js in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="7f00c-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="7f00c-160">Inizializzare `adalProvider` con i valori di configurazione relativi alla registrazione dell'applicazione anche in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="7f00c-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="7f00c-161">Per proteggere la visualizzazione `TodoList` nell'app, usare una sola riga di codice: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="7f00c-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="7f00c-162">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7f00c-162">Summary</span></span>
<span data-ttu-id="7f00c-163">A questo punto è disponibile un'app a singola pagina sicura, in grado di concedere l'accesso agli utenti e rilasciare richieste protette di token di connessione all'API back-end.</span><span class="sxs-lookup"><span data-stu-id="7f00c-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="7f00c-164">Quando un utente fa clic sul collegamento **TodoList**, se necessario viene reindirizzato automaticamente da adal.js ad Azure AD per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7f00c-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="7f00c-165">Inoltre, adal.js collegherà automaticamente un token di accesso a tutte le richieste Ajax inviate al back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f00c-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="7f00c-166">I passaggi illustrati sopra sono i requisiti minimi necessari per compilare un'app a singola pagina con adal.js.</span><span class="sxs-lookup"><span data-stu-id="7f00c-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="7f00c-167">Tuttavia sono disponibili altre funzionalità utili nelle app a singola pagina:</span><span class="sxs-lookup"><span data-stu-id="7f00c-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="7f00c-168">Per generare in modo esplicito richieste di accesso e disconnessione, è possibile definire funzioni nei controller per richiamare adal.js.</span><span class="sxs-lookup"><span data-stu-id="7f00c-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="7f00c-169">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="7f00c-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="7f00c-170">È anche possibile presentare informazioni sull'utente nell'interfaccia utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f00c-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="7f00c-171">Il servizio ADAL è già stato aggiunto al controller `userDataCtrl`, quindi è possibile accedere all'oggetto `userInfo` nella visualizzazione associata, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="7f00c-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="7f00c-172">Esistono anche molti scenari in cui è necessario sapere se l'utente è connesso oppure no.</span><span class="sxs-lookup"><span data-stu-id="7f00c-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="7f00c-173">Per raccogliere queste informazioni, è anche possibile usare l'oggetto `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="7f00c-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="7f00c-174">Ad esempio, in `index.html` è possibile visualizzare il pulsante **Accesso** o **Disconnessione** a seconda dello stato di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="7f00c-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="7f00c-175">A questo punto l'app a singola pagina integrata in Azure AD può autenticare gli utenti, chiamare in modo sicuro il relativo back-end tramite OAuth 2.0 e ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="7f00c-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="7f00c-176">Se non si è ancora popolato il tenant con alcuni utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="7f00c-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="7f00c-177">Eseguire l'app a singola pagina To Do List e accedere come uno di questi utenti.</span><span class="sxs-lookup"><span data-stu-id="7f00c-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="7f00c-178">Aggiungere attività all'elenco azioni dell'utente, disconnettersi e accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="7f00c-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="7f00c-179">Adal.js consente di incorporare facilmente nell'applicazione funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="7f00c-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="7f00c-180">Esegue automaticamente le attività più complesse: gestione della cache, supporto del protocollo OAuth, presentazione all'utente di un'interfaccia utente di accesso, aggiornamento dei token scaduti e altro.</span><span class="sxs-lookup"><span data-stu-id="7f00c-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="7f00c-181">Come riferimento, l'esempio completo (senza i valori di configurazione) è disponibile in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7f00c-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f00c-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f00c-182">Next steps</span></span>
<span data-ttu-id="7f00c-183">Ora è possibile passare ad altri scenari.</span><span class="sxs-lookup"><span data-stu-id="7f00c-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="7f00c-184">Ad esempio è possibile provare a [chiamare un'API Web CORS da un'app a singola pagina](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="7f00c-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
