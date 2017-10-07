---
title: Acquisizione di un token mediante un'applicazione iOS - Azure AD B2C | Microsoft Docs
description: "In questo articolo viene illustrato come toocreate un'app iOS che usa AppAuth con identità utente di Azure Active Directory B2C toomanage e autentica gli utenti."
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
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="35200-103">Azure AD B2C: accedere mediante un'applicazione iOS</span><span class="sxs-lookup"><span data-stu-id="35200-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="35200-104">piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="35200-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="35200-105">Utilizzando un protocollo standard aperto offre più opzioni agli sviluppatori quando si seleziona un toointegrate libreria con i servizi offerti.</span><span class="sxs-lookup"><span data-stu-id="35200-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="35200-106">È stato fornito in questa procedura dettagliata e altri simili agli sviluppatori tooaid con la scrittura di applicazioni che si connettono toohello piattaforma di Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="35200-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="35200-107">La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) della piattaforma in grado di tooconnect toohello Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="35200-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="35200-108">Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse.</span><span class="sxs-lookup"><span data-stu-id="35200-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="35200-109">In questo esempio utilizza una libreria di terze parti chiamata AppAuth che è stato testato per la compatibilità in scenari di base con hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="35200-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="35200-110">Problemi e richieste di funzionalità devono essere progetto open source toohello diretto della libreria.</span><span class="sxs-lookup"><span data-stu-id="35200-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="35200-111">Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="35200-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="35200-112">Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questo esempio di configurazione potrebbe non prevedere tooyou molto senso.</span><span class="sxs-lookup"><span data-stu-id="35200-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="35200-113">Si consiglia esaminare una breve [Panoramica del protocollo hello è stato documentato qui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="35200-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="35200-114">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="35200-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="35200-115">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="35200-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="35200-116">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="35200-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="35200-117">Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="35200-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="35200-118">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="35200-118">Create an application</span></span>
<span data-ttu-id="35200-119">Successivamente, è necessario toocreate un'app nel servizio directory B2C.</span><span class="sxs-lookup"><span data-stu-id="35200-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="35200-120">registrazione app Hello fornisce informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="35200-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="35200-121">toocreate un'app per dispositivi mobili, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="35200-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="35200-122">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="35200-122">Be sure to:</span></span>

* <span data-ttu-id="35200-123">Includere un **Native client** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="35200-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="35200-124">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="35200-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="35200-125">Questo GUID sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="35200-125">You need this GUID later.</span></span>
* <span data-ttu-id="35200-126">Configurare un **URI di reindirizzamento** con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="35200-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="35200-127">Questo URI sarà necessario in seguito.</span><span class="sxs-lookup"><span data-stu-id="35200-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="35200-128">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="35200-128">Create your policies</span></span>
<span data-ttu-id="35200-129">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="35200-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="35200-130">Questa app contiene un'esperienza di identità che combina accesso e iscrizione.</span><span class="sxs-lookup"><span data-stu-id="35200-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="35200-131">Creare i criteri come descritto nell'[articolo relativo ai criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="35200-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="35200-132">Quando si crea il criterio di hello, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="35200-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="35200-133">In **attributi iscrizione**selezionare attributo hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="35200-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="35200-134">È possibile selezionare anche altri attributi.</span><span class="sxs-lookup"><span data-stu-id="35200-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="35200-135">In **attestazioni applicazione**, selezionare le attestazioni hello **nome visualizzato** e **ID oggetto dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="35200-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="35200-136">Sono disponibili anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="35200-136">You can select other claims as well.</span></span>
* <span data-ttu-id="35200-137">Hello copia **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="35200-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="35200-138">Il nome dei criteri è preceduto da `b2c_1_` quando si salva il criterio di hello.</span><span class="sxs-lookup"><span data-stu-id="35200-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="35200-139">È necessario il nome di criterio hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="35200-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="35200-140">Dopo aver creato i criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="35200-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="35200-141">Scaricare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="35200-141">Download hello sample code</span></span>
<span data-ttu-id="35200-142">È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="35200-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="35200-143">È possibile scaricare codice hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="35200-143">You can download hello code and run it.</span></span> <span data-ttu-id="35200-144">toouse tenant proprio AD B2C Azure, seguire le istruzioni hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="35200-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="35200-145">In questo esempio è stato creato seguendo le istruzioni Leggimi hello da hello [iOS AppAuth progetto in GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="35200-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="35200-146">Per ulteriori informazioni sul funzionamento: esempio hello e libreria hello, fare riferimento a hello README AppAuth su GitHub.</span><span class="sxs-lookup"><span data-stu-id="35200-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="35200-147">Modifica toouse l'app Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="35200-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="35200-148">AppAuth supporta iOS 7 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="35200-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="35200-149">Tuttavia, è necessario toosupport social gli account di accesso Google, SFSafariViewController che richiede di iOS 9 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="35200-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="35200-150">Configurazione</span><span class="sxs-lookup"><span data-stu-id="35200-150">Configuration</span></span>

<span data-ttu-id="35200-151">È possibile configurare la comunicazione con Azure Active Directory B2C specificando l'endpoint di autorizzazione hello sia URI degli endpoint token.</span><span class="sxs-lookup"><span data-stu-id="35200-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="35200-152">toogenerate gli URI, è necessario hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="35200-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="35200-153">ID tenant (ad esempio contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="35200-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="35200-154">Nome del criterio (ad esempio B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="35200-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="35200-155">endpoint token URI può essere generato sostituendo Hello hello Tenant\_ID e hello criteri\_nome in hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="35200-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="35200-156">endpoint di autorizzazione URI può essere generato sostituendo Hello hello Tenant\_ID e hello criteri\_nome in hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="35200-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="35200-157">Hello esecuzione di codice seguente toocreate AuthorizationServiceConfiguration oggetto:</span><span class="sxs-lookup"><span data-stu-id="35200-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="35200-158">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="35200-158">Authorizing</span></span>

<span data-ttu-id="35200-159">Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="35200-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="35200-160">hello toocreate richiesta, è necessario hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="35200-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="35200-161">ID client (ad esempio 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="35200-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="35200-162">URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="35200-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="35200-163">Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="35200-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="35200-164">tooset backup la sezione relativa al toohello dei reindirizzamento di hello di applicazione toohandle con lo schema personalizzato hello URI, non è presente ' Schemes'URL' elenco hello tooupdate le Info. plist:</span><span class="sxs-lookup"><span data-stu-id="35200-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="35200-165">Aprire Info.pList.</span><span class="sxs-lookup"><span data-stu-id="35200-165">Open Info.pList.</span></span>
* <span data-ttu-id="35200-166">Passare il mouse su una riga come 'Codice di tipo del sistema operativo di Bundle' e fare clic su hello \+ simbolo.</span><span class="sxs-lookup"><span data-stu-id="35200-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="35200-167">Rinominare hello nuova riga 'URL types'.</span><span class="sxs-lookup"><span data-stu-id="35200-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="35200-168">Fare clic a sinistra di hello freccia toohello della struttura ad albero di 'Tipi URL' tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="35200-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="35200-169">Fare clic a sinistra di hello freccia toohello dell'albero di hello tooopen 'Elemento 0'.</span><span class="sxs-lookup"><span data-stu-id="35200-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="35200-170">Rinominare un elemento prima di sotto degli schemi di elemento too'URL 0.</span><span class="sxs-lookup"><span data-stu-id="35200-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="35200-171">Fare clic a sinistra di hello freccia toohello dell'albero di hello tooopen ' Schemes'URL.</span><span class="sxs-lookup"><span data-stu-id="35200-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="35200-172">Nella colonna 'Value' hello è un campo vuoto toohello sinistro 'Elemento 0' di sotto di ' Schemes'URL.</span><span class="sxs-lookup"><span data-stu-id="35200-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="35200-173">Impostare lo schema univoco dell'applicazione di hello valore tooyour.</span><span class="sxs-lookup"><span data-stu-id="35200-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="35200-174">il valore di Hello deve corrispondere schema hello utilizzato in redirectURL durante la creazione di oggetti OIDAuthorizationRequest hello.</span><span class="sxs-lookup"><span data-stu-id="35200-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="35200-175">Nel nostro esempio, abbiamo utilizzato lo schema hello 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="35200-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="35200-176">Fare riferimento toohello [AppAuth Guida](https://openid.github.io/AppAuth-iOS/) in modo toocomplete hello parte rimanente del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="35200-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="35200-177">Se è necessario tooquickly iniziare con un'app in funzione, estrarre [l'esempio](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="35200-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="35200-178">Seguire i passaggi hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter la configurazione di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="35200-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="35200-179">Ci sono sempre toofeedback aperti e i suggerimenti!</span><span class="sxs-lookup"><span data-stu-id="35200-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="35200-180">Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="35200-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="35200-181">Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="35200-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
