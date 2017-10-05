---
title: App Android v2.0 di Azure Active Directory | Documentazione Microsoft
description: Come compilare un'app per Android che consente agli utenti di accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione e chiama l'API Graph usando librerie di terze parti.
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="8118b-103">Aggiungere informazioni di accesso a un'app Android usando una libreria di terze parti con l'API Graph mediante l'endpoint v2.0</span><span class="sxs-lookup"><span data-stu-id="8118b-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="8118b-104">La piattaforma delle identità Microsoft usa standard aperti, ad esempio OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8118b-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="8118b-105">Gli sviluppatori possono usare qualsiasi libreria che desiderano integrare ai servizi.</span><span class="sxs-lookup"><span data-stu-id="8118b-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="8118b-106">Per aiutare gli sviluppatori a usare la piattaforma con altre librerie, sono state scritte alcune procedure dettagliate come questa, che illustrano come configurare le librerie di terze parti per connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8118b-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="8118b-107">La maggior parte delle librerie che implementano [la specifica OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) possono connettersi alla piattaforma delle identità Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8118b-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="8118b-108">Con l'applicazione creata in questa procedura dettagliata, gli utenti possono accedere alla propria organizzazione e cercare in modo indipendente all'interno dell'organizzazione tramite l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="8118b-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="8118b-109">Se non si ha familiarità con OAuth2 o OpenID Connect, gran parte di questo esempio risulterà poco chiara.</span><span class="sxs-lookup"><span data-stu-id="8118b-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="8118b-110">Per approfondimenti, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8118b-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="8118b-111">Per alcune funzionalità della piattaforma che trovano espressione negli standard OAuth2 o OpenID Connect, ad esempio l'accesso condizionale e la gestione criteri di Intune, è necessario usare le librerie di identità open source di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8118b-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="8118b-112">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="8118b-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="8118b-113">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8118b-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="8118b-114">Scaricare il codice da GitHub</span><span class="sxs-lookup"><span data-stu-id="8118b-114">Download the code from GitHub</span></span>
<span data-ttu-id="8118b-115">Il codice per questa esercitazione è salvato [su GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="8118b-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="8118b-116">Per seguire la procedura è possibile [scaricare la struttura dell'app come file con estensione zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o clonare la struttura:</span><span class="sxs-lookup"><span data-stu-id="8118b-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="8118b-117">È anche possibile scaricare l'esempio e iniziare subito:</span><span class="sxs-lookup"><span data-stu-id="8118b-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="8118b-118">Registrare un'app</span><span class="sxs-lookup"><span data-stu-id="8118b-118">Register an app</span></span>
<span data-ttu-id="8118b-119">Creare una nuova app nel [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o seguire la procedura riportata in [Come registrare un'app con l'endpoint v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8118b-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="8118b-120">Verificare di:</span><span class="sxs-lookup"><span data-stu-id="8118b-120">Make sure to:</span></span>

* <span data-ttu-id="8118b-121">Copiare l' **ID applicazione** assegnato all'app, perché verrà richiesto a breve.</span><span class="sxs-lookup"><span data-stu-id="8118b-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="8118b-122">Aggiungere la piattaforma **Mobile** per l'app.</span><span class="sxs-lookup"><span data-stu-id="8118b-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="8118b-123">Nota: il portale di registrazione delle applicazioni offre un valore per **URI di reindirizzamento** .</span><span class="sxs-lookup"><span data-stu-id="8118b-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="8118b-124">In questo esempio, tuttavia, è necessario usare il valore predefinito `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="8118b-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="8118b-125">Scaricare la libreria di terze parti NXOAuth2 e creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="8118b-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="8118b-126">Per questa procedura dettagliata si userà OIDCAndroidLib da GitHub, una libreria OAuth2 basata sul codice OpenID Connect di Google.</span><span class="sxs-lookup"><span data-stu-id="8118b-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="8118b-127">Questa libreria implementa il profilo dell'applicazione nativa e supporta l'endpoint di autorizzazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8118b-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="8118b-128">Ecco tutto ciò che serve per l'integrazione con la piattaforma delle identità di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8118b-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="8118b-129">Clonare il repository OIDCAndroidLib sul computer.</span><span class="sxs-lookup"><span data-stu-id="8118b-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="8118b-131">Configurare l'ambiente Android Studio</span><span class="sxs-lookup"><span data-stu-id="8118b-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="8118b-132">Creare un nuovo progetto Android Studio e accettare le impostazioni predefinite nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="8118b-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Creare un nuovo progetto in Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Target Android devices (Dispositivi Android di destinazione)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Aggiungere un'attività a un dispositivo mobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="8118b-136">Per impostare i moduli del progetto, spostare il repository clonato nel percorso del progetto.</span><span class="sxs-lookup"><span data-stu-id="8118b-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="8118b-137">È anche possibile creare il progetto e clonarlo direttamente nel percorso del progetto.</span><span class="sxs-lookup"><span data-stu-id="8118b-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="8118b-139">Aprire le impostazioni dei moduli del progetto tramite il menu di scelta rapida o tramite la combinazione di tasti Ctrl+Alt+Maj+S.</span><span class="sxs-lookup"><span data-stu-id="8118b-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Impostazioni dei moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="8118b-141">Dal momento che sono necessarie solo le impostazioni del contenitore del progetto, rimuovere il modulo dell'app predefinito.</span><span class="sxs-lookup"><span data-stu-id="8118b-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![Modulo predefinito dell'app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="8118b-143">Importare i moduli dal repository clonato al progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="8118b-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="8118b-144">![Progetto di importazione gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crea una nuova pagina modulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="8118b-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="8118b-145">Ripetere questi passaggi per il modulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="8118b-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="8118b-146">Controllare le dipendenze di oidclib del modulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="8118b-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![Dipendenze oidclib sul modulo oidlib di esempio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="8118b-148">Fare clic su **OK** e attendere la sincronizzazione di Gradle.</span><span class="sxs-lookup"><span data-stu-id="8118b-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="8118b-149">Il file settings.gradle sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8118b-149">Your settings.gradle should look like:</span></span>
   
    ![Schermata di settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="8118b-151">Compilare l'app di esempio per verificare che l'esempio venga eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="8118b-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="8118b-152">Non sarà ancora possibile usarlo con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8118b-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="8118b-153">Prima è necessario configurare alcuni endpoint</span><span class="sxs-lookup"><span data-stu-id="8118b-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="8118b-154">per assicurarsi di non avere problemi con Android Studio prima di iniziare a personalizzare l'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="8118b-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="8118b-155">Compilare ed eseguire `oidlib-sample` come destinazione in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="8118b-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Progresso della compilazione oidlib di esempio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="8118b-157">Eliminare la directory `app ` rimasta dopo la rimozione del modulo dal progetto perché Android Studio non la elimina per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8118b-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Struttura dei file che include la directory dell'applicazione](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="8118b-159">Aprire il menu **Edit Configurations** (Modifica configurazioni) per rimuovere la configurazione di esecuzione rimasta dopo la rimozione del modulo dal progetto.</span><span class="sxs-lookup"><span data-stu-id="8118b-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="8118b-160">![Menu Edit Configurations (Modifica configurazioni)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Configurazione di esecuzione dell'app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="8118b-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="8118b-161">Configurare gli endpoint dell'esempio</span><span class="sxs-lookup"><span data-stu-id="8118b-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="8118b-162">Ora che `oidlib-sample` è correttamente in esecuzione, verranno modificati alcuni endpoint per l'integrazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8118b-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="8118b-163">Configurare il client modificando il file oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="8118b-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="8118b-164">Poiché si stanno usando solo flussi OAuth2 per ottenere un token e chiamare l'API Graph, impostare il client solo per eseguire OAuth2.</span><span class="sxs-lookup"><span data-stu-id="8118b-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="8118b-165">OIDC verrà illustrato in un esempio successivo.</span><span class="sxs-lookup"><span data-stu-id="8118b-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="8118b-166">Configurare l'ID client ricevuto dal portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="8118b-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="8118b-167">Configurare l'URI di reindirizzamento con quello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8118b-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="8118b-168">Configurare gli ambiti necessari per accedere all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="8118b-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="8118b-169">Il valore `User.Read` in `oidc_scopes` consente di leggere il profilo di base dell'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="8118b-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="8118b-170">Per altre informazioni su tutti gli ambiti disponibili, vedere [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes)(Ambiti di autorizzazione di Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="8118b-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="8118b-171">Se si necessita di spiegazioni sugli ambiti `openid` o `offline_access` in OpenID Connect, vedere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8118b-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="8118b-172">Configurare gli endpoint client modificando il file oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="8118b-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="8118b-173">Aprire il file `oidc_endpoints.xml` e apportare le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="8118b-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="8118b-174">Se si usa OAuth2 come protocollo, questi endpoint non devono mai essere modificati.</span><span class="sxs-lookup"><span data-stu-id="8118b-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="8118b-175">Gli endpoint per `userInfoEndpoint` e `revocationEndpoint` non sono attualmente supportati da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8118b-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="8118b-176">Se si lasciano questi valori con il valore example.com predefinito, verrà ricordato che non sono disponibili nell'esempio :-)</span><span class="sxs-lookup"><span data-stu-id="8118b-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="8118b-177">Configurare una chiamata API Graph</span><span class="sxs-lookup"><span data-stu-id="8118b-177">Configure a Graph API call</span></span>
* <span data-ttu-id="8118b-178">Aprire il file `HomeActivity.java` e apportare le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="8118b-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="8118b-179">In questo caso una semplice chiamata all'API Graph restituisce le informazioni.</span><span class="sxs-lookup"><span data-stu-id="8118b-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="8118b-180">Si tratta di tutte le modifiche da apportare.</span><span class="sxs-lookup"><span data-stu-id="8118b-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="8118b-181">Eseguire l'applicazione `oidlib-sample` e fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="8118b-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="8118b-182">Una volta eseguita l'autenticazione, premere il pulsante **Request Protected Resource** (Richiedi risorsa protetta) per testare la chiamata all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="8118b-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="8118b-183">Ottenere aggiornamenti della sicurezza per il prodotto</span><span class="sxs-lookup"><span data-stu-id="8118b-183">Get security updates for our product</span></span>
<span data-ttu-id="8118b-184">È consigliabile ricevere notifiche sui problemi di sicurezza. A tale scopo, visitare [Security TechCenter](https://technet.microsoft.com/security/dd252948) e sottoscrivere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8118b-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

