---
title: app per Android v 2.0 aaaAzure Active Directory | Documenti Microsoft
description: Come un'app per Android che esegue l'accesso agli utenti con personali account Microsoft e lavoro o scuola e chiamate toobuild hello API Graph usando le librerie di terze parti.
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="8b31f-103">Aggiungere app per Android tooan Accedi con l'API Graph utilizzando hello v 2.0 endpoint di una libreria di terze parti</span><span class="sxs-lookup"><span data-stu-id="8b31f-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="8b31f-104">piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8b31f-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="8b31f-105">Gli sviluppatori possono utilizzare qualsiasi libreria desiderano toointegrate grazie ai servizi.</span><span class="sxs-lookup"><span data-stu-id="8b31f-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="8b31f-106">gli sviluppatori di toohelp utilizzano la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come piattaforma delle identità Microsoft tooconnect toohello tooconfigure librerie di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8b31f-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="8b31f-107">La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) possono connettersi toohello piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8b31f-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="8b31f-108">Con un'applicazione hello creati in questa procedura dettagliata, gli utenti possano accedere tootheir organizzazione e quindi cercare autonomamente nella propria organizzazione tramite l'API Graph hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="8b31f-109">Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questa configurazione di esempio può non avere senso tooyou.</span><span class="sxs-lookup"><span data-stu-id="8b31f-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="8b31f-110">Per approfondimenti, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8b31f-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="8b31f-111">Alcune funzionalità di piattaforma che dispone di un'espressione in hello OAuth2 o OpenID Connect standard, ad esempio l'accesso condizionale e gestione di criteri di Intune, richiedono si toouse l'open source di librerie di identità di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8b31f-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="8b31f-112">endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8b31f-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="8b31f-113">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8b31f-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="8b31f-114">Scaricare codice hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="8b31f-114">Download hello code from GitHub</span></span>
<span data-ttu-id="8b31f-115">codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="8b31f-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="8b31f-116">toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o scheletro hello clone:</span><span class="sxs-lookup"><span data-stu-id="8b31f-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="8b31f-117">È possibile anche scaricare l'esempio di hello e iniziare subito:</span><span class="sxs-lookup"><span data-stu-id="8b31f-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="8b31f-118">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="8b31f-118">Register an app</span></span>
<span data-ttu-id="8b31f-119">Creare una nuova app hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire hello i passaggi dettagliati in [come un'app con endpoint v 2.0 hello tooregister](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8b31f-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="8b31f-120">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="8b31f-120">Make sure to:</span></span>

* <span data-ttu-id="8b31f-121">Hello copia **Id applicazione** che è assegnato tooyour app perché è necessario prima.</span><span class="sxs-lookup"><span data-stu-id="8b31f-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="8b31f-122">Aggiungere hello **Mobile** piattaforma per l'app.</span><span class="sxs-lookup"><span data-stu-id="8b31f-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="8b31f-123">Nota: portale di registrazione applicazione hello fornisce un **URI di reindirizzamento** valore.</span><span class="sxs-lookup"><span data-stu-id="8b31f-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="8b31f-124">Tuttavia, in questo esempio è necessario utilizzare il valore predefinito hello di `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="8b31f-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="8b31f-125">Scaricare una libreria di terze parti NXOAuth2 hello e creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="8b31f-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="8b31f-126">Questa procedura dettagliata, si utilizzerà hello OIDCAndroidLib da GitHub, ovvero una raccolta di OAuth2 basata su hello codice OpenID Connect di Google.</span><span class="sxs-lookup"><span data-stu-id="8b31f-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="8b31f-127">Implementa il profilo di applicazione nativa hello e supporta l'endpoint di autorizzazione hello dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="8b31f-128">Questi sono tutti aspetti di hello che dovrai toointegrate con la piattaforma di identità Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="8b31f-129">Clonare computer tooyour di hello OIDCAndroidLib repository.</span><span class="sxs-lookup"><span data-stu-id="8b31f-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="8b31f-131">Configurare l'ambiente Android Studio</span><span class="sxs-lookup"><span data-stu-id="8b31f-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="8b31f-132">Creare un nuovo progetto Android Studio e accettare le impostazioni predefinite nella procedura guidata hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Creare un nuovo progetto in Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Target Android devices (Dispositivi Android di destinazione)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Aggiungere un'attività toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="8b31f-136">tooset dei moduli del progetto, spostare hello clonato repository toohello percorso del progetto.</span><span class="sxs-lookup"><span data-stu-id="8b31f-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="8b31f-137">È possibile anche creare progetto hello e clonare direttamente toohello percorso del progetto.</span><span class="sxs-lookup"><span data-stu-id="8b31f-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="8b31f-139">Aprire le impostazioni dei moduli di hello progetto utilizzando il menu di scelta rapida hello o tramite hello di scelta rapida Ctrl + Alt + Maj + S.</span><span class="sxs-lookup"><span data-stu-id="8b31f-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Impostazioni dei moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="8b31f-141">Rimuovere il modulo di applicazione predefinito di hello perché si vuole solo le impostazioni dei contenitori progetto hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![modulo di applicazione Hello predefinito](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="8b31f-143">Importare i moduli dal progetto corrente toohello di hello repository clonato.</span><span class="sxs-lookup"><span data-stu-id="8b31f-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="8b31f-144">![Progetto di importazione gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crea una nuova pagina modulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="8b31f-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="8b31f-145">Ripetere questi passaggi per hello `oidlib-sample` modulo.</span><span class="sxs-lookup"><span data-stu-id="8b31f-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="8b31f-146">Controllare le dipendenze oidclib hello hello `oidlib-sample` modulo.</span><span class="sxs-lookup"><span data-stu-id="8b31f-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![dipendenze oidclib modulo oidlib esempio hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="8b31f-148">Fare clic su **OK** e attendere la sincronizzazione di Gradle.</span><span class="sxs-lookup"><span data-stu-id="8b31f-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="8b31f-149">Il file settings.gradle sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8b31f-149">Your settings.gradle should look like:</span></span>
   
    ![Schermata di settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="8b31f-151">Compilare hello toomake app di esempio che tale esempio hello correttamente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8b31f-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="8b31f-152">Si sarà in grado di toouse questo con Azure Active Directory ancora.</span><span class="sxs-lookup"><span data-stu-id="8b31f-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="8b31f-153">È necessario tooconfigure alcuni endpoint prima.</span><span class="sxs-lookup"><span data-stu-id="8b31f-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="8b31f-154">Si tratta di tooensure non è di un problemi di Android Studio, prima di iniziare la personalizzazione di app di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="8b31f-155">Compilare ed eseguire `oidlib-sample` come destinazione di hello in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="8b31f-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Progresso della compilazione oidlib di esempio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="8b31f-157">Eliminare hello `app ` directory in cui è stato lasciato quando modulo hello rimosso dal progetto hello perché Android Studio non viene eliminato per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8b31f-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Struttura dei file che include directory dell'applicazione hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="8b31f-159">Aprire hello **modificare configurazioni** configurazione di hello eseguire tooremove menu che è stato lasciato anche quando il modulo hello è stata rimossa dal progetto hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="8b31f-160">![Menu Edit Configurations (Modifica configurazioni)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Configurazione di esecuzione dell'app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="8b31f-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="8b31f-161">Configurare gli endpoint hello dell'esempio hello</span><span class="sxs-lookup"><span data-stu-id="8b31f-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="8b31f-162">Dopo aver creato hello `oidlib-sample` eseguite correttamente, modifica alcuni tooget endpoint questo utilizzo di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b31f-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="8b31f-163">Configurare il client modificando il file di oidc_clientconf.xml hello</span><span class="sxs-lookup"><span data-stu-id="8b31f-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="8b31f-164">Poiché si utilizza OAuth2 flussi solo tooget un token e chiama l'API Graph hello, impostare hello client toodo OAuth2 solo.</span><span class="sxs-lookup"><span data-stu-id="8b31f-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="8b31f-165">OIDC verrà illustrato in un esempio successivo.</span><span class="sxs-lookup"><span data-stu-id="8b31f-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="8b31f-166">Configurare l'ID client ricevuto dal portale di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b31f-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="8b31f-167">Configurare l'URI di reindirizzamento con hello uno sotto.</span><span class="sxs-lookup"><span data-stu-id="8b31f-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="8b31f-168">Configurare gli ambiti che è necessario in ordine tooaccess hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="8b31f-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="8b31f-169">Hello `User.Read` valore `oidc_scopes` consente si tooread hello profilo di base hello effettuato l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="8b31f-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="8b31f-170">Maggiori informazioni su tutti gli ambiti disponibili hello in [gli ambiti di autorizzazione di Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="8b31f-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="8b31f-171">Se si necessita di spiegazioni sugli ambiti `openid` o `offline_access` in OpenID Connect, vedere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8b31f-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="8b31f-172">Configurare gli endpoint client modificando il file di oidc_endpoints.xml hello</span><span class="sxs-lookup"><span data-stu-id="8b31f-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="8b31f-173">Aprire hello `oidc_endpoints.xml` file e apportare hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="8b31f-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="8b31f-174">Se si usa OAuth2 come protocollo, questi endpoint non devono mai essere modificati.</span><span class="sxs-lookup"><span data-stu-id="8b31f-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="8b31f-175">gli endpoint per Hello `userInfoEndpoint` e `revocationEndpoint` non sono attualmente supportate da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b31f-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="8b31f-176">Se si lascia queste con il valore di example.com hello predefinito, verrà ricordato che non sono disponibili in: esempio hello :-)</span><span class="sxs-lookup"><span data-stu-id="8b31f-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="8b31f-177">Configurare una chiamata API Graph</span><span class="sxs-lookup"><span data-stu-id="8b31f-177">Configure a Graph API call</span></span>
* <span data-ttu-id="8b31f-178">Aprire hello `HomeActivity.java` file e apportare hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="8b31f-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="8b31f-179">In questo caso una semplice chiamata all'API Graph restituisce le informazioni.</span><span class="sxs-lookup"><span data-stu-id="8b31f-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="8b31f-180">Queste sono tutte le modifiche di hello che è necessario toodo.</span><span class="sxs-lookup"><span data-stu-id="8b31f-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="8b31f-181">Eseguire hello `oidlib-sample` applicazione e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="8b31f-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="8b31f-182">Dopo aver completata l'autenticazione, selezionare hello **richiesta risorsa protetta** pulsante tootest il toohello chiamata API Graph.</span><span class="sxs-lookup"><span data-stu-id="8b31f-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="8b31f-183">Ottenere aggiornamenti della sicurezza per il prodotto</span><span class="sxs-lookup"><span data-stu-id="8b31f-183">Get security updates for our product</span></span>
<span data-ttu-id="8b31f-184">Si consiglia di notifiche tooget sugli eventi di sicurezza, visitare hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="8b31f-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

