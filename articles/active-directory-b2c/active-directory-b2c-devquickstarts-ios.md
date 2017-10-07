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
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: accedere mediante un'applicazione iOS

piattaforma delle identità Microsoft Hello utilizza standard aperti quali OAuth2 e OpenID Connect. Utilizzando un protocollo standard aperto offre più opzioni agli sviluppatori quando si seleziona un toointegrate libreria con i servizi offerti. È stato fornito in questa procedura dettagliata e altri simili agli sviluppatori tooaid con la scrittura di applicazioni che si connettono toohello piattaforma di Microsoft Identity. La maggior parte delle librerie che implementano [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) della piattaforma in grado di tooconnect toohello Microsoft Identity.

> [!WARNING]
> Microsoft non fornisce correzioni per queste librerie di terze parti e non ha eseguito una verifica su esse. In questo esempio utilizza una libreria di terze parti chiamata AppAuth che è stato testato per la compatibilità in scenari di base con hello Azure Active Directory B2C. Problemi e richieste di funzionalità devono essere progetto open source toohello diretto della libreria. Per altre informazioni, vedere [questo articolo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Se si è nuovo tooOAuth2 o OpenID Connect, gran parte di questo esempio di configurazione potrebbe non prevedere tooyou molto senso. Si consiglia esaminare una breve [Panoramica del protocollo hello è stato documentato qui](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Ottenere una directory di Azure AD B2C
Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant. Una directory è un contenitore per utenti, app, gruppi e altro ancora. Se non ne è già disponibile una, [creare una directory B2C](active-directory-b2c-get-started.md) prima di continuare.

## <a name="create-an-application"></a>Creare un'applicazione
Successivamente, è necessario toocreate un'app nel servizio directory B2C. registrazione app Hello fornisce informazioni di Azure AD che deve toocommunicate in modo sicuro con l'app. toocreate un'app per dispositivi mobili, seguire [queste istruzioni](active-directory-b2c-app-registration.md). Assicurarsi di:

* Includere un **Native client** in un'applicazione hello.
* Hello copia **ID applicazione** ovvero tooyour assegnato app. Questo GUID sarà necessario in seguito.
* Configurare un **URI di reindirizzamento** con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Questo URI sarà necessario in seguito.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Creare i criteri
In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici. Questa app contiene un'esperienza di identità che combina accesso e iscrizione. Creare i criteri come descritto nell'[articolo relativo ai criteri](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando si crea il criterio di hello, assicurarsi di:

* In **attributi iscrizione**selezionare attributo hello **nome visualizzato**.  È possibile selezionare anche altri attributi.
* In **attestazioni applicazione**, selezionare le attestazioni hello **nome visualizzato** e **ID oggetto dell'utente**. Sono disponibili anche altre attestazioni.
* Hello copia **nome** dei criteri dopo averlo creato. Il nome dei criteri è preceduto da `b2c_1_` quando si salva il criterio di hello.  È necessario il nome di criterio hello in un secondo momento.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Dopo aver creato i criteri, si è pronti toobuild l'app.

## <a name="download-hello-sample-code"></a>Scaricare il codice di esempio hello
È fornito un esempio funzionante che usa AppAuth con Azure Active Directory B2C [in GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). È possibile scaricare codice hello ed eseguirlo. toouse tenant proprio AD B2C Azure, seguire le istruzioni hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

In questo esempio è stato creato seguendo le istruzioni Leggimi hello da hello [iOS AppAuth progetto in GitHub](https://github.com/openid/AppAuth-iOS). Per ulteriori informazioni sul funzionamento: esempio hello e libreria hello, fare riferimento a hello README AppAuth su GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modifica toouse l'app Azure AD B2C con AppAuth

> [!NOTE]
> AppAuth supporta iOS 7 e versioni successive.  Tuttavia, è necessario toosupport social gli account di accesso Google, SFSafariViewController che richiede di iOS 9 o versione successiva.
>

### <a name="configuration"></a>Configurazione

È possibile configurare la comunicazione con Azure Active Directory B2C specificando l'endpoint di autorizzazione hello sia URI degli endpoint token.  toogenerate gli URI, è necessario hello le seguenti informazioni:
* ID tenant (ad esempio contoso.onmicrosoft.com)
* Nome del criterio (ad esempio B2C\_1\_SignUpIn)

endpoint token URI può essere generato sostituendo Hello hello Tenant\_ID e hello criteri\_nome in hello URL seguente:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

endpoint di autorizzazione URI può essere generato sostituendo Hello hello Tenant\_ID e hello criteri\_nome in hello URL seguente:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Hello esecuzione di codice seguente toocreate AuthorizationServiceConfiguration oggetto:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autorizzazione

Dopo la configurazione o il recupero di una configurazione del servizio di autorizzazione, è possibile costruire una richiesta di autorizzazione. hello toocreate richiesta, è necessario hello le seguenti informazioni:  
* ID client (ad esempio 00000000-0000-0000-0000-000000000000)
* URI di reindirizzamento con schema personalizzato (ad esempio com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Entrambi gli elementi sono stati salvati durante la [registrazione dell'app](#create-an-application).

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

tooset backup la sezione relativa al toohello dei reindirizzamento di hello di applicazione toohandle con lo schema personalizzato hello URI, non è presente ' Schemes'URL' elenco hello tooupdate le Info. plist:
* Aprire Info.pList.
* Passare il mouse su una riga come 'Codice di tipo del sistema operativo di Bundle' e fare clic su hello \+ simbolo.
* Rinominare hello nuova riga 'URL types'.
* Fare clic a sinistra di hello freccia toohello della struttura ad albero di 'Tipi URL' tooopen hello.
* Fare clic a sinistra di hello freccia toohello dell'albero di hello tooopen 'Elemento 0'.
* Rinominare un elemento prima di sotto degli schemi di elemento too'URL 0.
* Fare clic a sinistra di hello freccia toohello dell'albero di hello tooopen ' Schemes'URL.
* Nella colonna 'Value' hello è un campo vuoto toohello sinistro 'Elemento 0' di sotto di ' Schemes'URL.  Impostare lo schema univoco dell'applicazione di hello valore tooyour.  il valore di Hello deve corrispondere schema hello utilizzato in redirectURL durante la creazione di oggetti OIDAuthorizationRequest hello.  Nel nostro esempio, abbiamo utilizzato lo schema hello 'com.onmicrosoft.fabrikamb2c.exampleapp'.

Fare riferimento toohello [AppAuth Guida](https://openid.github.io/AppAuth-iOS/) in modo toocomplete hello parte rimanente del processo di hello. Se è necessario tooquickly iniziare con un'app in funzione, estrarre [l'esempio](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Seguire i passaggi hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter la configurazione di Azure Active Directory B2C.

Ci sono sempre toofeedback aperti e i suggerimenti! Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello. Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
