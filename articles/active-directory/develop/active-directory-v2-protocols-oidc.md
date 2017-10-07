---
title: Active Directory v 2.0 e hello protocollo aaaAzure | Documenti Microsoft
description: Applicazioni web tramite l'implementazione di hello Azure AD versione 2.0 del protocollo di autenticazione OpenID Connect hello.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v 2.0 e hello protocollo
OpenID Connect è un protocollo di autenticazione basato su OAuth 2.0 che è possibile utilizzare toosecurely sign in un'applicazione web di tooa utente. Quando si utilizza l'implementazione dell'endpoint di hello v 2.0 di OpenID Connect, è possibile aggiungere Accedi e API accesso tooyour basata sul web app. In questo articolo verrà illustrato come toodo questo indipendente dalla lingua. Viene descritto come toosend e ricevere messaggi HTTP senza utilizzare tutte le librerie open source di Microsoft.

> [!NOTE]
> endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità. toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) estende hello OAuth 2.0 *autorizzazione* toouse protocollo come un *autenticazione* del protocollo, in modo che è possibile eseguire single sign-on tramite OAuth. OpenID Connect è stato introdotto il concetto di hello di un *token ID*, ovvero un token di sicurezza che consente ai client di hello identità hello tooverify dell'utente hello. token ID Hello ottiene anche le informazioni di profilo di base sull'utente hello. Poiché OpenID Connect ne estende OAuth 2.0, le applicazioni è possono acquisire in modo sicuro *i token di accesso*, che può essere utilizzato tooaccess risorse che sono protetti da un [server autorizzazione](active-directory-v2-protocols.md#the-basics). È consigliabile usare OpenID Connect per la compilazione di un'[applicazione Web](active-directory-v2-flows.md#web-apps) ospitata su un server e accessibile tramite browser.

## Diagramma di protocollo: accesso
Hello flusso di accesso più semplice prevede i passaggi di hello illustrati nel diagramma successivo hello. Questo articolo descrive dettagliatamente i singoli passaggi.

![Protocollo OpenID Connect: accesso](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Recuperare i documenti di metadati di OpenID Connect di hello
OpenID Connect viene descritto un documento di metadati che contiene la maggior parte delle informazioni di hello necessarie per un'app tooperform Accedi. Questo include informazioni quali toouse URL hello e il percorso di hello delle chiavi di firma pubbliche del servizio hello. Per l'endpoint di hello v 2.0, questo è hello OpenID Connect del documento di metadati che è necessario utilizzare:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Hello `{tenant}` può assumere uno dei quattro valori:

| Valore | Descrizione |
| --- | --- |
| `common` |Applicazione toohello possono accedere gli utenti con un account Microsoft personale e un account aziendale o dell'istituto di istruzione da Azure Active Directory (Azure AD). |
| `organizations` |Solo gli utenti con lavoro o scuola account da Azure AD possono accedere toohello applicazione. |
| `consumers` |Applicazione toohello possono accedere solo gli utenti con un account Microsoft personale. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` oppure `contoso.onmicrosoft.com` |Solo gli utenti con un account aziendale o dell'istituto di istruzione di un annuncio di Azure specifico tenant può accedere toohello applicazione. Il nome descrittivo di dominio hello di hello tenant di Azure AD o identificatore GUID del tenant hello può essere utilizzato. |

metadati Hello sono un semplice documento JavaScript Object Notation (JSON). Vedere hello seguente frammento di codice per un esempio. Hello contenuto del frammento di codice è descritte dettagliatamente in hello [OpenID Connect specifica](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

In genere, si usa il documento di metadati tooconfigure una libreria di OpenID Connect o SDK; libreria Hello utilizzerebbe hello metadati toodo il proprio lavoro. Tuttavia, se non si utilizza una libreria di OpenID Connect di pre-compilazione, è possibile seguire passaggi hello nel resto di hello di questo articolo tooperform sign-in un'app web tramite hello v 2.0 endpoint.

## Inviare una richiesta di accesso hello
Quando l'app web deve utente hello tooauthenticate, è possibile indirizzare hello utente toohello `/authorize` endpoint. Questa richiesta è simile toohello prima frazione di hello [flusso di codice di autorizzazione OAuth 2.0](active-directory-v2-protocols-oauth-code.md), con questi importanti differenze:

* richiesta di Hello deve includere hello `openid` ambito hello `scope` parametro.
* Hello `response_type` parametro deve includere `id_token`.
* richiesta di Hello deve includere hello `nonce` parametro.

ad esempio:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Fare clic su hello seguente collegamento tooexecute questa richiesta. Dopo l'accesso, il browser verrà reindirizzato toohttps://localhost/myapp/, con un ID token nella barra degli indirizzi hello. Si noti che questa richiesta usa `response_mode=query` (solo a scopo dimostrativo). È consigliabile usare `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parametro | Condizione | Descrizione |
| --- | --- | --- |
| tenant |Obbligatorio |È possibile utilizzare hello `{tenant}` valore nel percorso di hello di hello richiesta toocontrol chi può accedere toohello applicazione. Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant. Per altre informazioni, vedere le [nozioni di base sui protocolli](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatorio |l'ID applicazione Hello che hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assegnato tooyour app. |
| response_type |Obbligatorio |Deve includere `id_token` per l'accesso a OpenID Connect. Può anche includere altri valori `response_types`, ad esempio `code`. |
| redirect_uri |Consigliato |Hello URI di reindirizzamento dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app. Deve corrispondere esattamente uno di reindirizzamento hello URI è stato registrato nel portale di hello, ad eccezione del fatto che l'URL deve essere codificato. |
| scope |Obbligatorio |Elenco di ambiti separati da spazi. Per OpenID Connect, deve includere ambito hello `openid`, che converte l'autorizzazione "Accesso" toohello nell'interfaccia utente di consenso hello. È anche possibile includere in questa richiesta altri ambiti per richiedere il consenso. |
| nonce |Obbligatorio |Un valore incluso nella richiesta di hello, generato da app hello, che verrà incluso nel valore id_token risultante hello come attestazione. app Hello è possibile verificare che gli attacchi di riproduzione token di toomitigate questo valore. il valore di Hello in genere è una stringa casuale, univoca che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| response_mode |Consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello autorizzazione codice tooyour indietro app risultante. Può essere uno di `query`, `form_post` o `fragment`. Per le applicazioni web, è consigliabile utilizzare `response_mode=form_post`, tooensure hello trasferimento più sicuro dell'applicazione tooyour token. |
| state |Consigliato |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. Un valore univoco generato in modo casuale in genere viene utilizzato troppo[impedire attacchi di cross-site request forgery](http://tools.ietf.org/html/rfc6749#section-10.12). stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, come utente di hello hello pagina o la vista è stato in. |
| prompt |Facoltativo |Indica il tipo di hello di interazione utente richiesta. Hello solo i valori validi in questo momento sono `login`, `none`, e `consent`. Hello `prompt=login` attestazione forza hello tooenter utente le credenziali per tale richiesta, tra cui Nega accesso single sign-on. Hello `prompt=none` attestazione è hello opposto. Questa attestazione assicura che l'utente hello non è presentato con qualsiasi tipo di prompt interattivo. Se la richiesta hello può essere completata automaticamente tramite accesso single sign-on, l'endpoint v 2.0 hello restituisce un errore. Hello `prompt=consent` attestazione trigger hello di dialogo di consenso OAuth dopo l'accesso dell'utente hello. finestra di dialogo Hello chiede hello utente toogrant autorizzazioni toohello app. |
| login_hint |Facoltativo |È possibile utilizzare questo parametro toopre riempimento hello nome utente e la posta elettronica campo indirizzo di hello nella pagina di accesso per utente hello, se si conosce il nome utente hello anticipatamente. Spesso, App di usano questo parametro durante la riautenticazione, dopo aver già estratto hello username da un precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Facoltativo |Questo valore può essere `consumers` o `organizations`. Se incluso, ignora il processo di individuazione basata su posta elettronica hello utente hello va a buon hello v 2.0-pagina di accesso, per un'esperienza utente leggermente più semplice. Spesso, App di usano questo parametro durante la riautenticazione estraendo hello `tid` attestazione da token ID hello. Se hello `tid` attestazione valore `9188040d-6c67-4c5b-b112-36a304b66dad`, utilizzare `domain_hint=consumers`. In caso contrario, usare `domain_hint=organizations`. |

A questo punto, l'utente hello è tooenter richieste le credenziali e autenticazione hello completo. Hello v 2.0 endpoint verifica che l'utente hello ha acconsentito autorizzazioni toohello indicate nella hello `scope` parametro di query. Se l'utente hello non ha accettato le condizioni tooany di tali autorizzazioni, endpoint v 2.0 hello richiede le autorizzazioni di hello utente tooconsent toohello richiesto. Sono disponibili altre informazioni su [autorizzazioni, consenso e app multi-tenant](active-directory-v2-scopes.md).

Dopo che l'utente hello autentica e concede il consenso, hello v 2.0 endpoint restituisce un'app tooyour risposta in hello indicata URI di reindirizzamento utilizzando il metodo hello specificato in hello `response_mode` parametro.

### Risposta con esito positivo
La risposta con esito positivo quando si usa `response_mode=form_post` è simile alla seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parametro | Descrizione |
| --- | --- |
| id_token |Hello token ID hello app richiesto. È possibile utilizzare hello `id_token` tooverify parametro hello identità dell'utente e iniziare una sessione utente hello. Per ulteriori informazioni sui token ID e il relativo contenuto, vedere hello [v 2.0 endpoint token riferimento](active-directory-v2-tokens.md). |
| state |Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |

### Risposta di errore
Le risposte di errore potrebbero essere inviate anche URI di reindirizzamento toohello in modo che hello app in grado di gestirle. La risposta di errore è simile alla seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare per i tipi di errori che si verificano e tooreact tooerrors tooclassify. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |

### Codici per gli errori dell'endpoint di autorizzazione
Hello nella tabella seguente vengono descritti i codici di errore che possono essere restituiti in hello `error` parametro di risposta di errore hello:

| Codice di errore | Descrizione | Azione client |
| --- | --- | --- |
| invalid_request |Errore del protocollo, ad esempio un parametro obbligatorio mancante. |Correggere e inviare di nuovo la richiesta hello. Si tratta di un errore di sviluppo rilevato in genere durante il test iniziale. |
| unauthorized_client |un'applicazione Hello client non è possibile richiedere un codice di autorizzazione. |Ciò si verifica quando un'applicazione hello client non è registrata in Azure AD o non è stato aggiunto il tenant di Azure AD dell'utente toohello. un'applicazione Hello può richiedere hello utente con un'applicazione hello tooinstall istruzioni e aggiungerlo tooAzure AD. |
| access_denied |proprietario della risorsa Hello ha negato il consenso. |un'applicazione Hello client può inviare una notifica utente hello che è possibile continuare a meno che non hello utente autorizza l'accesso. |
| unsupported_response_type |server di autorizzazione Hello non supporta il tipo di risposta hello nella richiesta di hello. |Correggere e inviare di nuovo la richiesta hello. Si tratta di un errore di sviluppo rilevato in genere durante il test iniziale. |
| server_error |Hello rilevato un errore imprevisto. |Ripetere la richiesta hello. Questi errori possono dipendere da condizioni temporanee. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di errori temporanei tooa. |
| temporarily_unavailable |server Hello è temporaneamente richiesta hello toohandle troppo occupato. |Ripetere la richiesta hello. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di condizione temporanea tooa. |
| invalid_resource |risorsa di destinazione Hello è valido perché non esiste, Azure AD non riesce a trovarla o non sia configurato correttamente. |Ciò indica che la risorsa hello, se presente, non è stata configurata nel tenant di hello. un'applicazione Hello può richiedere utente hello con istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |

## Convalidare i token ID hello
Ricezione di un ID token non è sufficiente tooauthenticate hello. È inoltre necessario convalidare la firma del token ID hello e verificare hello attestazioni nel token hello requisiti dell'applicazione. Hello v 2.0 endpoint utilizza [i token Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e pubblica i token toosign di crittografia della chiave e verificare che siano validi.

È possibile scegliere un token di ID hello toovalidate nel codice client, ma una pratica comune è il server back-end token tooa di toosend hello ID ed eseguire la convalida di hello non esiste. Dopo aver convalidato firma hello del token ID hello, sarà necessario tooverify alcuni attestazioni. Per ulteriori informazioni, incluse informazioni su [convalida dei token](active-directory-v2-tokens.md#validating-tokens) e [informazioni importanti sul rollover della chiave di firma](active-directory-v2-tokens.md#validating-tokens), vedere hello [v 2.0 token riferimento](active-directory-v2-tokens.md). Si consiglia di usare una libreria tooparse e convalidare i token. È disponibile almeno una libreria per la maggior parte dei linguaggi e delle piattaforme.
<!--TODO: Improve hello information on this-->

È anche possibile toovalidate ulteriori attestazioni, a seconda dello scenario. Alcune convalide comuni includono:

* Verificare che hello utente o l'organizzazione ha effettuato l'iscrizione per l'applicazione hello.
* Verificare che l'utente hello necessaria autorizzazione o privilegi.
* Verificare che sia stato applicato un determinato livello di autenticazione, ad esempio l'autenticazione a più fattori.

Per ulteriori informazioni sulle attestazioni hello in un ID token, vedere hello [v 2.0 endpoint token riferimento](active-directory-v2-tokens.md).

Dopo avere convalidato completamente token ID hello, è possibile iniziare una sessione utente hello. Usare le attestazioni di hello hello ID token tooget informazioni utente hello nell'app. Queste informazioni possono essere usate per la visualizzazione, i record, le autorizzazioni e così via.

## Inviare una richiesta di disconnessione
Quando si desidera toosign utente hello dall'app, non è sufficiente tooclear i cookie dell'applicazione oppure in caso contrario terminare la sessione dell'utente hello. È inoltre necessario reindirizzare hello utente toohello v 2.0 endpoint toosign out. Se non si esegue questa operazione, utente hello autentica nuovamente tooyour app senza dover immettere nuovamente le proprie credenziali perché avranno una valida singola sessione di accesso con l'endpoint di hello v 2.0.

È possibile reindirizzare hello utente toohello `end_session_endpoint` elencati nel documento di metadati di OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| . | Condizione | Descrizione |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Consigliato | URL Hello hello utente viene reindirizzato tooafter correttamente la disconnessione. Se il parametro hello non è incluso, utente hello viene visualizzato un messaggio generico che viene generato dall'endpoint di hello v 2.0. L'URL deve corrispondere a uno di reindirizzamento hello che URI registrati per l'applicazione nel portale di registrazione applicazione hello.  |

## Single Sign-Out
Quando si reindirizza hello utente toohello `end_session_endpoint`, endpoint v 2.0 hello Cancella hello sessione utente da browser hello. Tuttavia, hello utente può comunque essere connesso tooother applicazioni che utilizzano gli account di Microsoft per l'autenticazione. tooenable tali utente hello toosign applicazioni contemporaneamente, endpoint di hello v 2.0 invia un toohello di richiesta HTTP GET registrato `LogoutUrl` di tutte le applicazioni hello utente hello è attualmente connesso al. Applicazioni devono rispondere toothis richiesta deselezionando qualsiasi sessione che identifica l'utente hello e restituendo un `200` risposta.  Se si desidera toosupport l'accesso single sign out nell'applicazione, è necessario implementare ad un `LogoutUrl` nel codice dell'applicazione.  È possibile impostare hello `LogoutUrl` dal portale di registrazione applicazione hello.

## Diagramma di protocollo: acquisizione dei token
Molte applicazioni web necessitano toonot solo accesso hello utente, ma anche un servizio web per conto di utente hello tooaccess tramite OAuth. Questo scenario combina OpenID Connect per l'autenticazione utente durante il recupero contemporaneamente un'autorizzazione i token del codice che è possibile utilizzare accesso tooget se si utilizza un flusso di codice di autorizzazione OAuth hello.

Hello completo OpenID Connect Accedi e flusso di acquisizione del token ha un aspetto simile toohello nel diagramma seguente. Viene descritto ogni passaggio in modo dettagliato in hello nelle sezioni seguenti di articolo hello.

![Protocollo OpenID Connect: acquisizione dei token](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Ottenere i token di accesso
tooacquire i token di accesso, modificare una richiesta di accesso hello:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Fare clic su hello seguente collegamento tooexecute questa richiesta. Dopo l'accesso, il browser viene reindirizzato toohttps://localhost/myapp/, con un token ID e codice nella barra degli indirizzi hello. Si noti che questa richiesta usa `response_mode=query` (solo a scopo dimostrativo). È consigliabile usare `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

Includendo gli ambiti di autorizzazione nella richiesta di hello e usando `response_type=id_token code`, endpoint v 2.0 hello assicura che l'utente hello ha acconsentito autorizzazioni toohello indicate nella hello `scope` parametro di query. Restituisce un tooexchange di app tooyour codice autorizzazione per un token di accesso.

### Risposta con esito positivo
La risposta con esito positivo quando si usa `response_mode=form_post` è simile alla seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametro | Descrizione |
| --- | --- |
| id_token |Hello token ID hello app richiesto. È possibile utilizzare l'identità dell'utente di hello ID tooverify token hello e avviare una sessione utente hello. Sono disponibili ulteriori informazioni sui token ID e il relativo contenuto in hello [v 2.0 endpoint token riferimento](active-directory-v2-tokens.md). |
| code |codice di autorizzazione Hello che hello app richiesto. app Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per la risorsa di destinazione hello. La durata del codice di autorizzazione è molto breve. In genere, un codice di autorizzazione scade dopo circa 10 minuti. |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |

### Risposta di errore
Le risposte di errore potrebbero essere inviate anche URI di reindirizzamento toohello in modo che hello app in grado di gestirle in modo appropriato. La risposta di errore è simile alla seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare per i tipi di errori che si verificano e tooreact tooerrors tooclassify. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |

Per una descrizione dei possibili codici di errore e delle risposte client consigliate, vedere [Codici per gli errori dell'endpoint di autorizzazione](#error-codes-for-authorization-endpoint-errors).

Quando si dispone di un codice di autorizzazione e un ID token, è possibile eseguire l'accesso utente hello e ottenere i token di accesso per loro conto. toosign hello utente, è necessario convalidare i token di ID hello [esattamente come descritto](#validate-the-id-token). i token di accesso tooget, seguire i passaggi di hello descritti nel nostro [documentazione relativa al protocollo OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
