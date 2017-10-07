---
title: 'Azure Active Directory B2C: app a singola pagina tramite flusso implicito | Microsoft Docs'
description: Informazioni su come le applicazioni a pagina singola toobuild direttamente tramite OAuth 2.0 impliciti flusso con Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure Active Directory B2C: app a singola pagina tramite il flusso implicito OAuth 2.0

> [!NOTE]
> Questa funzionalità è in anteprima.
> 

Molte app moderne hanno un front-end dell'app a singola pagina scritto principalmente in JavaScript. Spesso, hello app viene scritta tramite un framework come AngularJS, Ember.js o Durandal. Le app a pagina singola e le altre app JavaScript che vengono eseguite soprattutto in un browser presentano alcune problematiche aggiuntive per l'autenticazione:

* caratteristiche di sicurezza Hello di queste App sono sostanzialmente diverse dalle applicazioni web basate su server tradizionale.
* Molti server di autorizzazione e provider di identità non supportano le richieste CORS (Condivisione risorse tra le origini).
* Reindirizzamenti di pagina intera browser dall'app hello possono essere notevolmente invasivo toohello esperienza dell'utente.

toosupport queste applicazioni, Azure Active Directory B2C (Azure AD B2C) Usa flusso implicito hello OAuth 2.0. flusso di concessione implicita OAuth 2.0 Hello autorizzazione è descritto in [sezione 4.2 di specifica OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749). Nel flusso implicito, app hello ricevuto token direttamente da hello Azure Active Directory (Azure AD) autorizza un endpoint, senza alcun exchange server-server. Tutti la logica di autenticazione e accetta di gestione delle sessioni inserire interamente nel client JavaScript hello, senza i reindirizzamenti di pagina aggiuntiva.

Azure Active Directory B2C estende hello standard OAuth 2.0 impliciti flusso toomore rispetto alla semplice autenticazione e autorizzazione. Azure Active Directory B2C introduce hello [parametro criteri](active-directory-b2c-reference-policies.md). Con parametro hello criteri, è possibile usare OAuth 2.0 tooadd utente esperienze tooyour app, ad esempio effettua l'iscrizione, accesso e la gestione dei profili. In questo articolo viene illustrata la modalità toouse hello flusso implicito e Azure AD tooimplement ciascuna di queste esperienze nelle applicazioni a pagina singola. toohelp informazioni per iniziare, esaminiamo il nostro [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) e [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) esempi.

Nelle richieste HTTP di esempio di hello in questo articolo, utilizziamo la directory di Azure Active Directory B2C, **fabrikamb2c.onmicrosoft.com**. Si usano anche i criteri e l'applicazione di esempio. È possibile provare le richieste di hello utilizzando i valori o sostituirli con valori personalizzati.
Informazioni su come troppo[ottenere la propria directory, applicazione e i criteri di Azure Active Directory B2C](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Diagramma di protocollo

Hello implicita flusso di accesso è simile al seguente illustrazione hello. Ogni passaggio è descritto in dettaglio più avanti nell'articolo di hello.

![Corsie di OpenID Connect](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Invio di richieste di autenticazione
Quando l'app web deve utente hello tooauthenticate ed eseguito un criterio, indirizza hello utente toohello `/authorize` endpoint. Si tratta di hello interattivo parte del flusso di hello, in cui utente hello accetta azione, a seconda dei criteri di hello. utente Hello Ottiene un ID token hello endpoint di Azure AD.

In questa richiesta, il client hello indica in hello `scope` autorizzazioni hello parametro che deve tooacquire utente hello. In hello `p` parametro indica tooexecute criteri hello. Hello tre esempi seguenti (con interruzioni di riga per migliorare la leggibilità) ogni usano criteri diversi. tooget un'idea di come funziona ciascuna richiesta, provare a richiesta hello incollare in un browser e l'esecuzione.

### <a name="use-a-sign-in-policy"></a>Uso di un criterio di accesso
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Uso di un criterio di iscrizione
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Uso di un criterio di modifica del profilo
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametro | Obbligatorio? | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |ID dell'applicazione Hello assegnato app tooyour in hello [portale di Azure](https://portal.azure.com). |
| response_type |Obbligatorio |Deve includere `id_token` per l'accesso a OpenID Connect. Può includere anche il tipo di risposta hello `token`. Se si utilizza `token`, immediatamente l'app può ricevere un token di accesso da hello autorizza un endpoint, senza un toohello richiesta secondo endpoint authorize.  Se si utilizza hello `token` tipo di risposta, hello `scope` parametro deve contenere un ambito che indica quale token hello tooissue della risorsa per. |
| redirect_uri |Consigliato |Hello URI di reindirizzamento dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app. Deve corrispondere esattamente a uno di reindirizzamento hello URI a cui è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in URL. |
| response_mode |Consigliato |Specifica hello metodo toouse toosend hello token tooyour indietro app risultante.  Per i flussi impliciti, usare `fragment`. |
| scope |Obbligatorio |Elenco di ambiti separati da spazi. Il valore di un singolo ambito indica tooAzure AD entrambi delle autorizzazioni di hello che sono stati richiesti. Hello `openid` ambito indica che un toosign autorizzazione nei dati utente e ottenere hello, sull'utente hello sotto forma di hello di token ID. (Verranno fornite informazioni più avanti nell'articolo di hello.) Hello `offline_access` ambito è facoltativo per le applicazioni web. Indica che l'app è necessario un token di aggiornamento per tooresources di accesso di lunga durata. |
| state |Consigliato |Un valore incluso nella richiesta di hello inoltre restituito in risposta token hello. Può essere una stringa di qualsiasi contenuto che si desidera toouse. In genere, viene utilizzato un valore generato casualmente, univoco, attacchi di tooprevent cross-site request forgery. Hello lo stato è anche usato tooencode informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio hello pagina si trovassero in. |
| nonce |Obbligatorio |Un valore incluso nella richiesta di hello (generato da app hello) che è incluso nel token ID risultante hello come attestazione. app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore. In genere, il valore di hello è una stringa casuale, univoca che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| p |Obbligatorio |tooexecute criteri Hello. Hello nome di un criterio che viene creato nel tenant di Azure Active Directory B2C. valore del nome criterio Hello deve iniziare con **b2c\_1\_**. Per altre informazioni, vedere [Criteri incorporati di Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Facoltativo |tipo di Hello dell'interazione dell'utente che ha richiesto. Attualmente, hello unico valore valido è `login`. In questo modo le proprie credenziali hello utente tooenter tale richiesta. L'accesso Single Sign-On non avrà effetto. |

A questo punto, hello verrà chiesto del flusso di lavoro del criterio di toocomplete hello. Questa operazione potrebbe comportare hello immissione di nome utente e password, accedere con un'identità di social networking, iscriversi a directory hello o qualsiasi altro numero di passaggi. Le azioni dell'utente dipendono come criterio di hello è definito.

Al termine di criteri di hello, utente hello Azure AD restituisce una app tooyour risposta al valore di hello utilizzato per `redirect_uri`. Usa metodo hello specificato in hello `response_mode` parametro. risposta Hello è esattamente hello stesso per ogni hello azione scenari utente, indipendentemente dal criterio hello che è stato eseguito.

### <a name="successful-response"></a>Risposta con esito positivo
Una risposta corretta che utilizza `response_mode=fragment` e `response_type=id_token+token` sarà simile seguente hello, interruzioni di riga per migliorare la leggibilità:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| . | Descrizione |
| --- | --- |
| access_token |token di accesso di Hello che hello app richiesto.  token di accesso Hello non deve essere decodificato oppure esaminate in altro modo. ma può essere trattato come una stringa opaca. |
| token_type |valore di tipo di token Hello. Hello solo il tipo che supporta Azure AD connessione. |
| expires_in |durata Hello che hello token di accesso è valido (in secondi). |
| scope |gli ambiti di Hello hello token è valido per. È inoltre possibile utilizzare i token toocache ambiti per un uso successivo. |
| id_token |Hello token ID hello app richiesto. È possibile utilizzare l'identità dell'utente di hello ID tooverify token hello e avviare una sessione utente hello. Per ulteriori informazioni sui token ID e il relativo contenuto, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). |
| state |Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |

### <a name="error-response"></a>Risposta di errore
Le risposte di errore inoltre possono essere inviate toohello URI di reindirizzamento in modo che hello app in grado di gestirle in modo appropriato:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore utilizzato tooclassify tipi di errori che si verificano. È inoltre possibile utilizzare il codice di errore hello per la gestione degli errori. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |
| state |Vedere la descrizione completa di hello in hello tabella precedente. Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici.|

## <a name="validate-hello-id-token"></a>Convalidare i token ID hello
Ricezione di un ID token non è sufficiente tooauthenticate hello. È necessario convalidare la firma del token ID hello e verificare hello attestazioni nel token hello requisiti dell'applicazione. Usa Azure Active Directory B2C [i token Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e pubblica i token toosign di crittografia della chiave e verificare che siano validi.

Molte librerie open source disponibili per la convalida di Jwt, a seconda del linguaggio hello si preferisce toouse. È consigliabile prendere in esame le librerie open source disponibili anziché implementare una logica di convalida personalizzata. È possibile utilizzare informazioni hello in toohelp questo articolo viene illustrato l'utilizzo di tali librerie tooproperly.

Azure AD B2C include un endpoint dei metadati di OpenID Connect. Un'app è possibile utilizzare le informazioni sull'Azure Active Directory B2C toofetch endpoint hello in fase di esecuzione. Queste informazioni includono endpoint, contenuti del token e chiavi per la firma dei token. Il tenant Azure AD B2C include un documento di metadati JSON per ogni criterio. Ad esempio, il documento di metadati hello per i criteri b2c_1_sign_in hello tenant fabrikamb2c.onmicrosoft.com hello si trova in:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Una delle proprietà di hello di questo documento di configurazione è hello `jwks_uri`. valore di Hello per hello stesso criterio sarebbe:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine quali criteri è stato utilizzato toosign un ID token (e in cui toofetch hello i metadati da), sono disponibili due opzioni. In primo luogo, il nome di criterio hello è incluso in hello `acr` di attestazione `id_token`. Per informazioni su come tooparse hello attestazioni da un ID token, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md). L'altra opzione è criteri hello tooencode valore hello hello `state` parametro quando si esegue una richiesta di hello. Decodificare quindi hello `state` toodetermine parametro è stato utilizzato il tipo di criteri. Entrambi i metodi sono validi.

Dopo aver acquistato il documento di metadati hello dall'endpoint di metadati di OpenID Connect hello, è possibile utilizzare hello RSA-256 (che si trova in questo endpoint) le chiavi pubbliche toovalidate hello firma di token ID hello. In un determinato punto nel tempo è possibile che siano presenti più chiavi elencate in questo endpoint, ognuna identificata da un'attestazione `kid`. intestazione Hello di `id_token` contiene inoltre un `kid` attestazione. Indica quali di queste chiavi è toosign utilizzati token di ID hello. Per ulteriori informazioni, inclusi l'apprendimento [convalida dei token](active-directory-b2c-reference-tokens.md#token-validation), vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Dopo aver convalidato firma hello del token ID hello, attestazioni diverse richiedono la verifica. ad esempio:

* Convalidare hello `nonce` tooprevent attacchi di riproduzione token di attestazione. Il valore deve essere specificato nella richiesta di accesso hello.
* Convalidare hello `aud` attestazione tooensure che hello token ID è stato emesso per l'app. Il valore deve essere l'ID applicazione hello dell'app.
* Convalidare hello `iat` e `exp` attestazioni tooensure che hello token ID non sia scaduto.

Le convalide di ulteriori diversi che è necessario eseguire sono descritte in dettaglio in hello [OpenID Connect Core Spec](http://openid.net/specs/openid-connect-core-1_0.html). È inoltre possibile toovalidate ulteriori attestazioni, a seconda dello scenario. Alcune convalide comuni includono:

* Assicura che utente hello o l'organizzazione ha effettuato l'iscrizione per app hello.
* Assicurare che l'utente hello dispone di privilegi e dell'autorizzazione necessaria.
* Verificare che sia stato applicato un determinato livello di autenticazione, ad esempio l'autenticazione a più fattori di Azure.

Per ulteriori informazioni sulle attestazioni hello in un ID token, vedere hello [riferimento del token di Azure Active Directory B2C](active-directory-b2c-reference-tokens.md).

Dopo avere convalidato completamente token ID hello, è possibile iniziare una sessione utente hello. Nell'app, usare le attestazioni hello hello ID token tooobtain informazioni utente hello. Queste informazioni possono essere usate per la visualizzazione, i record, le autorizzazioni e così via.

## <a name="get-access-tokens"></a>Ottenere i token di accesso
Se l'unica cosa hello il toodo esigenze di App web è eseguirà i criteri, è possibile ignorare hello prossime sezioni. informazioni di Hello in hello le sezioni seguenti sono applicabili solo le app tooweb toomake autenticato chiamate tooa web API di cui è necessario e che sono protetti da Azure Active Directory B2C.

Ora che hai effettuato l'accesso utente hello in tooyour a pagina singola applicazione, è possibile ottenere i token di accesso per il web chiamata API che sono protetti da Azure AD. Anche se è già stato ricevuto un token utilizzando hello `token` il tipo di risposta, è possibile utilizzare questo token tooacquire di risorse aggiuntive senza reindirizzamento nuovamente toosign utente hello in.

In un flusso di app web tipiche, questa operazione viene effettuata effettua una richiesta toohello `/token` endpoint.  Tuttavia, endpoint hello non non richieste supporto CORS, in modo da rendere AJAX chiama tooget e token di aggiornamento non è un'opzione. In alternativa, è possibile utilizzare flusso implicito hello in un nascosto HTML iframe elemento tooget nuovi token per altre API web. Di seguito è riportato un esempio, con le interruzioni di riga per migliorare la leggibilità:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parametro | Obbligatorio? | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |ID dell'applicazione Hello assegnato app tooyour in hello [portale di Azure](https://portal.azure.com). |
| response_type |Obbligatorio |Deve includere `id_token` per l'accesso a OpenID Connect.  Può inoltre includere il tipo di risposta hello `token`. Se si utilizza `token` in questo caso, l'app immediatamente può ricevere un token di accesso da hello autorizza un endpoint, senza un toohello richiesta secondo endpoint authorize. Se si utilizza hello `token` tipo di risposta, hello `scope` parametro deve contenere un ambito che indica quale token hello tooissue della risorsa per. |
| redirect_uri |Consigliato |Hello URI di reindirizzamento dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app. Deve corrispondere esattamente a uno di reindirizzamento hello URI è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in URL. |
| scope |Obbligatorio |Elenco di ambiti separati da spazi.  Per ottenere i token, includere tutti gli ambiti richiesti per la risorsa hello previsto. |
| response_mode |Consigliato |Specifica il metodo hello è usato toosend hello risultante token tooyour indietro app.  Può essere `query`, `form_post` o `fragment`. |
| state |Consigliato |Un valore incluso nella richiesta di hello restituito nella risposta token hello.  Può essere una stringa di qualsiasi contenuto che si desidera toouse.  In genere, viene utilizzato un valore generato casualmente, univoco, attacchi di tooprevent cross-site request forgery.  stato di Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello. Ad esempio, utente di hello pagina o una vista di hello è in. |
| nonce |Obbligatorio |Un valore incluso nella richiesta di hello, generato da app hello, che è incluso nel token ID risultante hello come attestazione.  app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore. In genere, il valore di hello è una stringa casuale e univoca che identifica l'origine di hello della richiesta di hello. |
| prompt |Obbligatorio |Utilizzare i token toorefresh e get in un iframe nascosto, `prompt=none` tooensure che hello iframe non improvvisi nella pagina di accesso hello e restituisce immediatamente. |
| login_hint |Obbligatorio |i token di toorefresh e get in un iframe nascosto, includono hello nome utente dell'utente hello in toodistinguish Questo hint tra più sessioni utente hello potrebbe avere in un determinato momento. È possibile estrarre nome utente hello da un precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Obbligatorio |Può essere `consumers` o `organizations`.  Per l'aggiornamento e ottenere i token in un iframe nascosto, è necessario includere hello `domain_hint` valore nella richiesta di hello.  Estrarre hello `tid` attestazione da token ID hello di un precedente Accedi toodetermine toouse il valore.  Se hello `tid` attestazione valore `9188040d-6c67-4c5b-b112-36a304b66dad`, utilizzare `domain_hint=consumers`.  In caso contrario, usare `domain_hint=organizations`. |

Per impostazione hello `prompt=none` parametro, la richiesta sia ha esito positivo o ha immediatamente esito negativo e restituisce tooyour applicazione.  Una risposta corretta viene inviata app tooyour in hello indicato l'URI di reindirizzamento, usando il metodo di hello specificato in hello `response_mode` parametro.

### <a name="successful-response"></a>Risposta con esito positivo
La risposta con esito positivo quando si usa `response_mode=fragment` è simile alla seguente:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parametro | Descrizione |
| --- | --- |
| access_token |token Hello hello app richiesto. |
| token_type |il tipo di token Hello sarà sempre una connessione. |
| state |Se un `state` parametro è incluso nella richiesta di hello, hello stesso valore deve essere visualizzato nella risposta hello. Hello app deve verificare che hello `state` valori hello richiesta e risposta sono identici. |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| scope |gli ambiti di Hello hello token di accesso è valido per. |

### <a name="error-response"></a>Risposta di errore
Le risposte di errore inoltre possono essere inviate toohello URI di reindirizzamento in modo che hello app in grado di gestirle in modo appropriato.  Per `prompt=none` un errore previsto è simile al seguente:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parametro | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano. È inoltre possibile utilizzare hello stringa tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |

Se si riceve questo errore nella richiesta di iframe hello, hello utente necessario in modo interattivo accedere nuovamente tooretrieve un nuovo token. È possibile gestire questa condizione in modo appropriato per l'applicazione.

## <a name="refresh-tokens"></a>Token di aggiornamento
Token ID e token di accesso scadono entrambi dopo un breve periodo di tempo. L'app deve essere preparato toorefresh questi token periodicamente.  eseguire dei tipi di token, toorefresh hello stessa richiesta iframe nascosto è usata in un esempio precedente, utilizzando hello `prompt=none` passaggi toocontrol Azure AD di parametro.  tooreceive un nuovo `id_token` valore, essere toouse che `response_type=id_token` e `scope=openid`e un `nonce` parametro.

## <a name="send-a-sign-out-request"></a>Inviare una richiesta di disconnessione
Quando si desidera toosign hello utente all'esterno dell'app hello, reindirizzamento hello utente tooAzure AD toosign out. Se non si esegue questa operazione, l'utente hello potrebbe essere in grado di tooreauthenticate tooyour app senza dover immettere nuovamente le proprie credenziali. in quanto avrà accesso a una sessione Single Sign-On valida con Azure AD.

È possibile reindirizzare semplicemente hello utente toohello `end_session_endpoint` ovvero elencati in hello stesso documento di metadati di OpenID Connect descritto in [token di convalida hello ID](#validate-the-id-token). ad esempio:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parametro | Obbligatorio? | Descrizione |
| --- | --- | --- |
| p |Obbligatorio |Hello criteri toouse toosign hello dell'utente dall'applicazione. |
| post_logout_redirect_uri |Consigliato |Hello URL utente hello deve essere reindirizzato tooafter riuscita disconnessione. Se non è incluso, Azure AD B2C viene visualizzato un utente toohello messaggio generico. |

> [!NOTE]
> Indirizzamento hello utente toohello `end_session_endpoint` Cancella alcune hello stato dell'utente single sign-on con Azure Active Directory B2C. Tuttavia non accedere utente hello dalla sessione del provider di identità di social networking hello utente. Se l'utente di hello seleziona hello stesso identificare provider durante un successivo Accedi, riautenticare l'utente hello, senza immettere le proprie credenziali. Se un utente desideri toosign dall'applicazione Azure Active Directory B2C, non necessariamente significa che desiderano toocompletely disconnettiti proprio account Facebook, ad esempio. Tuttavia, per gli account locali, hello sessione verrà terminata correttamente.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Usare il tenant personale di Azure AD B2C
Queste richieste, completare tootry hello tre passaggi. Sostituire i valori di esempio hello che viene usato in questo articolo con valori personalizzati:

1. [Creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md). Utilizzare il nome di hello del tenant nelle richieste di hello.
2. [Creare un'applicazione](active-directory-b2c-app-registration.md) tooobtain un ID applicazione e un `redirect_uri` valore. Includere un'API Web o un'app Web nell'app. Se lo si desidera, è possibile creare un segreto dell'applicazione.
3. [Creare i criteri](active-directory-b2c-reference-policies.md) tooobtain i nomi dei criteri.

## <a name="samples"></a>Esempi

* [Creare un'app a singola pagina con Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Creare un'app a singola pagina con .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

