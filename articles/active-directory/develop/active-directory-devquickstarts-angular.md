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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="b327b-103">Proteggere le app AngularJS a singola pagina con Azure AD</span><span class="sxs-lookup"><span data-stu-id="b327b-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b327b-104">Azure Active Directory (Azure AD) rende semplice e diretto per si tooadd accesso, disconnessione, e chiamate all'API OAuth sicura tooyour applicazioni a pagina singola.</span><span class="sxs-lookup"><span data-stu-id="b327b-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="b327b-105">Consente agli utenti di tooauthenticate App con gli account di Windows Server Active Directory e utilizzare qualsiasi API Azure AD consente di proteggere, ad esempio hello API di Office 365 o hello Azure API web.</span><span class="sxs-lookup"><span data-stu-id="b327b-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="b327b-106">Per le applicazioni JavaScript in esecuzione in un browser, Azure Active Directory fornisce hello Active Directory Authentication Library (ADAL) o adal.js.</span><span class="sxs-lookup"><span data-stu-id="b327b-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="b327b-107">Hello unico scopo del adal.js è toomake è più facile per i token di accesso tooget app.</span><span class="sxs-lookup"><span data-stu-id="b327b-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="b327b-108">la semplicità è, toodemonstrate qui, verrà creata una tooDo AngularJS applicazione elenco:</span><span class="sxs-lookup"><span data-stu-id="b327b-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="b327b-109">Utente di hello segni toohello App usando Azure AD come provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="b327b-110">Consente di visualizzare alcune informazioni sull'utente hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="b327b-111">Le chiamate in modo sicuro hello tooDo dell'app API di elenco con i token di connessione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b327b-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="b327b-112">Segni di hello utente all'esterno dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="b327b-113">un'applicazione toobuild hello completato, lavoro, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b327b-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="b327b-114">Registrare l'app con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b327b-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="b327b-115">ADAL di installare e configurare l'applicazione a una pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="b327b-116">Utilizzare pagine protette toohelp ADAL nell'app a pagina singola hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="b327b-117">tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b327b-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="b327b-118">È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b327b-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="b327b-119">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b327b-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="b327b-120">Passaggio 1: Registrare un'applicazione hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="b327b-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="b327b-121">tooenable app tooauthenticate utenti e i token get, è necessario innanzitutto tooregister tenant in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b327b-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="b327b-122">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b327b-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b327b-123">Se si accede alla directory toomultiple, potrebbe essere visualizzato directory corretta hello tooensure.</span><span class="sxs-lookup"><span data-stu-id="b327b-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="b327b-124">toodo in tal caso, nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="b327b-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="b327b-125">In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b327b-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="b327b-126">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b327b-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b327b-127">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b327b-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b327b-128">Seguire le istruzioni di hello e creare una nuova applicazione web e/o API web:</span><span class="sxs-lookup"><span data-stu-id="b327b-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="b327b-129">**Nome** descrive toousers l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b327b-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="b327b-130">**Uri di reindirizzamento** toowhich percorso hello Azure AD restituirà i token.</span><span class="sxs-lookup"><span data-stu-id="b327b-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="b327b-131">il percorso predefinito Hello per questo esempio è `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="b327b-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="b327b-132">Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="b327b-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="b327b-133">È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="b327b-134">Adal.js Usa hello OAuth flusso implicito toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b327b-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="b327b-135">Per l'applicazione, è necessario abilitare il flusso implicito hello:</span><span class="sxs-lookup"><span data-stu-id="b327b-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="b327b-136">Fare clic su un'applicazione hello e selezionare **manifesto** editor del manifesto tooopen hello inline.</span><span class="sxs-lookup"><span data-stu-id="b327b-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="b327b-137">Individuare hello `oauth2AllowImplicitFlow` proprietà.</span><span class="sxs-lookup"><span data-stu-id="b327b-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="b327b-138">Impostare il relativo valore troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="b327b-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="b327b-139">Fare clic su **salvare** manifesto hello toosave.</span><span class="sxs-lookup"><span data-stu-id="b327b-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="b327b-140">Concedere le autorizzazioni nel tenant per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b327b-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="b327b-141">Andare troppo**impostazioni** > **proprietà** > **autorizzazioni obbligatorie**, fare clic su hello **concedere autorizzazioni**pulsante nella barra superiore hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="b327b-142">Fare clic su **Sì** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="b327b-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="b327b-143">Passaggio 2: Installare ADAL e configurare l'applicazione a una pagina hello</span><span class="sxs-lookup"><span data-stu-id="b327b-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="b327b-144">Ora che si dispone di un'applicazione in Azure AD, è possibile installare adal.js e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="b327b-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="b327b-145">Configurare i client JavaScript hello</span><span class="sxs-lookup"><span data-stu-id="b327b-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="b327b-146">Inizia ad aggiungere adal.js toohello TodoSPA progetto utilizzando la Console di gestione pacchetti hello:</span><span class="sxs-lookup"><span data-stu-id="b327b-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="b327b-147">Scaricare [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e aggiungerlo toohello `App/Scripts/` directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="b327b-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="b327b-148">Scaricare [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e aggiungerlo toohello `App/Scripts/` directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="b327b-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="b327b-149">Caricare ogni script entro hello hello `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="b327b-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="b327b-150">Configurare i server back-end hello</span><span class="sxs-lookup"><span data-stu-id="b327b-150">Configure hello back end server</span></span>
<span data-ttu-id="b327b-151">Per back-end tooDo API elenco tooaccept i token dell'applicazione a pagina singola hello da browser hello, back-end hello richiede informazioni di configurazione di registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="b327b-152">Nel progetto TodoSPA hello aprire `web.config`.</span><span class="sxs-lookup"><span data-stu-id="b327b-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="b327b-153">Sostituire i valori hello elementi hello in hello `<appSettings>` hello di sezione tooreflect valori hello utilizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b327b-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="b327b-154">Il codice farà riferimento a questi valori ogni volta che userà ADAL.</span><span class="sxs-lookup"><span data-stu-id="b327b-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b327b-155">`ida:Tenant`è il dominio di hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b327b-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="b327b-156">`ida:Audience`è l'ID client hello dell'applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="b327b-157">Passaggio 3: Usare ADAL toohelp sicura pagine hello a pagina singola app</span><span class="sxs-lookup"><span data-stu-id="b327b-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="b327b-158">Adal.js si integra con i provider di route e HTTP AngularJS e permette di proteggere visualizzazioni individuali nell'app a singola pagina.</span><span class="sxs-lookup"><span data-stu-id="b327b-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="b327b-159">In `App/Scripts/app.js`, importare il modulo di adal.js hello:</span><span class="sxs-lookup"><span data-stu-id="b327b-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="b327b-160">Inizializzare `adalProvider` utilizzando i valori di configurazione hello della registrazione dell'applicazione, anche in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="b327b-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="b327b-161">Guida in linea protetta hello `TodoList` Visualizza nell'app hello usando solo una riga di codice: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="b327b-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="b327b-162">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b327b-162">Summary</span></span>
<span data-ttu-id="b327b-163">È ora disponibile un'applicazione a pagina singola protetta che può accedere gli utenti e rilasciare l'API di back-end tooits le richieste di token di connessione protetta.</span><span class="sxs-lookup"><span data-stu-id="b327b-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="b327b-164">Quando un utente fa clic hello **TodoList** collegamento, adal.js verrà reindirizzata automaticamente tooAzure Active Directory per l'accesso se necessario.</span><span class="sxs-lookup"><span data-stu-id="b327b-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="b327b-165">Inoltre, adal.js collegherà automaticamente un accesso token tooany che le richieste Ajax back-end dell'app toohello inviati.</span><span class="sxs-lookup"><span data-stu-id="b327b-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="b327b-166">Hello passaggi precedenti sono hello bare minimo necessario toobuild un'applicazione a singola pagina utilizzando adal.js.</span><span class="sxs-lookup"><span data-stu-id="b327b-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="b327b-167">Tuttavia sono disponibili altre funzionalità utili nelle app a singola pagina:</span><span class="sxs-lookup"><span data-stu-id="b327b-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="b327b-168">è possibile definire funzioni nei controller di che richiamano adal.js tooexplicitly emettere richieste di accesso e disconnessione.</span><span class="sxs-lookup"><span data-stu-id="b327b-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="b327b-169">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="b327b-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="b327b-170">Le informazioni utente toopresent nell'interfaccia utente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="b327b-171">Hello ADAL servizio è già stato aggiunto toohello `userDataCtrl` controller, pertanto è possibile accedere hello `userInfo` oggetto hello associata visualizzazione `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="b327b-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="b327b-172">Esistono molti scenari in cui è opportuno tooknow se hello utente è connesso o non.</span><span class="sxs-lookup"><span data-stu-id="b327b-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="b327b-173">È inoltre possibile utilizzare hello `userInfo` oggetto toogather queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="b327b-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="b327b-174">Ad esempio, in `index.html`, è possibile visualizzare entrambi hello **accesso** o **Logout** pulsante in base allo stato di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="b327b-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="b327b-175">L'app Azure a pagina singola integrata in Active Directory può autenticare gli utenti, in modo sicuro chiamare il relativo back-end tramite OAuth 2.0 e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="b327b-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="b327b-176">Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="b327b-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="b327b-177">Eseguire l'app di una pagina di elenco tooDo e accedere con uno di tali utenti.</span><span class="sxs-lookup"><span data-stu-id="b327b-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="b327b-178">Aggiungere l'elenco di attività dell'utente di attività toohello, disconnettersi e accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b327b-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="b327b-179">Adal.js rende facile tooincorporate funzionalità comuni delle identità nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b327b-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="b327b-180">Si occupa di tutto il lavoro dirty hello per l'utente: gestione della cache, supporto del protocollo OAuth, presentate utente hello con un'accesso dell'interfaccia utente, l'aggiornamento, i token scaduti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="b327b-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="b327b-181">Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b327b-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b327b-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b327b-182">Next steps</span></span>
<span data-ttu-id="b327b-183">È possibile procedere con tooadditional scenari.</span><span class="sxs-lookup"><span data-stu-id="b327b-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="b327b-184">Potrebbe essere necessario tootry: [chiamare un'API web CORS da un'applicazione a pagina singola](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="b327b-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
