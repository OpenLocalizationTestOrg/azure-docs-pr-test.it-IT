---
title: Accesso Web con OpenID Connect - Azure AD B2C | Microsoft Docs
description: Creazione di applicazioni web tramite l'implementazione di Azure Active Directory hello hello OpenID Connect del protocollo di autenticazione
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: accesso Web con OpenID Connect
OpenID Connect è un protocollo di autenticazione basato su OAuth 2.0, che possono essere utilizzati toosecurely effettua l'accesso utente nelle applicazioni tooweb. Tramite l'implementazione di hello Azure Active Directory B2C (Azure AD B2C) di OpenID Connect, è possibile assegnare l'iscrizione, accedi, altri gestione delle identità esperienze e nella tooAzure di applicazioni web Active Directory (Azure AD). Questa guida illustra come toodo così in modo indipendente dal linguaggio. Viene descritto come toosend e ricevere messaggi HTTP senza utilizzare uno dei nostri librerie open source.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) estende hello OAuth 2.0 *autorizzazione* protocollo per l'utilizzo come un *autenticazione* protocollo. In questo modo si tooperform single sign-on tramite OAuth. Introduce il concetto di hello di un *token ID*, ovvero un token di sicurezza che consente di hello client tooverify hello identità dell'utente hello e ottenere informazioni sul profilo di base sull'utente hello.

Dal momento che estende OAuth 2.0, consente inoltre di acquisire toosecurely app *i token di accesso*. È possibile utilizzare access_tokens tooaccess risorse che sono protetti da un [server autorizzazione](active-directory-b2c-reference-protocols.md#the-basics). Si consiglia OpenID Connect per la compilazione di un'applicazione Web ospitata su un server e accessibile da browser. Se si desidera tooadd identità tooyour portatili o desktop le applicazioni di gestione tramite Azure Active Directory B2C, è necessario utilizzare [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) anziché OpenID Connect.

Azure Active Directory B2C estende toodo hello standard OpenID Connect protocollo più semplice autenticazione e autorizzazione. Introduce hello [parametro policy](active-directory-b2c-reference-policies.md), che consente toouse OpenID Connect tooadd esperienze degli utenti, ad esempio effettua l'iscrizione, accesso e la gestione dei profili - tooyour app. In questo caso, verrà illustrato come tooimplement toouse OpenID Connect e criteri, ognuna di queste esperienze in applicazioni web. È inoltre mostreremo come tooget i token di accesso per l'accesso a web API.

le richieste HTTP di esempio di Hello nella sezione successiva hello utilizzano la directory di esempio B2C, fabrikamb2c.onmicrosoft.com, nonché l'applicazione di esempio, https://aadb2cplayground.azurewebsites.net e criteri. Si è gratuita tootry out hello richiede manualmente utilizzando i valori o sostituirli con valori personalizzati.
Informazioni su come troppo[Ottieni B2C tenant, applicazione e i criteri](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Invio di richieste di autenticazione
Quando l'app web deve utente hello tooauthenticate ed eseguito un criterio, è possibile indirizzare hello utente toohello `/authorize` endpoint. Si tratta di hello interattivo parte del flusso di hello, in cui utente hello accetta azione, a seconda dei criteri di hello.

In questa richiesta, il client di hello indica autorizzazioni hello talmente tooacquire tra utente hello in hello `scope` tooexecute di criteri di parametro e hello in hello `p` parametro. Vengono forniti esempi di tre in hello seguenti sezioni (con interruzioni di riga per migliorare la leggibilità), ognuno dei quali utilizza criteri diversi. tooget un'idea di come funziona ciascuna richiesta, provare a richiesta hello incollare in un browser e l'esecuzione.

#### <a name="use-a-sign-in-policy"></a>Uso di un criterio di accesso
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Uso di un criterio di iscrizione
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Uso di un criterio di modifica del profilo
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametro | Obbligatorio? | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |applicazione Hello ID tale hello [portale di Azure](https://portal.azure.com/) assegnato tooyour app. |
| response_type |Obbligatorio |tipo di risposta Hello, che deve includere un ID token di OpenID Connect. Se l'app Web necessita anche di token per chiamare un'API Web, è possibile usare `code+id_token`, come illustrato qui. |
| redirect_uri |Consigliato |Hello `redirect_uri` parametro dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app. Deve corrispondere esattamente a uno di hello `redirect_uri` parametri che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in URL. |
| scope |Obbligatorio |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambe le autorizzazioni che sono stati richiesti. Hello `openid` ambito indica che un toosign autorizzazione nei dati utente e ottenere hello, sull'utente hello sotto forma di hello di token ID (toocome più su questo più avanti in articolo hello). Hello `offline_access` ambito è facoltativo per le applicazioni web. Indica che l'app sarà necessario un *token di aggiornamento* per tooresources di accesso di lunga durata. |
| response_mode |Consigliato |metodo Hello che deve essere utilizzati toosend hello autorizzazione codice tooyour indietro app risultante. Può essere `query`, `form_post` o `fragment`.  Hello `form_post` modalità di risposta è consigliabile per motivi di sicurezza. |
| state |Consigliato |Un valore incluso nella richiesta di hello che viene inoltre restituito in risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. Per evitare gli attacchi di richiesta intersito falsa, viene in genere usato un valore univoco generato casualmente. stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio fossero nella pagina di hello. |
| nonce |Obbligatorio |Un valore incluso nella richiesta di hello (generato da app hello) che verrà incluso nel token ID risultante hello come attestazione. app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore. valore di Hello in genere è una stringa univoca casuale che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| p |Obbligatorio |criteri di Hello che verranno eseguito. È il nome di hello di un criterio che viene creato nel tenant di B2C. valore del nome criterio Hello deve iniziare con `b2c\_1\_`. Informazioni su criteri e hello [framework criteri estendibile](active-directory-b2c-reference-policies.md). |
| prompt |Facoltativo |tipo di Hello dell'interazione dell'utente che è obbligatorio. Hello unico valore valido in questo momento è `login`, che forza hello tooenter utente le credenziali per tale richiesta. L'accesso Single Sign-On non avrà effetto. |

A questo punto, hello verrà chiesto del flusso di lavoro del criterio di toocomplete hello. Questa operazione potrebbe comportare hello immissione di nome utente e password, accedere con un'identità di social networking, iscriversi a directory hello o qualsiasi altro numero di passaggi, a seconda di come sono definiti i criteri di hello.

Al termine di criteri di hello, utente hello Azure AD restituisce una app tooyour risposta in hello indicato `redirect_uri` parametro, utilizzando il metodo hello specificato in hello `response_mode` parametro. risposta Hello è hello stesso per ogni hello precedono i casi, indipendentemente dal criterio hello che viene eseguita.

Una risposta con esito positivo che utilizza `response_mode=fragment` ha un aspetto simile al seguente:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametro | Descrizione |
| --- | --- |
| id_token |Hello token ID hello app richiesto. È possibile utilizzare l'identità dell'utente di hello ID tooverify token hello e avviare una sessione utente hello. Ulteriori informazioni sul token ID e il relativo contenuto sono inclusi in hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). |
| code |Hello codice di autorizzazione che app hello richiesto, se è stato utilizzato `response_type=code+id_token`. app Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per una risorsa di destinazione. I codici di autorizzazione hanno una durata molto breve. In genere scadono dopo circa 10 minuti. |
| state |Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |

Le risposte di errore possono anche essere inviate toohello `redirect_uri` parametro in modo che app hello possibile gestirli nel modo appropriato:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e che può essere utilizzato tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |
| state |Vedere la descrizione completa di hello nella tabella prima di hello in questa sezione. Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |

## <a name="validate-hello-id-token"></a>Convalidare i token ID hello
Solo la ricezione di un ID token non è sufficiente tooauthenticate hello. È necessario convalidare la firma del token ID hello e verificare hello attestazioni nel token hello requisiti dell'applicazione. Usa Azure Active Directory B2C [i token Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e pubblica i token toosign di crittografia della chiave e verificare che siano validi.

Sono disponibili molte librerie open source per la convalida dei token JWT, a seconda del linguaggio preferito. È consigliabile prendere in esame tali opzioni anziché implementare una logica di convalida personalizzata. informazioni di Hello qui saranno utili per capire come tooproperly utilizzare tali raccolte.

Azure Active Directory B2C dispone di un endpoint dei metadati di OpenID Connect, che consente un'app toofetch informazioni Azure Active Directory B2C in fase di esecuzione. Queste informazioni includono endpoint, contenuti del token e chiavi per la firma dei token. Il tenant B2C include un documento di metadati JSON per ogni criterio. Ad esempio, hello documento di metadati per hello `b2c_1_sign_in` criteri in `fabrikamb2c.onmicrosoft.com` si trova in:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Una delle proprietà hello di questo documento di configurazione è `jwks_uri`, il cui valore per hello stesso criterio sarebbe:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine quali criteri è stato utilizzato per la firma di un ID token (e da dove toofetch hello metadati), sono disponibili due opzioni. In primo luogo, il nome di criterio hello è incluso in hello `acr` attestazione nel token ID hello. Per informazioni su come tooparse hello attestazioni da un ID token, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). L'altra opzione è criteri hello tooencode valore hello hello `state` parametro quando si invia la richiesta hello e decodificarlo in toodetermine quali criteri è stato utilizzato. Entrambi i metodi sono validi.

Dopo aver acquistato il documento di metadati hello dall'endpoint di metadati di OpenID Connect hello, è possibile utilizzare le chiavi pubbliche RSA 256 hello (che si trovano in questo endpoint) firma hello toovalidate di token ID hello. In un determinato punto nel tempo è possibile che siano presenti più chiavi elencate in questo endpoint, ognuna identificata da un'attestazione `kid`. Hello intestazione dei token ID hello contiene inoltre un `kid` attestazione, che indica quali di queste chiavi è stata toosign utilizzati token di ID hello. Per ulteriori informazioni, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md) (hello sezione su [convalida dei token](active-directory-b2c-reference-tokens.md#token-validation), in particolare).
<!--TODO: Improve hello information on this-->

Dopo aver convalidato firma hello del token ID hello, esistono diverse attestazioni che è necessario tooverify. Ad esempio:

* È necessario convalidare hello `nonce` tooprevent attacchi di riproduzione token di attestazione. Il valore deve essere specificato nella richiesta di accesso hello.
* È necessario convalidare hello `aud` attestazione tooensure che hello token ID è stato emesso per l'app. Il valore deve essere l'ID applicazione hello dell'app.
* È necessario convalidare hello `iat` e `exp` attestazioni tooensure che hello token ID non sia scaduto.

Esistono numerose altre convalide che è consigliabile eseguire. Questi elementi sono descritti in dettaglio in hello [OpenID Connect Core Spec](http://openid.net/specs/openid-connect-core-1_0.html).  È inoltre possibile toovalidate ulteriori attestazioni, a seconda dello scenario. Alcune convalide comuni includono:

* Assicurando che hello utente o l'organizzazione ha effettuato l'iscrizione per l'applicazione hello.
* Assicurandosi che l'utente hello abbia l'autorizzazione diritti.
* Verificare che sia stato applicato un determinato livello di autenticazione, ad esempio l'autenticazione a più fattori di Azure.

Per ulteriori informazioni sulle attestazioni hello in un ID token, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md).

Dopo avere convalidato token ID hello, è possibile iniziare una sessione utente hello. È possibile utilizzare le attestazioni hello hello ID token tooobtain informazioni utente hello nell'app. Gli usi di queste informazioni includono la visualizzazione, i record e l'autorizzazione.

## <a name="get-a-token"></a>Acquisizione di un token
Se è necessario il tooonly app web eseguire i criteri, è possibile ignorare hello prossime sezioni. Queste sezioni sono applicabili tooweb solo app che necessitano di toomake autenticato chiamate tooa web API e sono anche protetti da Azure Active Directory B2C.

È possibile riscattare il codice di autorizzazione hello acquisito (tramite `response_type=code+id_token`) per un token toohello desiderato risorsa inviando un `POST` richiesta toohello `/token` endpoint. Sono attualmente, hello solo risorse che è possibile richiedere un token per l'API web di back-end dell'app. convenzione di Hello per richiedere un token tooyourself è l'ID client dell'app come ambito hello toouse:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| . | Obbligatorio? | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |criteri che è stato utilizzato tooacquire hello autorizzazione Hello codice. Non è possibile usare un criterio diverso in questa richiesta. Si noti che si aggiunge questa stringa di query del parametro toohello, non toohello `POST` corpo. |
| client_id |Obbligatorio |applicazione Hello ID tale hello [portale di Azure](https://portal.azure.com/) assegnato tooyour app. |
| grant_type |Obbligatorio |tipo di concessione, che deve essere Hello `authorization_code` per flusso di codice di autorizzazione hello. |
| scope |Consigliato |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambe le autorizzazioni che sono stati richiesti. Hello `openid` ambito indica che un toosign autorizzazione nei dati utente e ottenere hello, sull'utente hello sotto forma di hello di id_token parametri. Può essere utilizzato tooget token tooyour dell'app web back-end API, rappresentato da hello stesso ID applicazione come client hello. Hello `offline_access` ambito indica che l'app sarà necessario un token di aggiornamento per tooresources di accesso di lunga durata. |
| code |Obbligatorio |codice di autorizzazione Hello acquisito nel segmento prima di hello del flusso di hello. |
| redirect_uri |Obbligatorio |Hello `redirect_uri` parametro di un'applicazione hello in cui viene visualizzato il codice di autorizzazione hello. |
| client_secret |Obbligatorio |segreto dell'applicazione Hello generato nel hello [portale di Azure](https://portal.azure.com/). La chiave privata dell'applicazione è un elemento di sicurezza importante. È necessario archiviarla in modo sicuro nel server. È necessario anche far ruotare periodicamente la chiave privata client. |

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
| token_type |valore di tipo di token Hello. Hello solo tipo di Azure AD supporta `Bearer`. |
| access_token |Hello firmato il token JWT richiesto. |
| scope |ambiti di Hello per cui hello token è valido. Possono essere usati per memorizzare i token nella cache per un uso successivo. |
| expires_in |durata Hello che hello token di accesso è valido (in secondi). |
| refresh_token |Token di aggiornamento di OAuth 2.0. app Hello è possibile usare questo token aggiuntivi tooacquire token alla scadenza del token corrente hello. Aggiornare i token sono di lunga durati e può essere utilizzato tooretain accesso tooresources per lunghi periodi di tempo. Per ulteriori informazioni, vedere toohello [riferimento token B2C](active-directory-b2c-reference-tokens.md). Si noti che è necessario aver utilizzato ambito hello `offline_access` autorizzazione hello sia token richieste in ordine tooreceive un token di aggiornamento. |

Le risposte di errore si presentano nel modo seguente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e che può essere utilizzato tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

## <a name="use-hello-token"></a>Usare il token di hello
Ora che è stato acquisito un token di accesso, è possibile utilizzare token hello in web back-end tramite tooyour richieste API includendola in hello `Authorization` intestazione:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Hello token di aggiornamento
I token ID hanno breve durata. È necessario aggiornarli dopo la scadenza toocontinue da tooaccess in grado di risorse. È possibile farlo tramite l'invio di un altro `POST` richiesta toohello `/token` endpoint. Questa volta, fornire hello `refresh_token` parametro anziché hello `code` parametro:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| . | Obbligatorio | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |Hello criteri token di aggiornamento utilizzato tooacquire hello originale. Non è possibile usare un criterio diverso in questa richiesta. Si noti che si aggiunge questa stringa di query del parametro toohello, non toohello corpo del POST. |
| client_id |Obbligatorio |applicazione Hello ID tale hello [portale di Azure](https://portal.azure.com/) assegnato tooyour app. |
| grant_type |Obbligatorio |tipo di Hello di concessione, che deve essere un token di aggiornamento per questo segmento del flusso di codice di autorizzazione hello. |
| scope |Consigliato |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambe le autorizzazioni che sono stati richiesti. Hello `openid` ambito indica che un toosign autorizzazione nei dati utente e ottenere hello, sull'utente hello sotto forma di hello di token ID. Può essere utilizzato tooget token tooyour dell'app web back-end API, rappresentato da hello stesso ID applicazione come client hello. Hello `offline_access` ambito indica che l'app sarà necessario un token di aggiornamento per tooresources di accesso di lunga durata. |
| redirect_uri |Consigliato |Hello `redirect_uri` parametro di un'applicazione hello in cui viene visualizzato il codice di autorizzazione hello. |
| refresh_token |Obbligatorio |Hello originale token di aggiornamento acquisito nel segmento di secondo hello del flusso di hello. Si noti che è necessario aver utilizzato ambito hello `offline_access` autorizzazione hello sia token richieste in ordine tooreceive un token di aggiornamento. |
| client_secret |Obbligatorio |segreto dell'applicazione Hello generato nel hello [portale di Azure](https://portal.azure.com/). La chiave privata dell'applicazione è un elemento di sicurezza importante. È necessario archiviarla in modo sicuro nel server. È necessario anche far ruotare periodicamente la chiave privata client. |

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
| token_type |valore di tipo di token Hello. Hello solo tipo di Azure AD supporta `Bearer`. |
| access_token |Hello firmato il token JWT richiesto. |
| scope |ambito Hello hello token è valido, che può essere usato per la memorizzazione nella cache i token per un uso successivo. |
| expires_in |durata Hello che hello token di accesso è valido (in secondi). |
| refresh_token |Token di aggiornamento di OAuth 2.0. app Hello è possibile usare questo token aggiuntivi tooacquire token alla scadenza del token corrente hello.  Aggiornare i token sono di lunga durati e può essere utilizzato tooretain accesso tooresources per lunghi periodi di tempo. Per ulteriori dettagli, consultare toohello [riferimento token B2C](active-directory-b2c-reference-tokens.md). |

Le risposte di errore si presentano nel modo seguente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e che può essere utilizzato tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

## <a name="send-a-sign-out-request"></a>Inviare una richiesta di disconnessione
Quando si desidera toosign hello utente all'esterno dell'app hello, è insufficiente tooclear i cookie dell'applicazione o in caso contrario terminare la sessione di hello con utente hello. È inoltre necessario reindirizzare hello utente tooAzure AD toosign out. Se non si toodo così, utente hello potrebbe essere in grado di tooreauthenticate tooyour app senza dover immettere nuovamente le proprie credenziali. in quanto avrà accesso a una sessione Single Sign-On valida con Azure AD.

È possibile reindirizzare semplicemente hello utente toohello `end_session` endpoint elencato nel documento di metadati di OpenID Connect hello descritto in precedenza in hello sezione "Convalida token ID hello":

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| . | Obbligatorio? | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |criteri di Hello che si desidera che toouse toosign hello utente dall'applicazione. |
| post_logout_redirect_uri |Consigliato |Hello URL utente hello deve essere reindirizzato tooafter riuscita disconnessione. Se non è incluso, Azure AD B2C utente hello viene visualizzato un messaggio generico. |

> [!NOTE]
> Sebbene l'indirizzamento hello utente toohello `end_session` endpoint verrà cancellato alcune hello stato dell'utente single sign-on con Azure Active Directory B2C, non convalida utente hello fuori la sessione di provider di Attestazioni di identità di social networking. Se utente hello seleziona hello IDP stesso durante un successivo Accedi, essi verranno riautenticare, senza immettere le proprie credenziali. Se un utente desideri toosign dall'applicazione B2C, non necessariamente significa che desiderano toosign fuori il proprio account Facebook. Tuttavia, nel caso di hello di account locali, hello sessione verrà terminata correttamente.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Uso del proprio tenant B2C
Se si desidera tootry queste richieste per conto proprio, è necessario innanzitutto eseguire tre passaggi seguenti e quindi sostituire i valori di esempio hello descritti in precedenza con il proprio:

1. [Creare un tenant B2C](active-directory-b2c-get-started.md)e usare il nome di hello del tenant in hello richieste.
2. [Creare un'applicazione](active-directory-b2c-app-registration.md) tooobtain un ID applicazione. Includere un'API Web/app Web nell'app. Se lo si desidera, creare un segreto dell'applicazione.
3. [Creare i criteri](active-directory-b2c-reference-policies.md) tooobtain i nomi dei criteri.

