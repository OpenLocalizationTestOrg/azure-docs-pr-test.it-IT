---
title: Integrare Azure AD in un'app iOS | Microsoft Docs
description: Informazioni su come compilare un'applicazione iOS che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="b3818-103">Integrare Azure AD in un'app iOS</span><span class="sxs-lookup"><span data-stu-id="b3818-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="b3818-104">È consigliabile provare l'anteprima del nuovo [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consente di imparare a usare Azure Active Directory in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b3818-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="b3818-105">Il portale per sviluppatori guida l'utente nel processo di registrazione di un'app e di integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="b3818-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="b3818-106">Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="b3818-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="b3818-107">Azure Active Directory (Azure AD) include Active Directory Authentication Library, o ADAL, per i client iOS che devono accedere a risorse protette.</span><span class="sxs-lookup"><span data-stu-id="b3818-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="b3818-108">ADAL semplifica il processo usato dall'applicazione per ottenere i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="b3818-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="b3818-109">Per far capire quanto sia semplice, in questo articolo verrà compilata un'applicazione Objective C per eseguire alcuni operazioni che:</span><span class="sxs-lookup"><span data-stu-id="b3818-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="b3818-110">Ottiene i token di accesso per chiamare l'API Graph di Azure AD con il [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3818-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b3818-111">Cerca in una directory gli utenti con un determinato alias.</span><span class="sxs-lookup"><span data-stu-id="b3818-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="b3818-112">Per compilare l'applicazione funzionante completa, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b3818-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="b3818-113">Registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3818-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="b3818-114">Installare e configurare ADAL.</span><span class="sxs-lookup"><span data-stu-id="b3818-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="b3818-115">Usare ADAL per ottenere i token da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3818-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="b3818-116">Per iniziare, [scaricare la struttura dell'app](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) o [scaricare l'esempio completato](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b3818-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="b3818-117">È necessario anche un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b3818-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="b3818-118">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b3818-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="b3818-119">È consigliabile provare l'anteprima del nuovo [portale per sviluppatori](https://identity.microsoft.com/Docs/iOS) che consente di imparare a usare Azure AD in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b3818-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="b3818-120">Il portale per sviluppatori guida l'utente nel processo di registrazione di un'app e di integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="b3818-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="b3818-121">Al termine si ottiene un'applicazione semplice in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="b3818-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="b3818-122">1. Determinare qual è l'URI di reindirizzamento per iOS</span><span class="sxs-lookup"><span data-stu-id="b3818-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="b3818-123">Per avviare in modo sicuro le applicazioni in determinati scenari SSO, è necessario creare un *URI di reindirizzamento* in un formato particolare.</span><span class="sxs-lookup"><span data-stu-id="b3818-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="b3818-124">Un URI di reindirizzamento viene usato per assicurarsi che i token vengano restituiti all'applicazione corretta che li aveva richiesti.</span><span class="sxs-lookup"><span data-stu-id="b3818-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="b3818-125">Il formato iOS per l'URI di reindirizzamento è il seguente:</span><span class="sxs-lookup"><span data-stu-id="b3818-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="b3818-126">**app-scheme**: è registrato nel progetto XCode</span><span class="sxs-lookup"><span data-stu-id="b3818-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="b3818-127">ed è il modo in cui altre applicazioni possono eseguire la chiamata.</span><span class="sxs-lookup"><span data-stu-id="b3818-127">It is how other applications can call you.</span></span> <span data-ttu-id="b3818-128">È possibile trovarlo in Info.plist -> URL types -> URL Identifier.</span><span class="sxs-lookup"><span data-stu-id="b3818-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="b3818-129">È consigliabile crearne uno se non sono stati configurati uno o più URI.</span><span class="sxs-lookup"><span data-stu-id="b3818-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="b3818-130">**bundle-id** : è il Bundle Identifier presente in "identity" nelle impostazioni del progetto in XCode.</span><span class="sxs-lookup"><span data-stu-id="b3818-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="b3818-131">Per un esempio di questo codice di QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="b3818-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="b3818-132">2. Registrare l'applicazione DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="b3818-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="b3818-133">Per impostare l'app perché ottenga i token, è prima necessario registrarla nel tenant di Azure AD e concederle l'autorizzazione per accedere all'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3818-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="b3818-134">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3818-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3818-135">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="b3818-135">On the top bar, click your account.</span></span> <span data-ttu-id="b3818-136">Nell'elenco **Directory** scegliere il tenant di Active Directory in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b3818-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="b3818-137">Fare clic su **More Services** (Altri servizi) nel riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b3818-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b3818-138">Fare clic su **Registrazioni per l'app**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b3818-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b3818-139">Seguire le istruzioni e creare una nuova **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="b3818-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="b3818-140">Il **nome** dell'applicazione descrive l'applicazione agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="b3818-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="b3818-141">L'**URI di reindirizzamento** è una combinazione dello schema e della stringa che Azure AD usa per restituire le risposte dei token.</span><span class="sxs-lookup"><span data-stu-id="b3818-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="b3818-142">Immettere un valore specifico per l'applicazione in base alle informazioni sull'URI di reindirizzamento sopra riportate.</span><span class="sxs-lookup"><span data-stu-id="b3818-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="b3818-143">Dopo avere completato la registrazione, Azure AD assegna automaticamente all'app un ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="b3818-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="b3818-144">Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla scheda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b3818-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="b3818-145">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b3818-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="b3818-146">Selezionare **Microsoft Graph** come API e aggiungere l'autorizzazione **Lettura dati directory** in **Autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="b3818-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b3818-147">In questo modo l'applicazione potrà eseguire una query sugli utenti nell'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3818-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="b3818-148">3. Installare e configurare ADAL</span><span class="sxs-lookup"><span data-stu-id="b3818-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="b3818-149">Ora che si dispone di un'applicazione in Azure AD, è possibile installare ADAL e scrivere il codice relativo all'identità.</span><span class="sxs-lookup"><span data-stu-id="b3818-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="b3818-150">Affinché ADAL possa comunicare con Azure AD, è necessario fornirle alcune informazioni sulla registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b3818-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="b3818-151">Si può iniziare aggiungendo la libreria ADAL al progetto DirectorySearcher usando CocaPods.</span><span class="sxs-lookup"><span data-stu-id="b3818-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="b3818-152">Aggiungere il codice seguente al podfile:</span><span class="sxs-lookup"><span data-stu-id="b3818-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="b3818-153">Caricare ora il podfile usando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="b3818-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="b3818-154">Verrà creata una nuova area di lavoro XCode che sarà caricata.</span><span class="sxs-lookup"><span data-stu-id="b3818-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="b3818-155">Nel progetto QuickStart, aprire il file plist `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="b3818-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="b3818-156">Sostituire i valori degli elementi nella sezione in modo che corrispondano ai valori immessi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3818-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="b3818-157">Il codice fa riferimento a questi valori ogni volta che usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="b3818-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b3818-158">`tenant` è il dominio del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b3818-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="b3818-159">`clientId` è l'ID client dell'applicazione copiato dal portale.</span><span class="sxs-lookup"><span data-stu-id="b3818-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="b3818-160">`redirectUri` è l'URL di reindirizzamento registrato nel portale.</span><span class="sxs-lookup"><span data-stu-id="b3818-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="b3818-161">4.    Usare ADAL per ottenere i token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3818-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="b3818-162">Il principio alla base di ADAL è che l'app, ogni volta che ha bisogno di un token di accesso, deve solo chiamare un CompletionBlock `+(void) getToken : ` e ADAL fa il resto.</span><span class="sxs-lookup"><span data-stu-id="b3818-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="b3818-163">Nel progetto `QuickStart` aprire `GraphAPICaller.m` e trovare il commento `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` nella parte superiore,</span><span class="sxs-lookup"><span data-stu-id="b3818-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="b3818-164">dove si passano ad ADAL le coordinate attraverso un CompletionBlock per comunicare con Azure AD e gli si indica come memorizzare i token nella cache.</span><span class="sxs-lookup"><span data-stu-id="b3818-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="b3818-165">A questo punto è necessario usare questo token per cercare gli utenti nel grafico.</span><span class="sxs-lookup"><span data-stu-id="b3818-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="b3818-166">Trovare il commento `// TODO: implement SearchUsersList`.</span><span class="sxs-lookup"><span data-stu-id="b3818-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="b3818-167">Questo metodo invia una richiesta GET all'API Graph di Azure AD per eseguire una query sugli utenti il cui UPN inizia con il termine di ricerca specificato.</span><span class="sxs-lookup"><span data-stu-id="b3818-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="b3818-168">Per eseguire una query nell'API Graph di Azure AD, è necessario includere un oggetto access_token nell'intestazione `Authorization` della richiesta.</span><span class="sxs-lookup"><span data-stu-id="b3818-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="b3818-169">È qui che entra in gioco ADAL.</span><span class="sxs-lookup"><span data-stu-id="b3818-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="b3818-170">Quando l'app richiede un token mediante la chiamata a `getToken(...)`, ADAL tenta di restituire un token senza chiedere le credenziali all'utente.</span><span class="sxs-lookup"><span data-stu-id="b3818-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="b3818-171">Se ADAL determina che l'utente deve eseguire l'accesso per ottenere un token, visualizza una finestra di dialogo di accesso, raccoglie le credenziali dell'utente e restituisce un token al termine dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b3818-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="b3818-172">Se ADAL non può restituire un token per qualsiasi motivo, genera una `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="b3818-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="b3818-173">L'oggetto `AuthenticationResult` contiene un oggetto `tokenCacheStoreItem` che può essere usato per raccogliere informazioni che potrebbero essere richieste dall'app.</span><span class="sxs-lookup"><span data-stu-id="b3818-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="b3818-174">Nel progetto QuickStart viene usato `tokenCacheStoreItem` per determinare se l'autenticazione è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="b3818-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="b3818-175">5. Compilare ed eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="b3818-175">5. Build and run the application</span></span>
<span data-ttu-id="b3818-176">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b3818-176">Congratulations!</span></span> <span data-ttu-id="b3818-177">Si dispone ora di un'applicazione iOS funzionante in grado di autenticare gli utenti, chiamare in modo sicuro le API Web usando OAuth 2.0 e ottenere informazioni di base sull'utente.</span><span class="sxs-lookup"><span data-stu-id="b3818-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="b3818-178">Se non si è ancora popolato il tenant con alcuni utenti, ora è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="b3818-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="b3818-179">Avviare l'applicazione QuickStart e accedere come uno di questi utenti.</span><span class="sxs-lookup"><span data-stu-id="b3818-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="b3818-180">Cercare altri utenti in base al relativo UPN.</span><span class="sxs-lookup"><span data-stu-id="b3818-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="b3818-181">Chiudere l'app e avviarla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b3818-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="b3818-182">Si noti che la sessione dell'utente non è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="b3818-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="b3818-183">ADAL consente di incorporare facilmente nell'applicazione tutte queste funzionalità comuni relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="b3818-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="b3818-184">Esegue automaticamente le attività più complesse, ovvero gestione della cache, supporto del protocollo OAuth, visualizzazione all'utente di un'interfaccia utente di accesso e aggiornamento dei token scaduti.</span><span class="sxs-lookup"><span data-stu-id="b3818-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="b3818-185">Tutto ciò che occorre conoscere è una sola chiamata all'API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="b3818-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="b3818-186">L'esempio completato (senza i valori di configurazione) è disponibile in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip) per riferimento.</span><span class="sxs-lookup"><span data-stu-id="b3818-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b3818-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3818-187">Next steps</span></span>
<span data-ttu-id="b3818-188">Ora è possibile passare ad altri scenari.</span><span class="sxs-lookup"><span data-stu-id="b3818-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="b3818-189">È possibile consultare:</span><span class="sxs-lookup"><span data-stu-id="b3818-189">You may want to try:</span></span>

* [<span data-ttu-id="b3818-190">Proteggere un'API Web Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3818-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="b3818-191">Ottenere informazioni su [Come abilitare l'accesso Single Sign-On tra app in iOS usando ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="b3818-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

