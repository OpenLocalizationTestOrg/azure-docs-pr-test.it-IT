---
title: 'Azure Active Directory B2C: acquisire un token mediante un''applicazione Android | Documentazione Microsoft'
description: "In questo articolo viene illustrato come toocreate un'app per Android che utilizza AppAuth con identità utente di Azure Active Directory B2C toomanage e autentica gli utenti."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="d9250-103">Azure AD B2C: accedere mediante un'applicazione Android</span><span class="sxs-lookup"><span data-stu-id="d9250-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="d9250-104">piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d9250-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d9250-105">Questo consente agli sviluppatori tooleverage qualsiasi libreria desiderano toointegrate grazie ai servizi.</span><span class="sxs-lookup"><span data-stu-id="d9250-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="d9250-106">gli sviluppatori tooaid utilizzando la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come tooconfigure 3rd party librerie tooconnect toohello Microsoft piattaforma delle identità.</span><span class="sxs-lookup"><span data-stu-id="d9250-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="d9250-107">La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sarà piattaforma di Microsoft Identity toohello tooconnect in grado di.</span><span class="sxs-lookup"><span data-stu-id="d9250-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="d9250-108">Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse.</span><span class="sxs-lookup"><span data-stu-id="d9250-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="d9250-109">In questo esempio utilizza una libreria di terze parti 3rd chiamata AppAuth che è stato testato per la compatibilità in scenari di base con hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d9250-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="d9250-110">Problemi e richieste di funzionalità devono essere progetto open source toohello diretto della libreria.</span><span class="sxs-lookup"><span data-stu-id="d9250-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="d9250-111">Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="d9250-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="d9250-112">Se si è nuovo tooOAuth2 o OpenID Connect gran parte di questo esempio di configurazione potrebbe non prevedere tooyou molto senso.</span><span class="sxs-lookup"><span data-stu-id="d9250-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="d9250-113">Si consiglia esaminare una breve [Panoramica del protocollo hello è stato documentato qui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d9250-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="d9250-114">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d9250-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="d9250-115">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="d9250-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d9250-116">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="d9250-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="d9250-117">Se non ne è già disponibile una, prima di continuare [creare una directory B2C](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="d9250-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="d9250-118">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="d9250-118">Create an application</span></span>

<span data-ttu-id="d9250-119">Successivamente, è necessario toocreate un'app nel servizio directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d9250-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="d9250-120">Vengono riportate informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="d9250-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="d9250-121">toocreate un'app per dispositivi mobili, seguire [queste istruzioni](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d9250-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="d9250-122">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="d9250-122">Be sure to:</span></span>

* <span data-ttu-id="d9250-123">Includere un **Native Client** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d9250-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="d9250-124">Hello copia **ID applicazione** ovvero tooyour assegnato app.</span><span class="sxs-lookup"><span data-stu-id="d9250-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="d9250-125">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="d9250-125">You will need this later.</span></span>
* <span data-ttu-id="d9250-126">Configurare un **URI di reindirizzamento** client nativo (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="d9250-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="d9250-127">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="d9250-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d9250-128">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="d9250-128">Create your policies</span></span>

<span data-ttu-id="d9250-129">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="d9250-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d9250-130">Questa app contiene un'esperienza di identità che combina accesso e iscrizione.</span><span class="sxs-lookup"><span data-stu-id="d9250-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="d9250-131">È necessario toocreate questo criterio, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="d9250-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="d9250-132">Quando si crea il criterio di hello, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="d9250-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="d9250-133">Scegliere hello **nome visualizzato** come un attributo nei criteri di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="d9250-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="d9250-134">Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="d9250-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="d9250-135">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="d9250-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="d9250-136">Hello copia **nome** dei criteri dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="d9250-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="d9250-137">Devono contenere il prefisso hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="d9250-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="d9250-138">È necessario il nome di criterio hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d9250-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d9250-139">Dopo aver creato i criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="d9250-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="d9250-140">Scaricare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="d9250-140">Download hello sample code</span></span>

<span data-ttu-id="d9250-141">È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d9250-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="d9250-142">È possibile scaricare codice hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="d9250-142">You can download hello code and run it.</span></span> <span data-ttu-id="d9250-143">È possibile iniziare rapidamente con la propria app utilizzando la configurazione di Azure Active Directory B2C seguendo le istruzioni hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d9250-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="d9250-144">esempio Hello è una variante dell'esempio hello fornito da [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="d9250-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="d9250-145">Visitare il loro toolearn pagina informazioni su AppAuth e delle relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d9250-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="d9250-146">Modifica toouse l'app Azure AD B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="d9250-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="d9250-147">AppAuth supporta l'API 16 (Jellybean) di Android e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d9250-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="d9250-148">Si consiglia di usare l'API 23 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d9250-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="d9250-149">Configurazione</span><span class="sxs-lookup"><span data-stu-id="d9250-149">Configuration</span></span>

<span data-ttu-id="d9250-150">È possibile configurare la comunicazione con Azure Active Directory B2C mediante l'individuazione di hello specificando URI o specificando l'endpoint di autorizzazione hello sia URI degli endpoint token.</span><span class="sxs-lookup"><span data-stu-id="d9250-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="d9250-151">In entrambi i casi, è necessario hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d9250-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="d9250-152">ID tenant (ad esempio contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="d9250-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="d9250-153">Nome del criterio (ad esempio B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="d9250-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="d9250-154">Se si sceglie tooautomatically individuare hello token e l'autorizzazione URI degli endpoint, è necessario toofetch informazioni dall'individuazione hello URI.</span><span class="sxs-lookup"><span data-stu-id="d9250-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="d9250-155">individuazione di Hello URI può essere generato sostituendo hello Tenant\_ID e hello criteri\_nome in hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="d9250-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="d9250-156">È quindi possibile acquisire autorizzazione hello e URI degli endpoint token e creare un oggetto AuthorizationServiceConfiguration eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="d9250-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="d9250-157">Anziché utilizzare l'autorizzazione di hello tooobtain individuazione e l'URI degli endpoint token, è inoltre possibile specificare tali in modo esplicito sostituendo hello Tenant\_ID e hello criteri\_nome hello dell'URL di seguito:</span><span class="sxs-lookup"><span data-stu-id="d9250-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="d9250-158">Hello esecuzione di codice seguente toocreate AuthorizationServiceConfiguration oggetto:</span><span class="sxs-lookup"><span data-stu-id="d9250-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="d9250-159">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="d9250-159">Authorizing</span></span>

<span data-ttu-id="d9250-160">Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="d9250-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="d9250-161">hello toocreate richiesta, sarà necessario hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d9250-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="d9250-162">ID client (ad esempio 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="d9250-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="d9250-163">URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="d9250-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="d9250-164">Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="d9250-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="d9250-165">Consultare toohello [AppAuth Guida](https://openid.github.io/AppAuth-Android/) in modo toocomplete hello parte rimanente del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="d9250-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="d9250-166">Se è necessario tooquickly iniziare con un'app in funzione, estrarre [l'esempio](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d9250-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="d9250-167">Seguire i passaggi hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter la configurazione di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d9250-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="d9250-168">Ci sono sempre toofeedback aperti e i suggerimenti!</span><span class="sxs-lookup"><span data-stu-id="d9250-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="d9250-169">Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="d9250-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="d9250-170">Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="d9250-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

