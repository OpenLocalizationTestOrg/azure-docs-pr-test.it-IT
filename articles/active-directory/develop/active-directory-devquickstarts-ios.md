---
title: aaaIntegrate AD Azure in un'app iOS | Documenti Microsoft
description: Come un'applicazione iOS che si integra con Azure AD per l'accesso e le chiamate AD Azure toobuild protetto API tramite OAuth.
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="efbbe-103">Integrare Azure AD in un'app iOS</span><span class="sxs-lookup"><span data-stu-id="efbbe-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="efbbe-104">Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consente di ottenere in esecuzione con Azure Active Directory in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="efbbe-105">portale per sviluppatori Hello in modo semplificato il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="efbbe-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="efbbe-106">Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="efbbe-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="efbbe-107">Azure Active Directory (Azure AD) offre hello Active Directory Authentication Library o ADAL, per i client iOS necessarie tooaccess risorse protette.</span><span class="sxs-lookup"><span data-stu-id="efbbe-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="efbbe-108">ADAL semplifica il processo di hello che l'app Usa i token di accesso tooobtain.</span><span class="sxs-lookup"><span data-stu-id="efbbe-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="efbbe-109">toodemonstrate facilmente, in questo articolo è compilare un'applicazione elenco attività di Objective C:</span><span class="sxs-lookup"><span data-stu-id="efbbe-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="efbbe-110">Ottiene i token per chiamare l'API di Azure AD Graph hello utilizzando hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="efbbe-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="efbbe-111">Cerca in una directory gli utenti con un determinato alias.</span><span class="sxs-lookup"><span data-stu-id="efbbe-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="efbbe-112">toobuild hello completo lavoro dell'applicazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="efbbe-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="efbbe-113">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efbbe-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="efbbe-114">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="efbbe-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="efbbe-115">Usare i token ADAL tooget da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efbbe-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="efbbe-116">tooget avviato, [scaricare scheletro app hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [scaricare l'esempio hello completato](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="efbbe-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="efbbe-117">È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="efbbe-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="efbbe-118">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="efbbe-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="efbbe-119">Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consentono di ottenere in esecuzione in Azure AD in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="efbbe-120">portale per sviluppatori Hello in modo semplificato il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="efbbe-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="efbbe-121">Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="efbbe-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="efbbe-122">1. Determinare qual è l'URI di reindirizzamento per iOS</span><span class="sxs-lookup"><span data-stu-id="efbbe-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="efbbe-123">toosecurely avviare le applicazioni in determinati scenari SSO, è necessario creare un *URI di reindirizzamento* in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="efbbe-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="efbbe-124">Un reindirizzamento URI viene usato tooensure che hello token restituito toohello corretta applicazione che ha richiesto la loro.</span><span class="sxs-lookup"><span data-stu-id="efbbe-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="efbbe-125">formato iOS Hello per un reindirizzamento dell'URI è:</span><span class="sxs-lookup"><span data-stu-id="efbbe-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="efbbe-126">**app-scheme**: è registrato nel progetto XCode</span><span class="sxs-lookup"><span data-stu-id="efbbe-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="efbbe-127">ed è il modo in cui altre applicazioni possono eseguire la chiamata.</span><span class="sxs-lookup"><span data-stu-id="efbbe-127">It is how other applications can call you.</span></span> <span data-ttu-id="efbbe-128">È possibile trovarlo in Info.plist -> URL types -> URL Identifier.</span><span class="sxs-lookup"><span data-stu-id="efbbe-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="efbbe-129">È consigliabile crearne uno se non sono stati configurati uno o più URI.</span><span class="sxs-lookup"><span data-stu-id="efbbe-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="efbbe-130">**id bundle** -questo è l'identificatore Bundle trovato in "identity" hello annullare le impostazioni del progetto in XCode.</span><span class="sxs-lookup"><span data-stu-id="efbbe-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="efbbe-131">Per un esempio di questo codice di QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="efbbe-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="efbbe-132">2. Registrare un'applicazione hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="efbbe-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="efbbe-133">tooset dei token tooget app, è innanzitutto necessario tooregister in Azure Active Directory del tenant e concedergli hello tooaccess autorizzazione API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="efbbe-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="efbbe-134">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="efbbe-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="efbbe-135">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="efbbe-135">On hello top bar, click your account.</span></span> <span data-ttu-id="efbbe-136">In hello **Directory** scegliere tenant di Active Directory hello in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="efbbe-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="efbbe-137">Fare clic su **più servizi** in hello riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efbbe-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="efbbe-138">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="efbbe-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="efbbe-139">Seguire hello richiede toocreate un nuovo **applicazione Client nativa**.</span><span class="sxs-lookup"><span data-stu-id="efbbe-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="efbbe-140">Hello **nome** di hello applicazione descrive tooend utenti applicazione.</span><span class="sxs-lookup"><span data-stu-id="efbbe-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="efbbe-141">Hello **Uri di reindirizzamento** è una combinazione di tipo stringa e lo schema che Azure AD Usa tooreturn token risposte.</span><span class="sxs-lookup"><span data-stu-id="efbbe-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="efbbe-142">Immettere un valore specifico tooyour applicazione e si basa sulle informazioni di URI di reindirizzamento precedente hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="efbbe-143">Dopo aver completato la registrazione di hello, Azure AD le assegna l'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="efbbe-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="efbbe-144">È necessario che questo valore in hello nelle sezioni seguenti, quindi copiarlo dalla scheda applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="efbbe-145">Da hello **impostazioni** selezionare **autorizzazioni obbligatorie** e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="efbbe-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="efbbe-146">Selezionare **Microsoft Graph** come hello API, quindi aggiungere hello **lettura dati Directory** autorizzazione in **autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="efbbe-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="efbbe-147">Questo imposta hello di tooquery l'applicazione Azure AD Graph API per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="efbbe-148">3. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="efbbe-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="efbbe-149">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="efbbe-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="efbbe-150">Per toocommunicate ADAL con Azure AD, è necessario tooprovide con alcune informazioni la registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="efbbe-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="efbbe-151">Inizia ad aggiungere toohello ADAL progetto DirectorySearcher utilizzando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="efbbe-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="efbbe-152">Aggiungere hello toothis podfile seguenti:</span><span class="sxs-lookup"><span data-stu-id="efbbe-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="efbbe-153">Ora è possibile caricare hello podfile utilizzando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="efbbe-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="efbbe-154">Verrà creata una nuova area di lavoro XCode che sarà caricata.</span><span class="sxs-lookup"><span data-stu-id="efbbe-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="efbbe-155">Nel progetto di avvio rapido hello, aprire il file plist hello `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="efbbe-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="efbbe-156">Sostituire i valori hello elementi hello in hello sezione tooreflect hello valori immessi in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="efbbe-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="efbbe-157">Il codice fa riferimento a questi valori ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="efbbe-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="efbbe-158">Hello `tenant` dominio hello del tenant di Azure AD, ad esempio, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="efbbe-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="efbbe-159">Hello `clientId` hello client ID dell'applicazione copiata dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="efbbe-160">Hello `redirectUri` è l'URL di reindirizzamento hello è registrato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="efbbe-161">4.    Utilizzare i token ADAL tooget da Azure AD</span><span class="sxs-lookup"><span data-stu-id="efbbe-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="efbbe-162">Hello principio fondamentale dietro ADAL è che ogni volta che è necessario un token di accesso dell'app, chiama semplicemente un completionBlock `+(void) getToken : `, e ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="efbbe-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="efbbe-163">In hello `QuickStart` progetto, aprire `GraphAPICaller.m` e individuare hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` commento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="efbbe-164">Questo è possibile passare attraverso un CompletionBlock, toocommunicate con Azure AD, ADAL hello e indicare come token toocache.</span><span class="sxs-lookup"><span data-stu-id="efbbe-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="efbbe-165">A questo punto è necessario toouse toosearch questo token per gli utenti nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="efbbe-166">Trovare hello `// TODO: implement SearchUsersList` commento.</span><span class="sxs-lookup"><span data-stu-id="efbbe-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="efbbe-167">Questo metodo rende un tooquery di toohello API Azure AD Graph richiesta GET per gli utenti il cui nome UPN inizia con hello termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="efbbe-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="efbbe-168">tooquery hello Azure AD Graph API, è necessario tooinclude access_token in hello `Authorization` intestazione della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="efbbe-169">È qui che entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="efbbe-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="efbbe-170">Quando l'app richiede un token chiamando `getToken(...)`, ADAL tenta tooreturn un token senza chiedere utente hello per le credenziali.</span><span class="sxs-lookup"><span data-stu-id="efbbe-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="efbbe-171">Se ADAL rileva che l'utente hello toosign in tooget un token, verrà visualizzato una finestra di dialogo per l'accesso, raccogliere le credenziali dell'utente hello e restituisce quindi un token dopo l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="efbbe-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="efbbe-172">Se la libreria ADAL non è in grado di tooreturn un token per qualsiasi motivo, viene generata una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="efbbe-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="efbbe-173">Hello `AuthenticationResult` oggetto contiene un `tokenCacheStoreItem` oggetto che può essere informazioni hello toocollect utilizzati che potrebbe essere necessario l'app.</span><span class="sxs-lookup"><span data-stu-id="efbbe-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="efbbe-174">Nella Guida introduttiva, hello `tokenCacheStoreItem` è toodetermine usato se l'autenticazione è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="efbbe-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="efbbe-175">5. Compilare ed eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="efbbe-175">5. Build and run hello application</span></span>
<span data-ttu-id="efbbe-176">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="efbbe-176">Congratulations!</span></span> <span data-ttu-id="efbbe-177">Ora è un'applicazione iOS che è possibile autenticare gli utenti, in modo sicuro chiamare l'API Web tramite OAuth 2.0 e ottenere le informazioni di base utente hello.</span><span class="sxs-lookup"><span data-stu-id="efbbe-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="efbbe-178">Se hai già fatto, è ora hello ora toopopulate tenant con alcuni utenti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="efbbe-179">Avviare l'applicazione QuickStart e accedere come uno di questi utenti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="efbbe-180">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="efbbe-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="efbbe-181">Chiudere l'applicazione hello e avviarla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="efbbe-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="efbbe-182">Si noti che la sessione dell'utente hello rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="efbbe-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="efbbe-183">ADAL rende facile tooincorporate tutte queste funzionalità comuni di identità nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="efbbe-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="efbbe-184">Si occupa di tutto il lavoro dirty hello, ad esempio la gestione della cache, supporto del protocollo OAuth, presentate utente hello con un toosign dell'interfaccia utente in e l'aggiornamento i token scaduti.</span><span class="sxs-lookup"><span data-stu-id="efbbe-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="efbbe-185">Ciò che occorre tooknow è una singola chiamata API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="efbbe-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="efbbe-186">Per riferimento, viene fornito l'esempio hello completata (senza i valori di configurazione) su [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="efbbe-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="efbbe-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efbbe-187">Next steps</span></span>
<span data-ttu-id="efbbe-188">È possibile procedere con tooadditional scenari.</span><span class="sxs-lookup"><span data-stu-id="efbbe-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="efbbe-189">È opportuno tootry:</span><span class="sxs-lookup"><span data-stu-id="efbbe-189">You may want tootry:</span></span>

* [<span data-ttu-id="efbbe-190">Proteggere un'API Web Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="efbbe-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="efbbe-191">Informazioni su [come tooenable SSO tra app in iOS usando ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="efbbe-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

