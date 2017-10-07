---
title: applicazioni a pagina singola aaaSecure tramite flusso implicito v 2.0 di hello Azure AD | Documenti Microsoft
description: Creazione di applicazioni web tramite l'implementazione di v 2.0 di Azure AD di flusso implicito hello per le applicazioni a pagina singola.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# v 2.0 protocolli - stabilimenti termali tramite flusso implicito hello
Con l'endpoint di hello v 2.0, è possibile accedere gli utenti alle App singola pagina con gli account personali e di lavoro o dell'istituto di istruzione di Microsoft.  Pagina singola e altre App JavaScript che eseguono principalmente in un tipo di carattere del browser alcuni interessanti richiede quando si deriva tooauthentication:

* caratteristiche di sicurezza Hello di queste App sono sostanzialmente diverse dalle applicazioni web basate su server tradizionale.
* Molti server di autorizzazione e provider di identità non supportano le richieste CORS.
* Pagina intera browser reindirizzamenti lontano da app hello diventano toohello particolarmente invasivo esperienza dell'utente.

Per queste applicazioni (pensare: AngularJS, Ember.js, React.js, e così via) AD Azure supporta il flusso di concessione implicita OAuth 2.0 hello.  flusso implicito Hello è descritta in hello [specifica di OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.2).  Il principale vantaggio è che consente i token di hello app tooget da Azure AD senza eseguire uno scambio di credenziali server back-end.  In questo modo hello app toosign utente hello, mantenimento della sessione e ottenere i token tooother web API tutti codice hello client JavaScript.  Esistono alcuni tootake considerazioni di sicurezza importanti in considerazione quando si utilizza in modo specifico il flusso implicito hello - [client](http://tools.ietf.org/html/rfc6749#section-10.3) e [rappresentazione utente](http://tools.ietf.org/html/rfc6749#section-10.3).

Se si desidera toouse flusso implicito di hello e app di Azure AD tooadd authentication tooyour JavaScript, è consigliabile utilizzare la libreria JavaScript open source, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Sono disponibili alcune esercitazioni AngularJS [qui](active-directory-appmodel-v2-overview.md#getting-started) toohelp iniziare.  

Tuttavia, se si preferisce non toouse una libreria dei messaggi di protocollo singola pagina app e inviare personalmente, procedura hello generale seguente.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## Diagramma di protocollo
Hello accesso implicito intero flusso sarà simile al seguente: hello passaggi sono descritti in dettaglio di seguito.

![Corsie di OpenID Connect](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Inviare una richiesta di accesso hello
accesso tooinitially hello utente nell'app, è possibile inviare un [OpenID Connect](active-directory-v2-protocols-oidc.md) richiesta di autorizzazione e ottenere un `id_token` dall'endpoint di hello v 2.0:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Fare clic sul collegamento di hello sotto tooexecute questa richiesta. Dopo aver effettuato l'accesso, il browser dovrebbe essere reindirizzato troppo`https://localhost/myapp/` con un `id_token` nella barra degli indirizzi hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parametro |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatoria |Id dell'applicazione il portale di registrazione hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assegnato l'app. |
| response_type |Obbligatoria |Deve includere `id_token` per l'accesso a OpenID Connect.  Può inoltre includere hello response_type `token`. Utilizzando `token` qui consentirà il tooreceive app un token di accesso immediatamente da hello autorizza un endpoint senza dovere toomake autorizzare un toohello richiesta secondo endpoint.  Se si utilizza hello `token` response_type, hello `scope` parametro deve contenere un ambito che indica quale token hello tooissue della risorsa per. |
| redirect_uri |consigliato |redirect_uri Hello dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app.  Deve corrispondere esattamente uno dei redirect_uris hello che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in url. |
| scope |Obbligatoria |Elenco di ambiti separati da spazi.  Per OpenID Connect, deve includere ambito hello `openid`, che converte l'autorizzazione "Accesso" toohello nell'interfaccia utente di consenso hello.  Facoltativamente, è inoltre possibile hello tooinclude `email` o `profile` [ambiti](active-directory-v2-scopes.md) per ottenere l'accesso ai dati dell'utente tooadditional.  È anche possibile includere altri ambiti in questa richiesta per la richiesta di consenso toovarious risorse. |
| response_mode |consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello risultante token tooyour indietro app.  Deve essere `fragment` per il flusso implicito hello. |
| state |consigliato |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello.  Può trattarsi di una stringa di qualsiasi contenuto.  Per [evitare gli attacchi di richiesta intersito falsa](http://tools.ietf.org/html/rfc6749#section-10.12), viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| nonce |Obbligatoria |Un valore incluso nella richiesta di hello, generato da app hello, che verranno inclusi nella richiesta id_token risultante hello come attestazione.  app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore.  valore di Hello in genere è una stringa casuale, univoca che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| prompt |Facoltativa |Indica il tipo di hello di interazione utente richiesta.  Hello solo i valori validi in questo momento sono 'account di accesso, 'none', 'di consenso e di.  `prompt=login`sarà il force hello tooenter utente le credenziali per tale richiesta, la negazione di single sign-in.  `prompt=none`è hello opposto: garantisce che l'utente hello non è presentato con qualsiasi tipo di prompt interattivo.  Se la richiesta hello può essere completata automaticamente tramite single-sign-on, l'endpoint v 2.0 hello restituirà un errore.  `prompt=consent`finestra di dialogo dopo il segno di utente hello, che richiede autorizzazioni toohello app di hello utente toogrant il consenso verrà hello trigger OAuth. |
| login_hint |Facoltativa |Può essere utilizzato toopre riempimento hello nome utente/posta elettronica campo indirizzo hello pagina di accesso per utente hello, se si conosce il nome utente anticipatamente.  Spesso le applicazioni utilizzano il parametro durante la riesecuzione dell'autenticazione, che già estratto hello username da una precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Facoltativa |Può essere uno di `consumers` o `organizations`.  Se incluso, non verrà eseguita il processo di individuazione basata su posta elettronica hello che l'utente passa attraverso nella pagina, hello v 2.0 accesso iniziali tooa leggermente più semplice l'esperienza utente.  Spesso le applicazioni utilizzano il parametro durante la riautenticazione, estraendo hello `tid` attestazione da id_token hello.  Se hello `tid` attestazione valore `9188040d-6c67-4c5b-b112-36a304b66dad`, si consiglia di utilizzare `domain_hint=consumers`.  In caso contrario, usare `domain_hint=organizations`. |

A questo punto, si sarà utente hello frequenti tooenter le credenziali e autenticazione hello completo.  Hello v 2.0 endpoint assicura anche che l'utente hello ha acconsentito autorizzazioni toohello indicate nella hello `scope` parametro di query.  Se l'utente hello non ha accettato le condizioni tooany di tali autorizzazioni, viene chiesto hello utente tooconsent toohello necessarie autorizzazioni.  Questo articolo contiene informazioni dettagliate su [autorizzazioni, consenso e app multi-tenant](active-directory-v2-scopes.md).

Una volta utente hello autentica e concede il consenso, endpoint v 2.0 hello restituirà un'app tooyour risposta in hello indicato `redirect_uri`, utilizzando il metodo di hello specificato nel hello `response_mode` parametro.

#### Risposta con esito positivo
Una risposta con esito positivo tramite `response_mode=fragment` e `response_type=id_token+token` sarà simile seguente hello, interruzioni di riga per migliorare la leggibilità:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| . | Descrizione |
| --- | --- |
| access_token |Incluso se `response_type` include `token`. token di accesso Hello hello app richiesta, in questo caso per hello Microsoft Graph.  token di accesso Hello non deve essere decodificato oppure controllato in caso contrario, può essere gestita come stringa opaca. |
| token_type |Incluso se `response_type` include `token`.  È sempre `Bearer`. |
| expires_in |Incluso se `response_type` include `token`.  Indica il numero di hello di hello token è valido, per la memorizzazione di secondi. |
| scope |Incluso se `response_type` include `token`.  Indica gli ambiti di hello per cui hello access_token saranno validi. |
| id_token |id_token Hello che hello app richiesto. È possibile utilizzare l'identità dell'utente di hello id_token tooverify hello e avviare una sessione utente hello.  Ulteriori informazioni su id_tokens e il relativo contenuto è incluso in hello [riferimento dell'endpoint token v 2.0](active-directory-v2-tokens.md). |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |

#### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo da gestire in modo appropriato le app hello:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

## Convalidare hello id_token
Solo la ricezione di un id_token, non è sufficiente tooauthenticate hello utente è necessario convalidare la firma del id_token hello e verificare hello attestazioni nel token hello requisiti dell'applicazione.  Hello v 2.0 endpoint utilizza [i token Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) e pubblica i token toosign di crittografia della chiave e verificare che siano validi.

È possibile scegliere hello toovalidate `id_token` nel codice client, ma una pratica comune è hello toosend `id_token` server back-end tooa ed eseguire la convalida di hello non esiste.  Dopo aver verificato la firma hello di hello id_token, esistono alcuni attestazioni che sarà tooverify obbligatorio.  Vedere hello [riferimento token v 2.0](active-directory-v2-tokens.md) per ulteriori informazioni, tra cui [convalida token](active-directory-v2-tokens.md#validating-tokens) e [importanti informazioni sulla firma Rollover della chiave](active-directory-v2-tokens.md#validating-tokens).  È consigliabile usare una libreria per l'analisi e la convalida dei token. È disponibile almeno una libreria per la maggior parte dei linguaggi e delle piattaforme.
<!--TODO: Improve hello information on this-->

È inoltre possibile toovalidate attestazioni aggiuntive a seconda dello scenario.  Alcune convalide comuni includono:

* Garantire hello utente o l'organizzazione ha effettuato l'iscrizione per app hello.
* Verifica utente hello dispone di autorizzazione diritti
* Garantire che sia stato applicato un determinato livello di autenticazione, ad esempio l'autenticazione a più fattori.

Per ulteriori informazioni sulle attestazioni hello in un id_token, vedere hello [riferimento dell'endpoint token v 2.0](active-directory-v2-tokens.md).

Dopo aver verificato completamente id_token hello, è possibile avviare una sessione utente hello e usare le attestazioni hello hello id_token tooobtain informazioni utente hello nell'app.  Queste informazioni possono essere usate per la visualizzazione, i record, le autorizzazioni e così via.

## Ottenere i token di accesso
Ora che si è effettuato l'accesso utente hello app singola pagina, è possibile ottenere i token di accesso per il chiamante di web API protette da Azure AD, ad esempio hello [Microsoft Graph](https://graph.microsoft.io).  Anche se già ricevuto un token utilizzando hello `token` response_type, è possibile utilizzare le risorse di tooadditional questo metodo tooacquire token senza tooredirect hello utente toosign in.

Nel flusso di OpenID Connect/OAuth hello normale, è questa operazione viene effettuata eseguendo una versione 2.0 toohello richiesta `/token` endpoint.  Tuttavia, endpoint v 2.0 hello non non richieste supporto CORS, in modo da rendere AJAX chiama tooget e token di aggiornamento non rientra domanda hello.  In alternativa, è possibile utilizzare flusso implicito hello in un iframe nascosto tooget nuovi token per altre API web: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Provare a copiare e incollare hello di sotto di richiesta in una scheda del browser. (Non dimenticare hello tooreplace `domain_hint` e hello `login_hint` valori con hello correggere i valori per l'utente)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obbligatoria |Id dell'applicazione il portale di registrazione hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assegnato l'app. |
| response_type |Obbligatoria |Deve includere `id_token` per l'accesso a OpenID Connect.  Può anche includere altri parametri response_type, ad esempio `code`. |
| redirect_uri |consigliato |redirect_uri Hello dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app.  Deve corrispondere esattamente uno dei redirect_uris hello che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in url. |
| scope |Obbligatoria |Elenco di ambiti separati da spazi.  Per ottenere i token, includere tutti [ambiti](active-directory-v2-scopes.md) desiderate per la risorsa hello di interesse. |
| response_mode |consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello risultante token tooyour indietro app.  Può essere uno di `query`, `form_post` o `fragment`. |
| state |consigliato |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello.  Può trattarsi di una stringa di qualsiasi contenuto.  Per evitare gli attacchi di richiesta intersito falsa, viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| nonce |Obbligatoria |Un valore incluso nella richiesta di hello, generato da app hello, che verranno inclusi nella richiesta id_token risultante hello come attestazione.  app Hello consente di verificare che gli attacchi di riproduzione token di toomitigate questo valore.  valore di Hello in genere è una stringa casuale, univoca che può essere utilizzato tooidentify hello origine della richiesta di hello. |
| prompt |Obbligatoria |Per l'aggiornamento e ottenere i token in un iframe nascosto, è consigliabile utilizzare `prompt=none` tooensure che hello iframe non di blocco hello nella pagina di accesso v 2.0 e viene restituito immediatamente. |
| login_hint |Obbligatoria |Per l'aggiornamento e ottenere i token in un iframe nascosto, è necessario includere nome utente hello hello utente in questo hint in ordine toodistinguish tra più sessioni utente hello potrebbe avere in un determinato punto nel tempo. È possibile estrarre nome utente hello da una precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Obbligatoria |Può essere uno di `consumers` o `organizations`.  Per l'aggiornamento e ottenere i token in un iframe nascosto, è necessario includere domain_hint hello nella richiesta di hello.  È necessario estrarre hello `tid` attestazione da id_token hello di un precedente toodetermine Accedi toouse il valore.  Se hello `tid` attestazione valore `9188040d-6c67-4c5b-b112-36a304b66dad`, si consiglia di utilizzare `domain_hint=consumers`.  In caso contrario, usare `domain_hint=organizations`. |

Ringrazia toohello `prompt=none` parametro, la richiesta verrà sia riuscita o non riescono immediatamente e restituire tooyour applicazione.  Una risposta corretta sarà inviata app tooyour hello indicato `redirect_uri`, utilizzando il metodo di hello specificato nel hello `response_mode` parametro.

#### Risposta con esito positivo
Una risposta con esito positivo che usa `response_mode=fragment` ha un aspetto simile al seguente:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Parametro | Descrizione |
| --- | --- |
| access_token |token Hello hello app richiesto. |
| token_type |È sempre `Bearer`. |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. Hello app deve verificare che i valori dello stato hello hello richiesta e risposta sono identici. |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| scope |gli ambiti di Hello hello token di accesso è valido per. |

#### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo app hello possibile gestirli nel modo appropriato.  Nel caso di hello di `prompt=none`, sarà un errore previsto:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| . | Descrizione |
| --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore di autenticazione. |

Se si riceve questo errore nella richiesta di iframe hello, hello utente necessario in modo interattivo accedere nuovamente tooretrieve un nuovo token.  È possibile scegliere questo caso toohandle in modo significativo per l'applicazione.

## Aggiornare i token
Entrambi `id_token`s e `access_token`s scadrà dopo un breve periodo di tempo, pertanto l'app deve essere preparata toorefresh questi token periodicamente.  toorefresh uno tipo di token, è possibile eseguire hello stessa richiesta iframe nascosto di sopra del utilizzando hello `prompt=none` parametro comportamento toocontrol Azure AD.  Se si desidera tooreceive un nuovo `id_token`, toouse assicurarsi di essere `response_type=id_token` e `scope=openid`, nonché una `nonce` parametro.

## Invio di una richiesta di disconnessione
Hello OpenIdConnect `end_session_endpoint` toosend l'app consente a un tooend di endpoint v 2.0 toohello di richiesta dell'utente, un cookie di sessione e deselezionare l'impostazione endpoint v 2.0 hello.  toofully accedere un utente da un'applicazione web, l'app deve terminare una propria sessione con utente hello (in genere mediante la cancellazione di una cache dei token o l'eliminazione dei cookie) e quindi reindirizzare hello browser:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono `common`, `organizations`, `consumers`e gli identificatori del tenant.  Per altre informazioni, vedere le [nozioni di base sul protocollo](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | consigliato | URL Hello hello utente devono essere restituiti tooafter disconnessione completa. Questo valore deve corrispondere a uno di reindirizzamento hello che URI registrati per l'applicazione hello. Se viene omesso, è possibile che l'utente hello verrà visualizzato un messaggio generico dall'endpoint di hello v 2.0. |
