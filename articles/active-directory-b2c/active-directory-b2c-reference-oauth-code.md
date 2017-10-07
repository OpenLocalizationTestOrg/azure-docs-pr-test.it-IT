---
title: Flusso del codice di autorizzazione - Azure AD B2C | Microsoft Docs
description: Informazioni su come toobuild App web utilizzando il protocollo di autenticazione di Azure Active Directory B2C e OpenID Connect.
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: flusso del codice di autorizzazione di OAuth 2.0
È possibile utilizzare concessione del codice di autorizzazione OAuth 2.0 hello in App installate in un dispositivo toogain accedere tooprotected alle risorse, ad esempio API web. Tramite l'implementazione di hello Azure Active Directory B2C (Azure AD B2C) di OAuth 2.0, è possibile aggiungere per l'abbonamento, accesso e le attività di altri gestione delle identità tooyour app di dispositivi mobili e desktop. Questo articolo è indipendente dal linguaggio. Nell'articolo hello, viene descritto come toosend e ricevere messaggi HTTP senza utilizzare le eventuali librerie open source.

<!-- TODO: Need link toolibraries -->

flusso di codice di autorizzazione OAuth 2.0 Hello è descritta in [sezione 4.1 della specifica OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749). È possibile usarlo per eseguire l'autenticazione e l'autorizzazione nella maggior parte dei tipi di app, tra cui le [App Web](active-directory-b2c-apps.md#web-apps) e le [app installate in modo nativo](active-directory-b2c-apps.md#mobile-and-native-apps). È possibile utilizzare hello acquisire toosecurely flusso codice di autorizzazione di OAuth 2.0 *i token di accesso* per le app, che può essere utilizzato tooaccess risorse che sono protetti da un [server autorizzazione](active-directory-b2c-reference-protocols.md#the-basics).

Questo articolo è incentrato su hello **client pubblica** flusso di codice di autorizzazione OAuth 2.0. Un client pubblico è qualsiasi applicazione client che non può essere attendibile toosecurely hello integrità di una password segreta. Ciò include l'App per dispositivi mobili, applicazioni desktop ed essenzialmente qualsiasi applicazione in esecuzione su un dispositivo e deve tooget i token di accesso. 

> [!NOTE]
> app web con Azure Active Directory B2C, utilizzare tooadd identity management tooa [OpenID Connect](active-directory-b2c-reference-oidc.md) anziché OAuth 2.0.

Azure Active Directory B2C estende standard hello che flusso OAuth 2.0 toodo più semplice autenticazione e autorizzazione. Introduce hello [parametro criteri](active-directory-b2c-reference-policies.md). Con i criteri predefiniti, è possibile usare OAuth 2.0 tooadd utente esperienze tooyour app, ad esempio effettua l'iscrizione, accesso e la gestione dei profili. In questo articolo verrà illustrato come tooimplement toouse OAuth 2.0 e i criteri, ognuna di queste esperienze nelle applicazioni native. Viene anche illustrata la modalità tooget i token di accesso per l'accesso a web API.

Nelle richieste HTTP di esempio di hello in questo articolo, utilizziamo la directory di Azure Active Directory B2C, **fabrikamb2c.onmicrosoft.com**. Si usano anche i criteri e l'applicazione di esempio. È possibile provare le richieste di hello utilizzando i valori o sostituirli con valori personalizzati.
Informazioni su come troppo[ottenere la propria directory, applicazione e i criteri di Azure Active Directory B2C](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Ottenere un codice di autorizzazione
flusso di codice di autorizzazione Hello inizia con il client di hello indirizzamento hello utente toohello `/authorize` endpoint. Questo è parte interattiva di hello del flusso di hello, in cui interviene utente hello. In questa richiesta, il client hello indica in hello `scope` autorizzazioni hello parametro che deve tooacquire utente hello. In hello `p` parametro indica tooexecute criteri hello. Hello tre esempi seguenti (con interruzioni di riga per migliorare la leggibilità) ogni usano criteri diversi.

### <a name="use-a-sign-in-policy"></a>Uso di un criterio di accesso
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Uso di un criterio di iscrizione
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Uso di un criterio di modifica del profilo
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parametro | Obbligatorio? | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |ID dell'applicazione Hello assegnato app tooyour in hello [portale di Azure](https://portal.azure.com). |
| response_type |Obbligatorio |tipo di risposta Hello, che deve includere `code` per flusso di codice di autorizzazione hello. |
| redirect_uri |Obbligatorio |Hello URI di reindirizzamento dell'app, in cui le risposte di autenticazione vengono inviate e ricevute dall'app. Deve corrispondere esattamente a uno di reindirizzamento hello URI a cui è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in URL. |
| scope |Obbligatorio |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure Active Directory (Azure AD) entrambi delle autorizzazioni di hello che sono stati richiesti. Utilizzando client hello ID come ambito hello indica che è necessario un token di accesso ai servizi o API web, è possibile utilizzare l'app è rappresentato dal hello stesso ID client.  Hello `offline_access` ambito indica che l'app è necessario un token di aggiornamento per tooresources di accesso di lunga durata. È inoltre possibile utilizzare hello `openid` toorequest ambito un ID di token da Azure Active Directory B2C. |
| response_mode |Consigliato |metodo Hello utilizzare toosend hello autorizzazione codice tooyour indietro app risultante. Può essere `query`, `form_post` o `fragment`. |
| state |Consigliato |Un valore incluso nella richiesta di hello restituito nella risposta token hello. Può essere una stringa di qualsiasi contenuto che si desidera toouse. In genere, viene utilizzato un valore univoco generato casualmente, attacchi di tooprevent cross-site request forgery. stato di Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello. Ad esempio, hello pagina hello utente nel o hello criteri che è stato in esecuzione. |
| p |Obbligatorio |criteri di Hello che viene eseguito. Hello nome di un criterio che viene creato nella directory di Azure Active Directory B2C. valore del nome criterio Hello deve iniziare con **b2c\_1\_**. toolearn informazioni sui criteri, vedere [criteri predefiniti di Azure Active Directory B2C](active-directory-b2c-reference-policies.md). |
| prompt |Facoltativo |tipo di Hello dell'interazione dell'utente che è obbligatorio. Attualmente, hello unico valore valido è `login`, che forza hello tooenter utente le credenziali per tale richiesta. L'accesso Single Sign-On non avrà effetto. |

A questo punto, hello verrà chiesto del flusso di lavoro del criterio di toocomplete hello. Questa operazione potrebbe comportare hello immissione di nome utente e password, accedere con un'identità di social networking, iscriversi a directory hello o qualsiasi altro numero di passaggi. Le azioni dell'utente dipendono come criterio di hello è definito.

Al termine di criteri di hello, utente hello Azure AD restituisce una app tooyour risposta al valore di hello utilizzato per `redirect_uri`. Usa metodo hello specificato in hello `response_mode` parametro. risposta Hello è esattamente hello stesso per ogni hello azione scenari utente, indipendentemente dal criterio hello che è stato eseguito.

Una risposta con esito positivo che usa `response_mode=query` ha un aspetto simile al seguente:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parametro | Descrizione |
| --- | --- |
| code |codice di autorizzazione Hello che hello app richiesto. app Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per una risorsa di destinazione. I codici di autorizzazione hanno una durata molto breve. In genere scadono dopo circa 10 minuti. |
| state |Vedere la descrizione completa di hello nella tabella hello nella precedente sezione hello. Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |

Le risposte di errore inoltre possono essere inviate toohello URI di reindirizzamento in modo che hello app in grado di gestirle in modo appropriato:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare i tipi di hello tooclassify di errori che si verificano. È inoltre possibile utilizzare hello stringa tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |
| state |Vedere la descrizione completa di hello in hello tabella precedente. Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |

## <a name="2-get-a-token"></a>2. Acquisizione di un token
Ora che è stato acquisito un codice di autorizzazione, è possibile riscattare hello `code` per un token toohello destinati risorsa inviando un toohello richiesta POST `/token` endpoint. In Azure Active Directory B2C, hello solo risorse che è possibile richiedere un token per sono l'API web di back-end dell'app. convenzione di Hello che viene utilizzato per richiedere un token tooyourself è l'ID client dell'app come ambito hello toouse:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| . | Obbligatorio? | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |criteri che è stato utilizzato tooacquire hello autorizzazione Hello codice. Non è possibile usare un criterio diverso in questa richiesta. Si noti che si aggiunge questo toohello parametro *stringa di query*, non nel corpo del POST hello. |
| client_id |Obbligatorio |ID dell'applicazione Hello assegnato app tooyour in hello [portale di Azure](https://portal.azure.com). |
| grant_type |Obbligatorio |tipo di Hello di concessione. Per flusso di codice di autorizzazione hello, deve essere il tipo di concessione di hello `authorization_code`. |
| scope |Consigliato |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambi delle autorizzazioni di hello che sono stati richiesti. Utilizzando client hello ID come ambito hello indica che è necessario un token di accesso ai servizi o API web, è possibile utilizzare l'app è rappresentato dal hello stesso ID client.  Hello `offline_access` ambito indica che l'app è necessario un token di aggiornamento per tooresources di accesso di lunga durata.  È inoltre possibile utilizzare hello `openid` toorequest ambito un ID di token da Azure Active Directory B2C. |
| code |Obbligatorio |codice di autorizzazione Hello acquisito nel segmento prima di hello del flusso di hello. |
| redirect_uri |Obbligatorio |Hello URI di reindirizzamento dell'applicazione hello in cui viene visualizzato il codice di autorizzazione hello. |

Una risposta di token con esito positivo ha un aspetto simile al seguente:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametro | Descrizione |
| --- | --- |
| not_before |ora di Hello al quale hello è considerato valido, in valore epoch token. |
| token_type |valore di tipo di token Hello. Hello solo il tipo che supporta Azure AD connessione. |
| access_token |Hello firmato JSON Web Token (JWT) richiesto. |
| scope |gli ambiti di Hello hello token è valido per. È inoltre possibile utilizzare i token toocache ambiti per un uso successivo. |
| expires_in |durata Hello che hello token è valido (in secondi). |
| refresh_token |Token di aggiornamento di OAuth 2.0. app Hello è possibile usare questo token aggiuntivi tooacquire token alla scadenza del token corrente hello. I token di aggiornamento sono di lunga durata. È possibile utilizzare tali tooretain accesso tooresources per lunghi periodi di tempo. Per ulteriori informazioni, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). |

Le risposte di errore si presentano nel modo seguente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare i tipi di hello tooclassify di errori che si verificano. È inoltre possibile utilizzare hello stringa tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |

## <a name="3-use-hello-token"></a>3. Usare il token di hello
Ora che è stato acquisito un token di accesso, è possibile utilizzare token hello in web back-end tramite tooyour richieste API includendola in hello `Authorization` intestazione:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Hello token di aggiornamento
I token di accesso e i token ID hanno breve durata. Dopo la scadenza, è necessario aggiornarli toocontinue tooaccess risorse. toodo, inviare un altro POST richiesta toohello `/token` endpoint. Questa volta, fornire hello `refresh_token` anziché hello `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| . | Obbligatorio? | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |Hello criteri token di aggiornamento utilizzato tooacquire hello originale. Non è possibile usare un criterio diverso in questa richiesta. Si noti che si aggiunge questo toohello parametro *stringa di query*, non nel corpo del POST hello. |
| client_id |Consigliato |ID dell'applicazione Hello assegnato app tooyour in hello [portale di Azure](https://portal.azure.com). |
| grant_type |Obbligatorio |tipo di Hello di concessione. Per questo segmento del flusso di codice di autorizzazione hello, deve essere il tipo di concessione di hello `refresh_token`. |
| scope |Consigliato |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambi delle autorizzazioni di hello che sono stati richiesti. Utilizzando client hello ID come ambito hello indica che è necessario un token di accesso ai servizi o API web, è possibile utilizzare l'app è rappresentato dal hello stesso ID client.  Hello `offline_access` ambito indica che l'app sarà necessario un token di aggiornamento per tooresources di accesso di lunga durata.  È inoltre possibile utilizzare hello `openid` toorequest ambito un ID di token da Azure Active Directory B2C. |
| redirect_uri |Facoltativo |Hello URI di reindirizzamento dell'applicazione hello in cui viene visualizzato il codice di autorizzazione hello. |
| refresh_token |Obbligatorio |Hello originale token di aggiornamento acquisito nel segmento di secondo hello del flusso di hello. |

Una risposta di token con esito positivo ha un aspetto simile al seguente:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametro | Descrizione |
| --- | --- |
| not_before |ora di Hello al quale hello è considerato valido, in valore epoch token. |
| token_type |valore di tipo di token Hello. Hello solo il tipo che supporta Azure AD connessione. |
| access_token |Hello firma JWT richiesto. |
| scope |gli ambiti di Hello hello token è valido per. È inoltre possibile utilizzare i token di hello ambiti toocache per un uso successivo. |
| expires_in |durata Hello che hello token è valido (in secondi). |
| refresh_token |Token di aggiornamento di OAuth 2.0. app Hello è possibile usare questo token aggiuntivi tooacquire token alla scadenza del token corrente hello. Aggiornare i token sono di lunga durati e possono essere utilizzati tooretain accesso tooresources per lunghi periodi di tempo. Per ulteriori informazioni, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). |

Le risposte di errore si presentano nel modo seguente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare tooclassify tipi di errori che si verificano. È inoltre possibile utilizzare hello stringa tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Usare la directory di Azure AD B2C
tootry queste richieste manualmente, hello completo seguendo i passaggi necessari. Sostituire i valori di esempio hello che è usata in questo articolo con valori personalizzati.

1. [Creare una directory Azure AD B2C](active-directory-b2c-get-started.md). Utilizzare il nome di hello di directory nelle richieste di hello.
2. [Creare un'applicazione](active-directory-b2c-app-registration.md) tooobtain un ID applicazione e un URI di reindirizzamento. Includere un client nativo nell'app.
3. [Creare i criteri](active-directory-b2c-reference-policies.md) tooobtain i nomi dei criteri.

