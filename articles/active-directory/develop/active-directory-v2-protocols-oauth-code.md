---
title: Flusso di codice di autorizzazione OAuth 2.0 di aaaAzure AD | Documenti Microsoft
description: Creazione di applicazioni web tramite l'implementazione di Azure AD hello OAuth 2.0 del protocollo di autenticazione.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Protocolli della versione 2.0: flusso del codice di autorizzazione di OAuth 2.0
concessione del codice di autorizzazione OAuth 2.0 Hello è utilizzabile nelle App che vengono installate in un dispositivo toogain accedere tooprotected alle risorse, ad esempio API web.  Tramite l'implementazione della versione 2.0 di hello app modello OAuth 2.0, è possibile aggiungere l'API di accesso e le App per dispositivi mobili e desktop tooyour.  Questa guida è indipendente dal linguaggio e viene descritto come toosend e ricevere messaggi HTTP senza utilizzare uno dei nostri librerie open source.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

flusso di codice di autorizzazione OAuth 2.0 Hello è descritta nel [sezione 4.1 della specifica OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749).  È utilizzato tooperform autenticazione e autorizzazione nella maggior parte di hello di tipi di app, inclusi [le app web](active-directory-v2-flows.md#web-apps) e [App installate in modo nativo](active-directory-v2-flows.md#mobile-and-native-apps).  In questo modo le app toosecurely acquisire access_tokens che possono essere utilizzati tooaccess risorse protette utilizzando hello v 2.0 endpoint.  

## Diagramma di protocollo
In generale, flusso di autenticazione intera hello per un'applicazione nativa/mobile un bit è simile al seguente:

![Flusso del codice di autenticazione di OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Richiedere un codice di autorizzazione
flusso di codice di autorizzazione Hello inizia con il client di hello indirizzamento hello utente toohello `/authorize` endpoint.  In questa richiesta, il client di hello indica hello autorizzazioni tooacquire utente hello:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Fare clic sul collegamento di hello sotto tooexecute questa richiesta. Dopo aver effettuato l'accesso, il browser dovrebbe essere reindirizzato troppo`https://localhost/myapp/` con un `code` nella barra degli indirizzi hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parametro |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatoria |Id dell'applicazione il portale di registrazione hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assegnato l'app. |
| response_type |Obbligatoria |Deve includere `code` per flusso di codice di autorizzazione hello. |
| redirect_uri |consigliato |redirect_uri Hello dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app.  Deve corrispondere esattamente uno dei redirect_uris hello che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in url.  Per le app native e mobili, è necessario utilizzare il valore predefinito hello di `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| scope |Obbligatoria |Un elenco separato da spazi di [ambiti](active-directory-v2-scopes.md) che si desidera hello utente tooconsent per. |
| response_mode |consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello risultante token tooyour indietro app.  Può essere `query` o `form_post`. |
| state |consigliato |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello.  Può trattarsi di una stringa di qualsiasi contenuto.  Per [evitare gli attacchi di richiesta intersito falsa](http://tools.ietf.org/html/rfc6749#section-10.12), viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| prompt |Facoltativa |Indica il tipo di hello di interazione utente richiesta.  Hello solo i valori validi in questo momento sono 'account di accesso, 'none', 'di consenso e di.  `prompt=login`sarà il force hello tooenter utente le credenziali per tale richiesta, la negazione di single sign-in.  `prompt=none`è hello opposto: garantisce che l'utente hello non è presentato con qualsiasi tipo di prompt interattivo.  Se la richiesta hello può essere completata automaticamente tramite single-sign-on, l'endpoint v 2.0 hello restituirà un errore.  `prompt=consent`finestra di dialogo dopo il segno di utente hello, che richiede autorizzazioni toohello app di hello utente toogrant il consenso verrà hello trigger OAuth. |
| login_hint |Facoltativa |Può essere utilizzato toopre riempimento hello nome utente/posta elettronica campo indirizzo hello pagina di accesso per utente hello, se si conosce il nome utente anticipatamente.  Spesso le applicazioni utilizzano il parametro durante la riesecuzione dell'autenticazione, che già estratto hello username da una precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Facoltativa |Può essere uno di `consumers` o `organizations`.  Se incluso, non verrà eseguita il processo di individuazione basata su posta elettronica hello che l'utente passa attraverso nella pagina, hello v 2.0 accesso iniziali tooa leggermente più semplice l'esperienza utente.  Spesso le applicazioni utilizzano il parametro durante la riautenticazione, estraendo hello `tid` da una precedente Accedi.  Se hello `tid` attestazione valore `9188040d-6c67-4c5b-b112-36a304b66dad`, si consiglia di utilizzare `domain_hint=consumers`.  In caso contrario, usare `domain_hint=organizations`. |

A questo punto, si sarà utente hello frequenti tooenter le credenziali e autenticazione hello completo.  Hello v 2.0 endpoint assicura anche che l'utente hello ha acconsentito autorizzazioni toohello indicate nella hello `scope` parametro di query.  Se l'utente hello non ha accettato le condizioni tooany di tali autorizzazioni, viene chiesto hello utente tooconsent toohello necessarie autorizzazioni.  Questo articolo contiene informazioni dettagliate su [autorizzazioni, consenso e app multi-tenant](active-directory-v2-scopes.md).

Una volta utente hello autentica e concede il consenso, endpoint v 2.0 hello restituirà un'app tooyour risposta in hello indicato `redirect_uri`, utilizzando il metodo di hello specificato nel hello `response_mode` parametro.

#### Risposta con esito positivo
Una risposta con esito positivo che usa `response_mode=query` ha un aspetto simile al seguente:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parametro | Descrizione |
| --- | --- |
| code |authorization_code Hello che hello app richiesto. app Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per la risorsa di destinazione hello.  I codici di autorizzazione hanno una durata molto breve, in genere scadono dopo circa 10 minuti. |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |

#### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo da gestire in modo appropriato le app hello:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

#### Codici per gli errori dell'endpoint di autorizzazione
Hello nella tabella seguente vengono descritti hello vari codici di errore che possono essere restituiti in hello `error` parametro di risposta di errore hello.

| Codice di errore | Descrizione | Azione client |
| --- | --- | --- |
| invalid_request |Errore del protocollo, ad esempio un parametro obbligatorio mancante. |Correggere e inviare di nuovo la richiesta hello. Si tratta di un errore di sviluppo rilevato in genere durante il test iniziale. |
| unauthorized_client |Hello applicazione client non è consentito toorequest un codice di autorizzazione. |Ciò si verifica quando un'applicazione hello client non è registrata in Azure AD o non è stato aggiunto il tenant di Azure AD dell'utente toohello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |
| access_denied |Consenso negato dal proprietario della risorsa |un'applicazione Hello client può inviare una notifica utente hello che è possibile continuare a meno che non hello utente autorizza l'accesso. |
| unsupported_response_type |server di autorizzazione Hello non supporta il tipo di risposta hello nella richiesta di hello. |Correggere e inviare di nuovo la richiesta hello. Si tratta di un errore di sviluppo rilevato in genere durante il test iniziale. |
| server_error |Hello rilevato un errore imprevisto. |Ripetere la richiesta hello. Questi errori possono dipendere da condizioni temporanee. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di un errore temporaneo. |
| temporarily_unavailable |server Hello è temporaneamente richiesta hello toohandle troppo occupato. |Ripetere la richiesta hello. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di una condizione temporanea. |
| invalid_resource |risorsa di destinazione Hello è valido perché non esiste, Azure AD non riesce a trovarla o non sia configurato correttamente. |Indica la risorsa hello, se presente, non è stata configurata nel tenant di hello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |

## Richiedere un token di accesso
Ora che è stato acquisito un authorization_code e dispongono dell'autorizzazione utente hello, è possibile riscattare hello `code` per un `access_token` toohello desiderato di risorsa, inviando un `POST` richiesta toohello `/token` endpoint:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Provare a eseguire la richiesta in Postman. (Non dimenticare hello tooreplace `code`) [ ![eseguiti in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatoria |Id dell'applicazione il portale di registrazione hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assegnato l'app. |
| grant_type |Obbligatoria |Deve essere `authorization_code` per flusso di codice di autorizzazione hello. |
| scope |Obbligatoria |Elenco di ambiti separati da spazi.  gli ambiti di Hello richiesti in questa parte deve essere equivalente tooor un subset degli ambiti hello richiesto nel primo segmento di hello.  Se gli ambiti di hello specificati nella richiesta sono estese a più server di risorse, endpoint v 2.0 hello restituirà un token per la risorsa hello specificata nell'ambito del primo hello.  Per una spiegazione più dettagliata di ambiti, vedere troppo[ambiti, autorizzazione e autorizzazioni](active-directory-v2-scopes.md). |
| code |Obbligatoria |Hello authorization_code acquisito nel segmento prima di hello del flusso di hello. |
| redirect_uri |Obbligatoria |Hello stesso valore di redirect_uri che è stato utilizzato tooacquire hello authorization_code. |
| client_secret |Obbligatorio per app Web |segreto dell'applicazione Hello creato nel portale di registrazione hello app per l'app.  È consigliabile non usarlo in un'app nativa, perché i segreti client non possono essere archiviati in modo affidabile nei dispositivi.  È necessario per le applicazioni web e web API, che sono in modo sicuro hello possibilità toostore hello client_secret sul lato server hello. |

#### Risposta con esito positivo
Una risposta token con esito positivo ha un aspetto simile al seguente:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametro | Descrizione |
| --- | --- |
| access_token |token di accesso richiesto Hello. app Hello è possibile utilizzare questo toohello tooauthenticate token risorsa, ad esempio un'API web protetta. |
| token_type |Indica il valore di tipo di token hello. solo il tipo che supporta Azure AD Hello è connessione |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| scope |gli ambiti di Hello hello access_token è valido per. |
| refresh_token |Token di aggiornamento di OAuth 2.0. Hello app può usare questo token acquisire token di accesso aggiuntivi dopo la scadenza del token di accesso corrente hello.  Refresh_tokens sono di lunga durata e possono essere utilizzati tooretain accesso tooresources per lunghi periodi di tempo.  Per ulteriori dettagli, consultare toohello [riferimento token v 2.0](active-directory-v2-tokens.md). |
| id_token |Token JWT (Token Web JSON) non firmato. Hello app può base64Url decodificare segmenti hello di questo token toorequest informazioni utente hello che ha effettuato l'accesso. app Hello può memorizzare nella cache i valori hello e visualizzarli, ma deve fare affidamento su di essi per qualsiasi autorizzazione o i limiti di sicurezza.  Per ulteriori informazioni su id_tokens vedere hello [riferimento dell'endpoint token v 2.0](active-directory-v2-tokens.md). |

#### Risposta di errore
Le risposte di errore hanno un aspetto simile al seguente:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |
| error_codes |Elenco dei codici di errore specifici del servizio token di sicurezza utile per la diagnostica. |
| timestamp |ora di Hello in corrispondenza del quale si è verificato l'errore hello. |
| trace_id |Identificatore univoco per la richiesta di hello che consentono di diagnostica. |
| correlation_id |Identificatore univoco per la richiesta di hello che consentono di diagnostica tra componenti. |

#### Codici per gli errori degli endpoint di token
| Codice di errore | Descrizione | Azione client |
| --- | --- | --- |
| invalid_request |Errore del protocollo, ad esempio un parametro obbligatorio mancante. |Correggere e inviare di nuovo la richiesta hello |
| invalid_grant |codice di autorizzazione Hello scaduto o non è valido. |Provare un nuovo toohello richiesta `/authorize` endpoint |
| unauthorized_client |Hello client autenticato non è autorizzato toouse tipo di concedere tale autorizzazione. |Ciò si verifica quando un'applicazione hello client non è registrata in Azure AD o non è stato aggiunto il tenant di Azure AD dell'utente toohello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |
| invalid_client |Autenticazione client non riuscita. |le credenziali di Hello del client non sono valide. toofix, l'amministratore dell'applicazione hello Aggiorna credenziali hello. |
| unsupported_grant_type |Hello autorizzazione server non supporta il tipo di hello autorizzazione grant. |Hello modifica concedere tipo nella richiesta di hello. Questo tipo di errore dovrebbe verificarsi solo durante lo sviluppo ed essere rilevato durante il test iniziale. |
| invalid_resource |risorsa di destinazione Hello è valido perché non esiste, Azure AD non riesce a trovarla o non sia configurato correttamente. |Indica la risorsa hello, se presente, non è stata configurata nel tenant di hello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |
| interaction_required |richiesta di Hello richiede l'intervento dell'utente. Ad esempio, è necessario un passaggio di autenticazione aggiuntivo. |Ripetere la richiesta hello con hello stessa risorsa. |
| temporarily_unavailable |server Hello è temporaneamente richiesta hello toohandle troppo occupato. |Ripetere la richiesta hello. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di una condizione temporanea. |

## Usare il token di accesso hello
Ora che è stato acquistato un `access_token`, è possibile utilizzare token hello in tooWeb richieste API includendola in hello `Authorization` intestazione:

> [!TIP]
> Eseguire la richiesta in Postman. (Sostituire hello `Authorization` intestazione prima) [ ![eseguiti in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Aggiornare il token di accesso di hello
Access_tokens hanno una durata breve e, è necessario aggiornarli dopo la scadenza toocontinue l'accesso alle risorse.  È possibile farlo tramite l'invio di un altro `POST` richiesta toohello `/token` endpoint, fornendo hello questa volta `refresh_token` anziché hello `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Provare a eseguire la richiesta in Postman. (Non dimenticare hello tooreplace `refresh_token`) [ ![eseguiti in Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatoria |Id dell'applicazione il portale di registrazione hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assegnato l'app. |
| grant_type |Obbligatoria |Deve essere `refresh_token` per questo segmento del flusso di codice di autorizzazione hello. |
| scope |Obbligatoria |Elenco di ambiti separati da spazi.  gli ambiti di Hello richiesti in questa parte deve essere equivalente tooor un subset degli ambiti hello richiesto nella parte di hello originale authorization_code richiesta.  Se gli ambiti di hello specificati nella richiesta sono estese a più server di risorse, endpoint v 2.0 hello restituirà un token per la risorsa hello specificata nell'ambito del primo hello.  Per una spiegazione più dettagliata di ambiti, vedere troppo[ambiti, autorizzazione e autorizzazioni](active-directory-v2-scopes.md). |
| refresh_token |Obbligatoria |Hello refresh_token acquisito nel segmento di secondo hello del flusso di hello. |
| redirect_uri |Obbligatoria |Hello stesso valore di redirect_uri che è stato utilizzato tooacquire hello authorization_code. |
| client_secret |Obbligatorio per app Web |segreto dell'applicazione Hello creato nel portale di registrazione hello app per l'app.  È consigliabile non usarlo in un'app nativa, perché i segreti client non possono essere archiviati in modo affidabile nei dispositivi.  È necessario per le applicazioni web e web API, che sono in modo sicuro hello possibilità toostore hello client_secret sul lato server hello. |

#### Risposta con esito positivo
Una risposta token con esito positivo ha un aspetto simile al seguente:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametro | Descrizione |
| --- | --- |
| access_token |token di accesso richiesto Hello. app Hello è possibile utilizzare questo toohello tooauthenticate token risorsa, ad esempio un'API web protetta. |
| token_type |Indica il valore di tipo di token hello. solo il tipo che supporta Azure AD Hello è connessione |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| scope |gli ambiti di Hello hello access_token è valido per. |
| refresh_token |Nuovo token di aggiornamento di OAuth 2.0. È necessario sostituire l'aggiornamento precedente hello token con questa tooensure token di aggiornamento appena acquisiti i token di aggiornamento rimangono validi per più a lungo possibile. |
| id_token |Token JWT (Token Web JSON) non firmato. Hello app può base64Url decodificare segmenti hello di questo token toorequest informazioni utente hello che ha effettuato l'accesso. app Hello può memorizzare nella cache i valori hello e visualizzarli, ma deve fare affidamento su di essi per qualsiasi autorizzazione o i limiti di sicurezza.  Per ulteriori informazioni su id_tokens vedere hello [riferimento dell'endpoint token v 2.0](active-directory-v2-tokens.md). |

#### Risposta di errore
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |
| error_codes |Elenco dei codici di errore specifici del servizio token di sicurezza utile per la diagnostica. |
| timestamp |ora di Hello in corrispondenza del quale si è verificato l'errore hello. |
| trace_id |Identificatore univoco per la richiesta di hello che consentono di diagnostica. |
| correlation_id |Identificatore univoco per la richiesta di hello che consentono di diagnostica tra componenti. |

Per una descrizione dei codici di errore hello e hello client azioni consigliate, vedere [codici di errore per gli errori di endpoint token](#error-codes-for-token-endpoint-errors).

