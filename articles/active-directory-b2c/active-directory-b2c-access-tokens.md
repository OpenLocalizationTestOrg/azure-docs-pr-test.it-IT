---
title: 'Azure Active Directory B2C: richiesta di token di accesso | Microsoft Docs'
description: In questo articolo viene illustrato come un'applicazione client toosetup e acquisire un token di accesso.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: richiesta di token di accesso

Un token di accesso (indicato come **accesso\_token** nelle risposte hello da Azure AD B2C) è un tipo di token di sicurezza che un client può utilizzare risorse tooaccess che sono protetti da un [server autorizzazione](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), ad esempio un'API web. I token di accesso sono rappresentati come [Jwt](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) e contengono informazioni su server di risorse previsto hello e hello autorizzazioni concesse toohello. Quando si chiama il server di risorse hello, token di accesso hello deve essere presente nella richiesta HTTP hello.

Questo articolo illustra come tooconfigure un'applicazione client e l'API web in ordine di tooobtain un **accesso\_token**.

> [!NOTE]
> **Le catene di API Web (On-Behalf-Of) non sono supportate da Azure Active Directory B2C.**
>
> Molte architetture includono un'API che deve toocall web a un'altra API web downstream, sia protetta da Azure Active Directory B2C. Questo scenario è comune in native client che dispongono di un'API web back-end, che a sua volta chiama un servizio online Microsoft, ad esempio hello API Azure AD Graph.
>
> Questo scenario di API web concatenate può essere supportato utilizzando noto come flusso di On-Behalf-Of hello hello concessione delle credenziali di connessione JWT di OAuth 2.0, in caso contrario. Tuttavia, hello On-Behalf-Of flusso non è attualmente implementata in Azure Active Directory B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Registrare un'API Web e pubblicare le autorizzazioni

Prima di richiedere un token di accesso, innanzitutto necessario tooregister un'API web e autorizzazioni (ambiti) che è possibile concedere l'applicazione client toohello di pubblicazione.

### <a name="register-a-web-api"></a>Registrare un'API Web

1. Nel Pannello di hello B2C funzionalità nel portale di Azure hello, fare clic su **applicazioni**.
1. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
1. Immettere un **nome** per un'applicazione hello che descriverà tooconsumers l'applicazione. Ad esempio, è possibile immettere "API Contoso".
1. Hello attiva/disattiva **Include app web o web API** passare troppo**Sì**.
1. Immettere un valore arbitrario per hello **gli URL di risposta**. Ad esempio, immettere `https://localhost:44316/`. il valore di Hello non è importante perché un'API deve non ricevere token hello direttamente da Azure Active Directory B2C.
1. Immettere un **URI ID app**. Questo è l'identificatore hello utilizzato per l'API web. Ad esempio, immettere "note" nella casella hello. Hello **URI ID App** sarà `https://{tenantName}.onmicrosoft.com/notes`.
1. Fare clic su **crea** tooregister l'applicazione.
1. Fare clic su un'applicazione hello appena creato e la copia hello univoco globale **ID Client applicazione** che verrà utilizzato successivamente nel codice.

### <a name="publishing-permissions"></a>Pubblicazione delle autorizzazioni

Gli ambiti, che sono analoghi toopermissions, sono necessari quando l'applicazione chiama un'API. Alcuni esempi di ambiti sono "read" e "write". Si supponga che si vuole dal web o app nativa troppo "Leggi" da un'API. Chiama l'app Azure AD B2C e richiesta di token di accesso che fornisce accesso toohello ambito "lettura". Per Azure Active Directory B2C tooemit un token di accesso, applicazione hello deve toobe concesse autorizzazioni troppo "lettura" dall'API specifica hello. toodo, toopublish hello "Leggi" ambito innanzitutto richiesto dall'API.

1. All'interno di Azure Active Directory B2C hello **applicazioni** pannello hello Apri applicazione dell'API web ("API Contoso").
1. Fare clic su **Ambiti pubblicati**. In questo campo definire le autorizzazioni di hello (ambiti) che possono essere concessa tooother applicazioni.
1. Configurare i campi **Valore ambito** nel modo necessario, ad esempio "read". Per impostazione predefinita, verrà definito ambito "user_impersonation" hello. che può essere ignorato se lo si desidera. Immettere una descrizione dell'ambito hello in hello **nome ambito** colonna.
1. Fare clic su **Salva**.

> [!IMPORTANT]
> Hello **nome ambito** descrizione hello di hello **valore di ambito**. Quando si utilizzano ambito hello, accertarsi che hello toouse **valore di ambito**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Concedere nativo o API web tooa le autorizzazioni di app web

Una volta configurato toopublish ambiti è un'API, un'applicazione client hello deve toobe concesso gli ambiti tramite hello portale di Azure.

1. Passare toohello **applicazioni** menu nel pannello funzionalità hello B2C.
1. Registrare un'applicazione client ([applicazione web](active-directory-b2c-app-registration.md#register-a-web-app) o [client nativo](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) se non è già disponibile. Se si segue questa guida come punto di partenza, occorre tooregister un'applicazione client.
1. Fare clic su **Accesso all'API**.
1. Fare clic su **Aggiungi**.
1. Selezionare i web API hello ambiti e si desidera toogrant (autorizzazioni).
1. Fare clic su **OK**.

> [!NOTE]
> Azure AD B2C non richiede il consenso agli utenti dell'applicazione client. Al contrario, tutti consenso viene fornito da salve, in base alle autorizzazioni hello configurate tra applicazioni hello descritte in precedenza. Se è stata revocata una concessione di autorizzazioni per un'applicazione, tutti gli utenti che sono stati tooacquire in precedenza in grado di tale autorizzazione non sarà più possibile così in grado di toodo.

## <a name="requesting-a-token"></a>Richiesta di un token

Quando viene richiesto un token di accesso, un'applicazione hello client deve ottenere le autorizzazioni di hello desiderato toospecify in hello **ambito** parametro della richiesta di hello. Ad esempio, toospecify hello **valore di ambito** hello API con hello "Leggi" **URI ID App** di `https://contoso.onmicrosoft.com/notes`, ambito hello sarebbe `https://contoso.onmicrosoft.com/notes/read`. Di seguito è riportato un esempio di un toohello di richiesta di autorizzazione codice `/authorize` endpoint.

> [!NOTE]
> Attualmente i domini personalizzati non sono supportati insieme ai token di accesso. È necessario utilizzare il dominio tenantName.onmicrosoft.com nell'URL di richiesta hello.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire più autorizzazioni in hello stessa richiesta, è possibile aggiungere più voci in hello singolo **ambito** parametro, separato da spazi. ad esempio:

URL decodificato:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

URL codificato:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

È possibile richiedere più ambiti (autorizzazioni) per una risorsa rispetto a quelli concessi per l'applicazione client. Quando ciò accade hello, chiamata di hello avrà esito positivo se è stata concessa almeno un'autorizzazione. Hello risultante **accesso\_token** avrà relativo attestazione "scp" popolata con solo le autorizzazioni di hello che sono stati concessi.

> [!NOTE] 
> Richiesta di autorizzazioni sulle risorse di due diversi web non è supportata in hello stessa richiesta. Questo tipo di richiesta avrà esito negativo.

### <a name="special-cases"></a>Casi speciali

Hello OpenID Connect standard consente di specificare diversi valori speciali "scope". Hello seguente speciali ambiti rappresentano hello autorizzazione troppo "accedere al profilo dell'utente hello":

* **openid**: richiede un token ID
* **offline\_access**: richiede un token di aggiornamento (mediante [flussi del codice di autenticazione](active-directory-b2c-reference-oauth-code.md)).

Se hello `response_type` parametro in un `/authorize` richiesta include `token`, hello `scope` parametro deve includere almeno un ambito (diverso da `openid` e `offline_access`) che verrà concesso. In caso contrario, hello `/authorize` richiesta verrà terminata con un errore.

## <a name="hello-returned-token"></a>Hello ha restituito un token

In un creato correttamente **accesso\_token** (da entrambi hello `/authorize` o `/token` endpoint), esempio hello attestazioni saranno presenti:

| Nome | Attestazione | Descrizione |
| --- | --- | --- |
|Audience |`aud` |Hello **ID applicazione** della singola risorsa hello token hello concede l'accesso a. |
|Scope |`scp` |Hello autorizzazioni toohello risorse. Le autorizzazioni multiple concesse saranno separate da spazi. |
|Entità autorizzati |`azp` |Hello **ID applicazione** di un'applicazione hello client che ha avviato la richiesta hello. |

Quando l'API riceve hello **accesso\_token**, è necessario [convalidare token hello](active-directory-b2c-reference-tokens.md) tooprove che hello token sia autentico e ha attestazioni corretto hello.

Ci sono sempre toofeedback aperti e i suggerimenti! Se hai difficoltà a questo argomento, post su Stack Overflow utilizzando tag hello ['azure-Active Directory b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Passaggi successivi

* Compilare un'API Web con [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Compilare un'API Web con [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
