---
title: 'Azure Active Directory B2C: acquisire un token mediante un''applicazione Android | Documentazione Microsoft'
description: "Questo articolo spiega come creare un'app per Android che usa AppAuth con Azure Active Directory B2C per gestire le identità utente e l'autenticazione degli utenti."
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
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="e2aa8-103">Azure AD B2C: accedere mediante un'applicazione Android</span><span class="sxs-lookup"><span data-stu-id="e2aa8-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="e2aa8-104">La piattaforma delle identità Microsoft usa standard aperti, ad esempio OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="e2aa8-105">Questo consente agli sviluppatori di sfruttare le librerie che vogliono integrare con i servizi.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="e2aa8-106">Per aiutare gli sviluppatori a usare la piattaforma con altre librerie, sono state scritte alcune procedure dettagliate come questa, che illustrano come configurare le librerie di terze parti per connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="e2aa8-107">La maggior parte delle librerie che implementano la [specifica OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) potrà connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="e2aa8-108">Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="e2aa8-109">In questo esempio si usa una libreria di terze parti chiamata AppAuth che è stata testata per la compatibilità in scenari di base con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="e2aa8-110">Le richieste relative a problemi e funzionalità devono essere indirizzate al progetto open source della libreria.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="e2aa8-111">Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="e2aa8-112">Se non si ha familiarità con OAuth2 o OpenID, gran parte di questo esempio risulterà poco chiara.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="e2aa8-113">È consigliabile vedere la breve [panoramica del protocollo documentata qui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="e2aa8-114">Ottenere una directory di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e2aa8-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="e2aa8-115">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="e2aa8-116">Una directory è un contenitore per utenti, app, gruppi e così via.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="e2aa8-117">Se non ne è già disponibile una, prima di continuare [creare una directory B2C](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="e2aa8-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="e2aa8-118">Creare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="e2aa8-118">Create an application</span></span>

<span data-ttu-id="e2aa8-119">Successivamente, è necessario creare un'app nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="e2aa8-120">In questo modo Azure AD acquisisce le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="e2aa8-121">Per creare un'app per dispositivi mobili, [seguire questa procedura](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="e2aa8-122">Assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-122">Be sure to:</span></span>

* <span data-ttu-id="e2aa8-123">Includere un **client nativo** nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="e2aa8-124">Copiare l' **ID applicazione** assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="e2aa8-125">che sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-125">You will need this later.</span></span>
* <span data-ttu-id="e2aa8-126">Configurare un **URI di reindirizzamento** client nativo (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="e2aa8-127">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="e2aa8-128">Creare i criteri</span><span class="sxs-lookup"><span data-stu-id="e2aa8-128">Create your policies</span></span>

<span data-ttu-id="e2aa8-129">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e2aa8-130">Questa app contiene un'esperienza di identità che combina accesso e iscrizione.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="e2aa8-131">È necessario creare i criteri, come descritto nell'[articolo di riferimento per i criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="e2aa8-132">Durante la creazione dei criteri, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="e2aa8-133">Scegliere **Nome visualizzato** come attributo di iscrizione nei criteri.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="e2aa8-134">Scegliere le attestazioni dell'applicazione **Nome visualizzato** e **ID oggetto** in tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="e2aa8-135">È consentito scegliere anche altre attestazioni.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="e2aa8-136">Copiare il **Nome** di ogni criterio dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="e2aa8-137">Dovrebbero mostrare il prefisso `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="e2aa8-138">Il nome dei criteri sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="e2aa8-139">Dopo aver creato i criteri, è possibile passare alla creazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="e2aa8-140">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="e2aa8-140">Download the sample code</span></span>

<span data-ttu-id="e2aa8-141">È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="e2aa8-142">È possibile scaricare ed eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-142">You can download the code and run it.</span></span> <span data-ttu-id="e2aa8-143">Si può iniziare rapidamente con la propria app usando la configurazione di Azure Active Directory B2C con le istruzioni riportare in [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="e2aa8-144">L'esempio è una versione modificata di quello fornito da [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="e2aa8-145">Visitare la pagina per altre informazioni su AppAuth e le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="e2aa8-146">Modifica dell'app per usare Azure Active Directory B2C con AppAuth</span><span class="sxs-lookup"><span data-stu-id="e2aa8-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="e2aa8-147">AppAuth supporta l'API 16 (Jellybean) di Android e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="e2aa8-148">Si consiglia di usare l'API 23 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="e2aa8-149">Configurazione</span><span class="sxs-lookup"><span data-stu-id="e2aa8-149">Configuration</span></span>

<span data-ttu-id="e2aa8-150">È possibile configurare la comunicazione con Azure AD B2C specificando l'URI di individuazione o specificando sia l'URI dell'endpoint di autorizzazione che quello dell'endpoint di token.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="e2aa8-151">In ogni caso sarà necessario specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="e2aa8-152">ID tenant (ad esempio contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="e2aa8-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="e2aa8-153">Nome del criterio (ad esempio B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="e2aa8-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="e2aa8-154">Se si sceglie di individuare automaticamente gli URI degli endpoint di autorizzazione e di token, è necessario recuperare le informazioni dall'URI di individuazione.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="e2aa8-155">L'URI di individuazione può essere generato mediante la sostituzione dell'ID\_tenant e del nome\_criterio nell'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="e2aa8-156">È quindi possibile acquisire gli URI degli endpoint di autorizzazione e di token e creare un oggetto AuthorizationServiceConfiguration eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

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
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="e2aa8-157">Anziché usare l'individuazione per ottenere gli URI degli endpoint di autorizzazione e di token, è possibile anche specificarli in modo esplicito mediante la sostituzione dell'ID\_tenant e del nome\_criterio negli URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="e2aa8-158">Eseguire il codice seguente per creare l'oggetto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="e2aa8-159">Autorizzazione</span><span class="sxs-lookup"><span data-stu-id="e2aa8-159">Authorizing</span></span>

<span data-ttu-id="e2aa8-160">Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="e2aa8-161">Per creare la richiesta sono necessarie le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2aa8-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="e2aa8-162">ID client (ad esempio 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="e2aa8-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="e2aa8-163">URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="e2aa8-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="e2aa8-164">Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="e2aa8-165">Per informazioni su come completare il resto della procedura, consultare la [guida di AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="e2aa8-166">Se è necessario iniziare subito con un'app funzionante, vedere [il nostro esempio](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="e2aa8-167">Seguire i passaggi indicati in [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) per immettere la configurazione di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="e2aa8-168">Commenti e suggerimenti sono sempre graditi.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="e2aa8-169">In caso di difficoltà con questo argomento o di suggerimenti per migliorarne il contenuto, è possibile lasciare un commento nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="e2aa8-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="e2aa8-170">Le richieste di funzionalità possono essere aggiunte in [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="e2aa8-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

