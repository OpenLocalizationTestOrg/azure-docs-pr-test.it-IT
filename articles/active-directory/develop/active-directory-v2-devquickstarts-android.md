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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Aggiungere app per Android tooan Accedi con l'API Graph utilizzando hello v 2.0 endpoint di una libreria di terze parti
piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect. Gli sviluppatori possono utilizzare qualsiasi libreria desiderano toointegrate grazie ai servizi. gli sviluppatori di toohelp utilizzano la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come piattaforma delle identità Microsoft tooconnect toohello tooconfigure librerie di terze parti. La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) possono connettersi toohello piattaforma delle identità Microsoft.

Con un'applicazione hello creati in questa procedura dettagliata, gli utenti possano accedere tootheir organizzazione e quindi cercare autonomamente nella propria organizzazione tramite l'API Graph hello.

Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questa configurazione di esempio può non avere senso tooyou. Per approfondimenti, è consigliabile leggere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

> [!NOTE]
> Alcune funzionalità di piattaforma che dispone di un'espressione in hello OAuth2 o OpenID Connect standard, ad esempio l'accesso condizionale e gestione di criteri di Intune, richiedono si toouse l'open source di librerie di identità di Microsoft Azure.
> 
> 

endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità.

> [!NOTE]
> toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Scaricare codice hello da GitHub
codice Hello per questa esercitazione viene mantenuto [su GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow lungo, è possibile [scheletro hello dell'app come un file ZIP di download](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o scheletro hello clone:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

È possibile anche scaricare l'esempio di hello e iniziare subito:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Registrare un'app
Creare una nuova app hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguire hello i passaggi dettagliati in [come un'app con endpoint v 2.0 hello tooregister](active-directory-v2-app-registration.md).  Verificare di:

* Hello copia **Id applicazione** che è assegnato tooyour app perché è necessario prima.
* Aggiungere hello **Mobile** piattaforma per l'app.

> Nota: portale di registrazione applicazione hello fornisce un **URI di reindirizzamento** valore. Tuttavia, in questo esempio è necessario utilizzare il valore predefinito hello di `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Scaricare una libreria di terze parti NXOAuth2 hello e creare un'area di lavoro
Questa procedura dettagliata, si utilizzerà hello OIDCAndroidLib da GitHub, ovvero una raccolta di OAuth2 basata su hello codice OpenID Connect di Google. Implementa il profilo di applicazione nativa hello e supporta l'endpoint di autorizzazione hello dell'utente hello. Questi sono tutti aspetti di hello che dovrai toointegrate con la piattaforma di identità Microsoft hello.

Clonare computer tooyour di hello OIDCAndroidLib repository.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Configurare l'ambiente Android Studio
1. Creare un nuovo progetto Android Studio e accettare le impostazioni predefinite nella procedura guidata hello hello.
   
    ![Creare un nuovo progetto in Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Target Android devices (Dispositivi Android di destinazione)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Aggiungere un'attività toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset dei moduli del progetto, spostare hello clonato repository toohello percorso del progetto. È possibile anche creare progetto hello e clonare direttamente toohello percorso del progetto.
   
    ![Moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Aprire le impostazioni dei moduli di hello progetto utilizzando il menu di scelta rapida hello o tramite hello di scelta rapida Ctrl + Alt + Maj + S.
   
    ![Impostazioni dei moduli del progetto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Rimuovere il modulo di applicazione predefinito di hello perché si vuole solo le impostazioni dei contenitori progetto hello.
   
    ![modulo di applicazione Hello predefinito](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Importare i moduli dal progetto corrente toohello di hello repository clonato.
   
    ![Progetto di importazione gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crea una nuova pagina modulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Ripetere questi passaggi per hello `oidlib-sample` modulo.
7. Controllare le dipendenze oidclib hello hello `oidlib-sample` modulo.
   
    ![dipendenze oidclib modulo oidlib esempio hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Fare clic su **OK** e attendere la sincronizzazione di Gradle.
   
    Il file settings.gradle sarà simile al seguente:
   
    ![Schermata di settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Compilare hello toomake app di esempio che tale esempio hello correttamente in esecuzione.
   
    Si sarà in grado di toouse questo con Azure Active Directory ancora. È necessario tooconfigure alcuni endpoint prima. Si tratta di tooensure non è di un problemi di Android Studio, prima di iniziare la personalizzazione di app di esempio hello.
10. Compilare ed eseguire `oidlib-sample` come destinazione di hello in Android Studio.
    
    ![Progresso della compilazione oidlib di esempio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Eliminare hello `app ` directory in cui è stato lasciato quando modulo hello rimosso dal progetto hello perché Android Studio non viene eliminato per motivi di sicurezza.
    
    ![Struttura dei file che include directory dell'applicazione hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Aprire hello **modificare configurazioni** configurazione di hello eseguire tooremove menu che è stato lasciato anche quando il modulo hello è stata rimossa dal progetto hello.
    
    ![Menu Edit Configurations (Modifica configurazioni)](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Configurazione di esecuzione dell'app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Configurare gli endpoint hello dell'esempio hello
Dopo aver creato hello `oidlib-sample` eseguite correttamente, modifica alcuni tooget endpoint questo utilizzo di Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Configurare il client modificando il file di oidc_clientconf.xml hello
1. Poiché si utilizza OAuth2 flussi solo tooget un token e chiama l'API Graph hello, impostare hello client toodo OAuth2 solo. OIDC verrà illustrato in un esempio successivo.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Configurare l'ID client ricevuto dal portale di registrazione hello.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Configurare l'URI di reindirizzamento con hello uno sotto.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Configurare gli ambiti che è necessario in ordine tooaccess hello API Graph.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Hello `User.Read` valore `oidc_scopes` consente si tooread hello profilo di base hello effettuato l'accesso utente.
Maggiori informazioni su tutti gli ambiti disponibili hello in [gli ambiti di autorizzazione di Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Se si necessita di spiegazioni sugli ambiti `openid` o `offline_access` in OpenID Connect, vedere [Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Configurare gli endpoint client modificando il file di oidc_endpoints.xml hello
* Aprire hello `oidc_endpoints.xml` file e apportare hello seguenti modifiche:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Se si usa OAuth2 come protocollo, questi endpoint non devono mai essere modificati.

> [!NOTE]
> gli endpoint per Hello `userInfoEndpoint` e `revocationEndpoint` non sono attualmente supportate da Azure Active Directory. Se si lascia queste con il valore di example.com hello predefinito, verrà ricordato che non sono disponibili in: esempio hello :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Configurare una chiamata API Graph
* Aprire hello `HomeActivity.java` file e apportare hello seguenti modifiche:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

In questo caso una semplice chiamata all'API Graph restituisce le informazioni.

Queste sono tutte le modifiche di hello che è necessario toodo. Eseguire hello `oidlib-sample` applicazione e fare clic su **Accedi**.

Dopo aver completata l'autenticazione, selezionare hello **richiesta risorsa protetta** pulsante tootest il toohello chiamata API Graph.

## <a name="get-security-updates-for-our-product"></a>Ottenere aggiornamenti della sicurezza per il prodotto
Si consiglia di notifiche tooget sugli eventi di sicurezza, visitare hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) e la sottoscrizione di avvisi consultivo tooSecurity.

