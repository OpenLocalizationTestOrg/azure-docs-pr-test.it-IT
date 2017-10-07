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
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: accedere mediante un'applicazione Android

piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect. Questo consente agli sviluppatori tooleverage qualsiasi libreria desiderano toointegrate grazie ai servizi. gli sviluppatori tooaid utilizzando la nostra piattaforma con altre librerie, abbiamo scritto alcune procedure dettagliate come questo uno toodemonstrate come tooconfigure 3rd party librerie tooconnect toohello Microsoft piattaforma delle identità. La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sarà piattaforma di Microsoft Identity toohello tooconnect in grado di.

> [!WARNING]
> Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse. In questo esempio utilizza una libreria di terze parti 3rd chiamata AppAuth che è stato testato per la compatibilità in scenari di base con hello Azure Active Directory B2C. Problemi e richieste di funzionalità devono essere progetto open source toohello diretto della libreria. Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).  
>
>

Se si è nuovo tooOAuth2 o OpenID Connect gran parte di questo esempio di configurazione potrebbe non prevedere tooyou molto senso. Si consiglia esaminare una breve [Panoramica del protocollo hello è stato documentato qui](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Ottenere una directory di Azure AD B2C

Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant. Una directory è un contenitore per utenti, app, gruppi e così via. Se non ne è già disponibile una, prima di continuare [creare una directory B2C](active-directory-b2c-get-started.md) .

## <a name="create-an-application"></a>Creare un'applicazione

Successivamente, è necessario toocreate un'app nel servizio directory B2C. Vengono riportate informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app. toocreate un'app per dispositivi mobili, seguire [queste istruzioni](active-directory-b2c-app-registration.md). Assicurarsi di:

* Includere un **Native Client** in un'applicazione hello.
* Hello copia **ID applicazione** ovvero tooyour assegnato app. che sarà necessario più avanti.
* Configurare un **URI di reindirizzamento** client nativo (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Sarà necessario più avanti.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri

In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questa app contiene un'esperienza di identità che combina accesso e iscrizione. È necessario toocreate questo criterio, come descritto nel [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando si crea il criterio di hello, assicurarsi di:

* Scegliere hello **nome visualizzato** come un attributo nei criteri di iscrizione.
* Scegliere hello **nome visualizzato** e **ID oggetto** applicazione le attestazioni in ogni criterio. È consentito scegliere anche altre attestazioni.
* Hello copia **nome** dei criteri dopo averlo creato. Devono contenere il prefisso hello `b2c_1_`.  È necessario il nome di criterio hello in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo aver creato i criteri, si è pronti toobuild l'app.

## <a name="download-hello-sample-code"></a>Scaricare il codice di esempio hello

È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). È possibile scaricare codice hello ed eseguirlo. È possibile iniziare rapidamente con la propria app utilizzando la configurazione di Azure Active Directory B2C seguendo le istruzioni hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

esempio Hello è una variante dell'esempio hello fornito da [AppAuth](https://openid.github.io/AppAuth-Android/). Visitare il loro toolearn pagina informazioni su AppAuth e delle relative funzionalità.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modifica toouse l'app Azure AD B2C con AppAuth

> [!NOTE]
> AppAuth supporta l'API 16 (Jellybean) di Android e versioni successive. Si consiglia di usare l'API 23 e versioni successive.
>

### <a name="configuration"></a>Configurazione

È possibile configurare la comunicazione con Azure Active Directory B2C mediante l'individuazione di hello specificando URI o specificando l'endpoint di autorizzazione hello sia URI degli endpoint token. In entrambi i casi, è necessario hello le seguenti informazioni:

* ID tenant (ad esempio contoso.onmicrosoft.com)
* Nome del criterio (ad esempio B2C\_1\_SignUpIn)

Se si sceglie tooautomatically individuare hello token e l'autorizzazione URI degli endpoint, è necessario toofetch informazioni dall'individuazione hello URI. individuazione di Hello URI può essere generato sostituendo hello Tenant\_ID e hello criteri\_nome in hello URL seguente:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

È quindi possibile acquisire autorizzazione hello e URI degli endpoint token e creare un oggetto AuthorizationServiceConfiguration eseguendo hello:

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

Anziché utilizzare l'autorizzazione di hello tooobtain individuazione e l'URI degli endpoint token, è inoltre possibile specificare tali in modo esplicito sostituendo hello Tenant\_ID e hello criteri\_nome hello dell'URL di seguito:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Hello esecuzione di codice seguente toocreate AuthorizationServiceConfiguration oggetto:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autorizzazione

Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione. hello toocreate richiesta, sarà necessario hello le seguenti informazioni:

* ID client (ad esempio 00000000-0000-0000-0000-000000000000)
* URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Consultare toohello [AppAuth Guida](https://openid.github.io/AppAuth-Android/) in modo toocomplete hello parte rimanente del processo di hello. Se è necessario tooquickly iniziare con un'app in funzione, estrarre [l'esempio](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Seguire i passaggi hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter la configurazione di Azure Active Directory B2C.

Ci sono sempre toofeedback aperti e i suggerimenti! Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello. Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

