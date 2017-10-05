---
title: Acquisizione di un token mediante un'applicazione iOS - Azure AD B2C | Microsoft Docs
description: "Questo articolo spiega come creare un'app per iOS che usa AppAuth con Azure Active Directory B2C per gestire le identità utente e l'autenticazione degli utenti."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="b5e55-103">Azure AD B2C: accedere mediante un'applicazione iOS</span><span class="sxs-lookup"><span data-stu-id="b5e55-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="b5e55-104">La piattaforma delle identità Microsoft usa standard aperti, ad esempio OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="b5e55-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="b5e55-105">L'uso di un protocollo a standard aperto offre più scelta allo sviluppatore nella selezione della libreria da integrare con i nostri servizi.</span><span class="sxs-lookup"><span data-stu-id="b5e55-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="b5e55-106">Abbiamo fornito questa procedura dettagliata e altre simili per aiutare gli sviluppatori a scrivere applicazioni che si connettono alla piattaforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="b5e55-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="b5e55-107">La maggior parte delle librerie che implementano la [specifica OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) può connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5e55-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="b5e55-108">Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse.</span><span class="sxs-lookup"><span data-stu-id="b5e55-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="b5e55-109">In questo esempio si usa una libreria di terze parti chiamata AppAuth che è stata testata per la compatibilità in scenari di base con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b5e55-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="b5e55-110">Le richieste relative a problemi e funzionalità devono essere indirizzate al progetto open source della libreria.</span><span class="sxs-lookup"><span data-stu-id="b5e55-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="b5e55-111">Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="b5e55-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="b5e55-112">Se non si ha familiarità con OAuth2 o OpenID, gran parte di questo esempio risulterà poco chiara.</span><span class="sxs-lookup"><span data-stu-id="b5e55-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="b5e55-113">È consigliabile vedere la breve [panoramica del protocollo documentata qui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b5e55-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="b5e55-114">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b5e55-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="b5e55-115">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="b5e55-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="b5e55-116">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="b5e55-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="b5e55-117">Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="b5e55-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="b5e55-118">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="b5e55-118">Create an application</span></span>
<span data-ttu-id="b5e55-119">Successivamente, è necessario creare un'app nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="b5e55-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="b5e55-120">La registrazione dell'app fornisce ad Azure AD le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="b5e55-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="b5e55-121">Per creare un'app per dispositivi mobili, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b5e55-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="b5e55-122">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="b5e55-122">Be sure to:</span></span>

* <span data-ttu-id="b5e55-123">Includere un **client nativo** nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5e55-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="b5e55-124">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="b5e55-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="b5e55-125">Questo GUID sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="b5e55-125">You need this GUID later.</span></span>
* <span data-ttu-id="b5e55-126">Configurare un **URI di reindirizzamento** con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="b5e55-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="b5e55-127">Questo URI sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="b5e55-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="b5e55-128">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="b5e55-128">Create your policies</span></span>
<span data-ttu-id="b5e55-129">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="b5e55-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="b5e55-130">Questa app contiene un'esperienza di identità che combina accesso e iscrizione.</span><span class="sxs-lookup"><span data-stu-id="b5e55-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="b5e55-131">Creare i criteri come descritto nell'[articolo relativo ai criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="b5e55-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="b5e55-132">Durante la creazione dei criteri, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="b5e55-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="b5e55-133">In **Attributi iscrizione** selezionare l'attributo **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="b5e55-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="b5e55-134">È possibile selezionare anche altri attributi.</span><span class="sxs-lookup"><span data-stu-id="b5e55-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="b5e55-135">In **Attestazioni applicazione** selezionare **Nome visualizzato** e **ID oggetto dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="b5e55-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="b5e55-136">Sono disponibili anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="b5e55-136">You can select other claims as well.</span></span>
* <span data-ttu-id="b5e55-137">Copiare il **Nome** di ogni criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="b5e55-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="b5e55-138">Quando si salva il criterio, al relativo nome viene aggiunto un prefisso `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="b5e55-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="b5e55-139">Il nome dei criteri sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="b5e55-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="b5e55-140">Dopo aver creato i criteri, è possibile passare alla creazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b5e55-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="b5e55-141">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="b5e55-141">Download the sample code</span></span>
<span data-ttu-id="b5e55-142">È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="b5e55-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="b5e55-143">È possibile scaricare ed eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="b5e55-143">You can download the code and run it.</span></span> <span data-ttu-id="b5e55-144">Per usare il proprio tenant Azure AD B2C, seguire le istruzioni riportate in [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="b5e55-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="b5e55-145">Questo esempio è stato creato seguendo le istruzioni del file README del [progetto iOS AppAuth in GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="b5e55-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="b5e55-146">Per altre informazioni sul funzionamento dell'esempio e della libreria, fare riferimento al file README di AppAuth in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5e55-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="b5e55-147">Modifica dell'app per usare Azure Active Directory B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="b5e55-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="b5e55-148">AppAuth supporta iOS 7 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b5e55-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="b5e55-149">Tuttavia, per supportare gli accessi da social network su Google, è necessario SFSafariViewController che richiede iOS 9 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b5e55-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="b5e55-150">Configurazione</span><span class="sxs-lookup"><span data-stu-id="b5e55-150">Configuration</span></span>

<span data-ttu-id="b5e55-151">È possibile configurare la comunicazione con Azure AD B2C specificando sia l'URI dell'endpoint di autorizzazione che quello dell'endpoint di token.</span><span class="sxs-lookup"><span data-stu-id="b5e55-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="b5e55-152">Per generare questi URI sono necessarie le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5e55-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="b5e55-153">ID tenant (ad esempio contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="b5e55-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="b5e55-154">Nome del criterio (ad esempio B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="b5e55-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="b5e55-155">L'URI dell'endpoint di token può essere generato mediante la sostituzione dell'ID\_tenant e del nome\_criterio nell'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="b5e55-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="b5e55-156">L'URI dell'endpoint di autorizzazione può essere generato mediante la sostituzione dell'ID\_tenant e del nome\_criterio nell'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="b5e55-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="b5e55-157">Eseguire il codice seguente per creare l'oggetto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="b5e55-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="b5e55-158">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b5e55-158">Authorizing</span></span>

<span data-ttu-id="b5e55-159">Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b5e55-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="b5e55-160">Per creare la richiesta sono necessarie le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5e55-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="b5e55-161">ID client (ad esempio 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="b5e55-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="b5e55-162">URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="b5e55-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="b5e55-163">Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="b5e55-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="b5e55-164">Per configurare l'applicazione per la gestione del reindirizzamento all'URI con lo schema personalizzato, è necessario aggiornare l'elenco degli "Schemi URL" in Info.pList:</span><span class="sxs-lookup"><span data-stu-id="b5e55-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="b5e55-165">Aprire Info.pList.</span><span class="sxs-lookup"><span data-stu-id="b5e55-165">Open Info.pList.</span></span>
* <span data-ttu-id="b5e55-166">Passare il mouse su una riga come "Codice del tipo di sistema operativo del creatore del bundle" e fare clic sul simbolo \+.</span><span class="sxs-lookup"><span data-stu-id="b5e55-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="b5e55-167">Rinominare la nuova riga come "Tipi di URL".</span><span class="sxs-lookup"><span data-stu-id="b5e55-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="b5e55-168">Fare clic sulla freccia a sinistra di "Tipi di URL" per aprire l'albero.</span><span class="sxs-lookup"><span data-stu-id="b5e55-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="b5e55-169">Fare clic sulla freccia a sinistra di "Elemento 0" per aprire l'albero.</span><span class="sxs-lookup"><span data-stu-id="b5e55-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="b5e55-170">Rinominare il primo elemento sotto l'elemento 0 in "Schemi URL".</span><span class="sxs-lookup"><span data-stu-id="b5e55-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="b5e55-171">Fare clic sulla freccia a sinistra di "Schemi URL" per aprire l'albero.</span><span class="sxs-lookup"><span data-stu-id="b5e55-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="b5e55-172">Nella colonna "Valore" è presente un campo vuoto a sinistra di "Elemento 0" sotto "Schemi URL".</span><span class="sxs-lookup"><span data-stu-id="b5e55-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="b5e55-173">Impostare il valore sullo schema univoco dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5e55-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="b5e55-174">Il valore deve corrispondere allo schema usato in redirectURL quando si crea l'oggetto OIDAuthorizationRequest.</span><span class="sxs-lookup"><span data-stu-id="b5e55-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="b5e55-175">Nel nostro esempio abbiamo usato lo schema "com.onmicrosoft.fabrikamb2c.exampleapp".</span><span class="sxs-lookup"><span data-stu-id="b5e55-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="b5e55-176">Per informazioni su come completare il resto della procedura, consultare la [guida di AppAuth](https://openid.github.io/AppAuth-iOS/).</span><span class="sxs-lookup"><span data-stu-id="b5e55-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="b5e55-177">Se è necessario iniziare subito con un'app funzionante, vedere [il nostro esempio](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="b5e55-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="b5e55-178">Seguire i passaggi indicati in [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) per immettere la configurazione di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b5e55-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="b5e55-179">Commenti e suggerimenti sono sempre graditi.</span><span class="sxs-lookup"><span data-stu-id="b5e55-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="b5e55-180">In caso di difficoltà con questo argomento o di suggerimenti per migliorarne il contenuto, è possibile lasciare un commento nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="b5e55-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="b5e55-181">Le richieste di funzionalità possono essere aggiunte in [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="b5e55-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
