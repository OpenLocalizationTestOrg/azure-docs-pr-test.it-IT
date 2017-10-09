---
title: hello aaaUnderstand OpenID Connect del flusso di codice di autenticazione in Azure AD | Documenti Microsoft
description: In questo articolo viene descritto come accedere a toouse HTTP messaggi tooauthorize tooweb applicazioni e API web nel tenant di utilizzo di Azure Active Directory e OpenID Connect.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Autorizzare l'accesso tooweb applicazioni tramite OpenID Connect e Azure Active Directory
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) è un livello identità semplice basato su protocollo hello OAuth 2.0. OAuth 2.0 definisce tooobtain meccanismi e utilizzare **i token di accesso** tooaccess risorse protette, ma non definiscono le informazioni di identità tooprovide metodi standard. OpenID Connect implementa l'autenticazione come un toohello di estensione per il processo di autorizzazione OAuth 2.0. Fornisce informazioni sull'utente finale di hello sotto forma di hello di un `id_token` che verifica hello identità dell'utente hello e vengono fornite informazioni di base del profilo utente hello.

È consigliabile usare OpenID Connect se si compila un'applicazione Web ospitata su un server e accessibile da browser.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Flusso di autenticazione con OpenID Connect
Hello più elementare di flusso di accesso contiene hello alla procedura seguente: ognuno di essi è descritto in dettaglio di seguito.

![Flusso di autenticazione di OpenID Connect](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Documento di metadati OpenID Connect

OpenID Connect viene descritto un documento di metadati che contiene la maggior parte delle informazioni di hello necessarie per un'app tooperform Accedi. Questo include informazioni quali toouse URL hello e il percorso di hello delle chiavi di firma pubbliche del servizio hello. documento di metadati di OpenID Connect Hello è reperibile in:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
metadati Hello sono un semplice documento JavaScript Object Notation (JSON). Vedere hello seguente frammento di codice per un esempio. Hello contenuto del frammento di codice è descritte dettagliatamente in hello [OpenID Connect specifica](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Inviare una richiesta di accesso hello
Quando l'utente hello tooauthenticate necessarie all'applicazione web, è necessario indicare hello utente toohello `/authorize` endpoint. Questa richiesta è simile toohello prima frazione di hello [del flusso di codice di autorizzazione OAuth 2.0](active-directory-protocols-oauth-code.md), con alcune differenze importanti:

* richiesta di Hello deve includere l'ambito di hello `openid` in hello `scope` parametro.
* Hello `response_type` parametro deve includere `id_token`.
* richiesta di Hello deve includere hello `nonce` parametro.

Una richiesta di esempio si presenta quindi come segue:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parametro |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono identificatori di tenant, ad esempio, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` per i token indipendente dal tenant |
| client_id |Obbligatoria |Id applicazione assegnato tooyour app Hello quando è stato registrato con Azure AD. È possibile trovare questo nel portale di Azure hello. Fare clic su **Azure Active Directory**, fare clic su **registrazioni di App**, scegliere un'applicazione hello e individuare hello Id applicazione nella pagina applicazione hello. |
| response_type |Obbligatoria |Deve includere `id_token` per l'accesso a OpenID Connect.  Può anche includere altri parametri response_type, ad esempio `code`. |
| scope |Obbligatoria |Elenco di ambiti separati da spazi.  Per OpenID Connect, deve includere ambito hello `openid`, che converte l'autorizzazione "Accesso" toohello nell'interfaccia utente di consenso hello.  È anche possibile includere in questa richiesta altri ambiti per richiedere il consenso. |
| nonce |Obbligatoria |Un valore incluso nella richiesta di hello, generato da app hello, che è incluso in hello risultante `id_token` come attestazione.  app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore.  il valore di Hello è in genere una stringa casuale e univoco o il GUID che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| redirect_uri |consigliato |redirect_uri Hello dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app.  Deve corrispondere esattamente uno dei redirect_uris hello che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in url. |
| response_mode |consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello risultante authorization_code tooyour indietro app.  I valori supportati sono `form_post` per *POST modulo HTTP* o `fragment` per *frammento URL*.  Per le applicazioni web, è consigliabile utilizzare `response_mode=form_post` tooensure hello trasferimento più sicuro dell'applicazione tooyour token. |
| state |consigliato |Un valore incluso nella richiesta di hello restituito nella risposta token hello.  Può trattarsi di una stringa di qualsiasi contenuto.  Per [evitare gli attacchi di richiesta intersito falsa](http://tools.ietf.org/html/rfc6749#section-10.12), viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| prompt |Facoltativa |Indica il tipo di hello di interazione utente richiesta.  Attualmente, hello solo i valori validi sono 'login', 'none', 'di consenso e di.  `prompt=login`forza hello utente tooenter le proprie credenziali per tale richiesta, la negazione single sign-in.  `prompt=none`hello opposto: assicura che l'utente hello non è presentato con qualsiasi interattivo prompt alcun tipo.  Se la richiesta hello può essere completata automaticamente tramite single-sign-on, l'endpoint di hello restituisce un errore.  `prompt=consent`Attiva hello OAuth di dialogo di consenso dopo il segno di utente hello, che richiede autorizzazioni toohello app di hello utente toogrant. |
| login_hint |Facoltativa |Può essere utilizzato toopre riempimento hello nome utente/posta elettronica campo indirizzo hello-pagina di accesso per utente hello, se si conosce il nome utente anticipatamente.  Spesso le app di usare questo parametro durante la riautenticazione, con già estratto il nome utente hello da una precedente Accedi utilizzando hello `preferred_username` attestazione. |

A questo punto, utente hello è richiesto tooenter le credenziali e autenticazione hello completo.

### Risposta di esempio
Una risposta di esempio, dopo hello utente è autenticato, potrebbe essere simile al seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| . | Descrizione |
| --- | --- |
| id_token |Hello `id_token` app hello richiesto. È possibile utilizzare hello `id_token` tooverify hello identità dell'utente e iniziare una sessione utente hello. |
| state |Un valore incluso nella richiesta di hello che viene inoltre restituito in risposta token hello. Per [evitare gli attacchi di richiesta intersito falsa](http://tools.ietf.org/html/rfc6749#section-10.12), viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |

### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo da gestire in modo appropriato le app hello:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
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
| server_error |Hello rilevato un errore imprevisto. |Ripetere la richiesta hello. Questi errori possono dipendere da condizioni temporanee. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di errori temporanei tooa. |
| temporarily_unavailable |server Hello è temporaneamente richiesta hello toohandle troppo occupato. |Ripetere la richiesta hello. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di condizione temporanea tooa. |
| invalid_resource |risorsa di destinazione Hello è valido perché non esiste, Azure AD non riesce a trovarla o non sia configurato correttamente. |Indica la risorsa hello, se presente, non è stata configurata nel tenant di hello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |

## Convalidare hello id_token
Solo la ricezione di un `id_token` non è sufficiente tooauthenticate hello utente; è necessario convalidare hello firma e verifica delle richieste di hello in hello `id_token` per i requisiti dell'applicazione. endpoint di Azure AD Hello utilizza i token Web JSON (Jwt) e i token di crittografia a chiave pubblica toosign e verificare che siano validi.

È possibile scegliere hello toovalidate `id_token` nel codice client, ma una pratica comune è hello toosend `id_token` server back-end tooa ed eseguire la convalida di hello non esiste. Dopo aver verificato la firma hello di hello `id_token`, esistono alcuni attestazioni si è tooverify obbligatorio.

È inoltre possibile toovalidate attestazioni aggiuntive a seconda dello scenario. Alcune convalide comuni includono:

* Garantire hello utente o l'organizzazione ha effettuato l'iscrizione per app hello.
* Verifica utente hello dispone di autorizzazione diritti
* Garantire che sia stato applicato un determinato livello di autenticazione, ad esempio l'autenticazione a più fattori.

Dopo aver verificato hello `id_token`, è possibile avviare una sessione utente hello e usare le attestazioni di hello in hello `id_token` tooobtain informazioni utente hello nell'app. Queste informazioni possono essere usate per la visualizzazione, i record, le autorizzazioni e così via. Per altre informazioni sui tipi di token hello e attestazioni, vedere [supportati Token e tipi di attestazione](active-directory-token-and-claims.md).

## Inviare una richiesta di disconnessione
Quando si desidera utente hello toosign all'esterno dell'app hello, è insufficiente tooclear i cookie dell'applicazione o in caso contrario terminare la sessione di hello con utente hello.  È inoltre necessario reindirizzare hello utente toohello `end_session_endpoint` per disconnessione.  Se non si toodo così, utente hello sarà in grado di tooreauthenticate tooyour app senza dover immettere nuovamente le proprie credenziali perché avranno una single sign-on sessione valido con l'endpoint di Azure AD hello.

È possibile reindirizzare semplicemente hello utente toohello `end_session_endpoint` elencati nel documento di metadati di OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| . |  | Descrizione |
| --- | --- | --- |
| post_logout_redirect_uri |consigliato |URL Hello hello utente deve essere reindirizzato tooafter di disconnessione ha esito positivo.  Se viene omesso, l'utente hello viene visualizzato un messaggio generico. |

## Single Sign-Out
Quando si reindirizza hello utente toohello `end_session_endpoint`, Azure AD Cancella hello sessione utente da browser hello. Tuttavia, hello utente può comunque essere connesso tooother applicazioni che usano Azure AD per l'autenticazione. tooenable toosign tali applicazioni hello utente contemporaneamente, Azure AD invia un toohello di richiesta HTTP GET registrato `LogoutUrl` di tutte le applicazioni hello utente hello è attualmente connesso al. Applicazioni devono rispondere toothis richiesta deselezionando qualsiasi sessione che identifica l'utente hello e restituendo un `200` risposta.  Se si desidera toosupport l'accesso single sign out nell'applicazione, è necessario implementare ad un `LogoutUrl` nel codice dell'applicazione.  È possibile impostare hello `LogoutUrl` da hello portale di Azure:

1. Passare toohello [portale Azure](https://portal.azure.com).
2. Scegliere il servizio Active Directory facendo clic sul proprio account nel hello angolo superiore destro della pagina hello.
3. Dal Pannello di navigazione a sinistra di hello, scegliere **Azure Active Directory**, quindi scegliere **registrazioni di App** e selezionare l'applicazione.
4. Fare clic su **proprietà** e trovare hello **Logout URL** casella di testo. 

## Acquisizione dei token
Molte applicazioni web devono toonot solo accesso hello utente, ma anche accedere a un servizio web per conto di tale utente tramite OAuth. Questo scenario consente di combinare OpenID Connect per l'autenticazione utente durante l'acquisizione contemporaneamente un `authorization_code` che può essere utilizzato tooget `access_tokens` utilizzando hello flusso di codice di autorizzazione OAuth.

## Ottenere i token di accesso
i token di accesso tooacquire, è necessario toomodify hello richiesta di accesso precedente:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Inclusi gli ambiti di autorizzazione nella richiesta di hello e utilizzando `response_type=code+id_token`, hello `authorize` endpoint assicura che l'utente hello ha acconsentito autorizzazioni toohello indicate nella hello `scope` parametro di query e restituire un codice di autorizzazione di app tooexchange per un token di accesso.

### Risposta con esito positivo
Una risposta con esito positivo che usa `response_mode=form_post` ha un aspetto simile al seguente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametro | Descrizione |
| --- | --- |
| id_token |Hello `id_token` app hello richiesto. È possibile utilizzare hello `id_token` tooverify hello identità dell'utente e iniziare una sessione utente hello. |
| code |authorization_code Hello che hello app richiesto. app Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per la risorsa di destinazione hello. I codici di autorizzazione hanno una durata breve e in genere scadono dopo circa 10 minuti. |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |

### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo da gestire in modo appropriato le app hello:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

Per una descrizione di hello possibili codici di errore e la loro azione consigliata client, vedere [codici di errore per gli errori di endpoint di autorizzazione](#error-codes-for-authorization-endpoint-errors).

Una volta un'autorizzazione `code` e `id_token`, è possibile eseguire l'accesso utente hello e ottenere i token di accesso per loro conto.  toosign hello utente, è necessario convalidare hello `id_token` esattamente come descritto in precedenza. i token di accesso tooget, è possibile seguire i passaggi di hello descritti nella sezione "Utilizzare toorequest codice di autorizzazione hello un token di accesso" hello del nostro [documentazione relativa al protocollo OAuth](active-directory-protocols-oauth-code.md).
