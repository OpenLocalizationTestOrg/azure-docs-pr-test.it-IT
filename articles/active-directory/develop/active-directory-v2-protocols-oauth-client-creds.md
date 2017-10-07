---
title: Azure AD aaaUse v 2.0 tooaccess proteggere le risorse senza l'intervento dell'utente | Documenti Microsoft
description: Applicazioni web tramite l'implementazione di hello Azure AD hello OAuth 2.0 del protocollo di autenticazione.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Flusso di Azure Active Directory v 2.0 e hello OAuth 2.0 credenziali client
È possibile utilizzare hello [concessione di credenziali client OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), talvolta denominato *due fasi OAuth*, tooaccess ospitato sul web di risorse utilizzando hello identità di un'applicazione. Questo tipo di concessione in genere viene utilizzato per le interazioni di server a server che devono essere eseguito in background di hello, senza interazione immediato a un utente. Questi tipi di applicazioni sono spesso di cui viene fatto riferimento tooas *daemon* o *gli account del servizio*.

> [!NOTE]
> endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità. toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

In più comune di comunicazione hello *OAuth tre schede di rete*, un'applicazione client è tooaccess autorizzazione concessa una risorsa per conto di un utente specifico. autorizzazione Hello viene delegata dall'utente toohello un'applicazione hello, in genere durante hello [consenso](active-directory-v2-scopes.md) processo. Tuttavia, nel flusso di credenziali client hello, le autorizzazioni vengono concesse direttamente toohello applicazione stessa. Quando l'applicazione hello presenta una risorsa tooa token, risorse hello impone che app hello stessa dispone di autorizzazione tooperform un'azione, e non utente hello non dispone di autorizzazioni.

## Diagramma di protocollo
flusso di credenziali client intera Hello ha un aspetto simile toohello nel diagramma seguente. Viene descritto ciascuno di hello passaggi più avanti in questo articolo.

![Flusso di credenziali client](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Ottenere l'autorizzazione diretta
Un'app in genere ne riceve autorizzazione diretto tooaccess una risorsa in uno dei due modi: tramite un elenco di controllo di accesso (ACL) a risorse hello o assegnazione di autorizzazione dell'applicazione in Azure Active Directory (Azure AD). Questi due metodi sono hello più comune in Azure AD e li consigliati per i client e risorse che eseguono il flusso di credenziali client hello. Una risorsa può scegliere tooauthorize dei client in altri modi, tuttavia. Ogni server di risorse è possibile scegliere il metodo hello hello più utile per l'applicazione.

### Elenchi di controllo di accesso
Un provider di risorse potrebbe imporre un controllo delle autorizzazioni in base a un elenco di ID applicazione che riconosce e concedere uno specifico livello di accesso. Quando la risorsa hello riceve un token dall'endpoint v 2.0 hello, può decodificare token hello ed estrarre l'ID dell'applicazione del client hello da hello `appid` e `iss` attestazioni. Confronta quindi un'applicazione hello contro un ACL che gestisce. granularità dell'ACL Hello e metodo potrebbe variare notevolmente tra le risorse.

Un caso di utilizzo comune è toouse toorun un ACL test per un'applicazione web o per un'API Web. Hello API Web può fornire solo un sottoinsieme di client specifico di autorizzazioni complete tooa. test end-to-end toorun su hello API, creare un client di test che acquisisce i token dall'endpoint v 2.0 hello e li invia toohello API. ID dell'applicazione del client per l'intera funzionalità toohello dell'API di accesso completo di test hello API quindi controlli hello ACL per hello. Se si utilizza questo tipo di ACL, assicurarsi toovalidate hello non solo del chiamante `appid` valore. Verificare inoltre che hello `iss` valore del token hello è attendibile.

Questo tipo di autorizzazione è comune per daemon e gli account di servizio che richiedono dati tooaccess di proprietà degli utenti che dispongono di account Microsoft personale. Per i dati appartenenti a organizzazioni, si consiglia di usufruire di autorizzazione necessaria di hello tramite le autorizzazioni dell'applicazione.

### Autorizzazioni dell'applicazione
Invece di usare gli ACL, è possibile utilizzare le API tooexpose un set di autorizzazioni per l'applicazione. Un'applicazione l'autorizzazione viene concessa tooan applicazione dall'amministratore dell'organizzazione e possono essere utilizzato tooaccess solo dati di proprietà dell'organizzazione e i relativi dipendenti. Ad esempio, Microsoft Graph espone diverse applicazione autorizzazioni toodo hello che segue:

* Lettura di e-mail in tutte le caselle e-mail
* Lettura e scrittura di e-mail in tutte le caselle e-mail
* Invio di e-mail come utente
* Leggi i dati della directory

Per ulteriori informazioni sulle autorizzazioni per l'applicazione, andare troppo[Microsoft Graph](https://graph.microsoft.io).

autorizzazioni per l'applicazione toouse nell'app, hello passaggi illustrate nelle sezioni successive di hello.

#### Richiedere le autorizzazioni di hello nel portale di registrazione applicazione hello
1. Passare tooyour applicazione hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o [creare un'app](active-directory-v2-app-registration.md), se hai già fatto. È necessario toouse almeno un segreto dell'applicazione quando si crea l'applicazione.
2. Individuare hello **autorizzazioni applicazione dirette** sezione e quindi aggiungere le autorizzazioni di hello che richiede l'app.
3. **Salvare** hello registrazione dell'app.

#### Consigliato: Sign hello utente tooyour app
In genere, quando si compila un'applicazione che utilizza le autorizzazioni dell'applicazione, hello app richiede una pagina o una vista in cui hello admin approva le autorizzazioni dell'applicazione hello. Questa pagina può far parte di flusso di accesso hello dell'applicazione, parte delle impostazioni dell'applicazione hello, o può essere dedicato flusso "connect". In molti casi, è opportuno per hello app tooshow questo "connect" visualizzazione solo dopo che un utente ha eseguito l'accesso con un lavoro o scuola account Microsoft.

Se si esegue l'utente hello in tooyour app, è possibile identificare l'organizzazione hello toowhich hello appartenenza prima di inserire hello utente tooapprove autorizzazioni per l'applicazione hello. Sebbene non sia strettamente necessario, questo consente di creare un'esperienza più intuitiva per gli utenti. toosign hello utente, seguire il nostro [esercitazioni protocollo v 2.0](active-directory-v2-protocols.md).

#### Richiedere le autorizzazioni di hello da un amministratore di directory
Quando sarai pronto toorequest autorizzazioni da amministratore dell'organizzazione hello, è possibile reindirizzare hello utente toohello 2.0 *admin consenso endpoint*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| . | Condizione | Descrizione |
| --- | --- | --- |
| tenant |Obbligatorio |tenant di directory Hello che si desidera toorequest autorizzazioni. Può essere fornito nel formato di nome descrittivo o GUID. Se non si conosce quale utente hello tenant appartiene tooand desiderato toolet loro l'accesso con un tenant, usare `common`. |
| client_id |Obbligatorio |l'ID applicazione Hello che hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assegnato tooyour app. |
| redirect_uri |Obbligatorio |Hello URI in cui si desidera hello toobe di risposta inviato per l'app toohandle di reindirizzamento. Deve corrispondere esattamente a uno di reindirizzamento hello URI a cui è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in URL e che può contenere segmenti di percorso aggiuntive. |
| state |Consigliato |Un valore che è incluso nella richiesta di hello inoltre restituito in risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. lo stato di Hello è tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |

A questo punto, Azure AD applica nella richiesta di hello toocomplete può accedere solo un amministratore tenant. verrà richiesto amministratore Hello tooapprove che tutti hello autorizzazioni applicazione diretta richiesti per l'app nel portale di registrazione applicazione hello.

##### Risposta con esito positivo
Se salve Approva autorizzazioni hello per l'applicazione, la risposta corretta hello simile al seguente:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| . | Descrizione |
| --- | --- | --- |
| tenant |tenant di directory Hello concesse le autorizzazioni per l'applicazione hello che siano richieste, in formato GUID. |
| state |Un valore che è incluso nella richiesta di hello inoltre restituito in risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. lo stato di Hello è tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| admin_consent |Impostare troppo**true**. |

##### Risposta di errore
Se salve non approvare autorizzazioni hello per l'applicazione, hello Impossibile risposta ha un aspetto simile al seguente:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| . | Descrizione |
| --- | --- | --- |
| error |Una stringa di codice di errore che è possibile utilizzare tooclassify tipi di errori e che è possibile utilizzare tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore. |

Dopo aver ricevuto una risposta corretta dall'endpoint di provisioning di app hello, l'app ha ottenuto le autorizzazioni applicazione diretta hello quando richiesto. Ora è possibile richiedere un token per la risorsa hello desiderati.

## Acquisizione di un token
Dopo aver acquistato autorizzazione necessaria hello per l'applicazione, procedere con l'acquisizione di token di accesso per le API. tooget un token con concessione di credenziali client hello, inviare un toohello richiesta POST `/token` v 2.0 endpoint:

### Primo caso: richiesta del token di accesso con un segreto condiviso

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parametro | Condizione | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |l'ID applicazione Hello che hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assegnato tooyour app. |
| scope |Obbligatorio |passato valore Hello per hello `scope` parametro in questa richiesta deve essere l'identificatore di risorsa hello (URI ID applicazione) della risorsa hello desiderato, provvisto hello `.default` suffisso. Ad esempio Microsoft Graph hello hello è `https://graph.microsoft.com/.default`. Questo valore indica l'endpoint v 2.0 hello che di tutte le autorizzazioni applicazione diretta di hello che è stato configurato per l'app, è necessario emettere un token per hello quelli associati alla risorsa hello da toouse. |
| client_secret |Obbligatorio |Segreto dell'applicazione che è stato generato per l'app nel portale di registrazione applicazione hello Hello. |
| grant_type |Obbligatorio |Deve essere `client_credentials`. |

### Secondo caso: richiesta del token di accesso con un certificato

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parametro | Condizione | Descrizione |
| --- | --- | --- |
| client_id |Obbligatorio |l'ID applicazione Hello che hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assegnato tooyour app. |
| scope |Obbligatorio |passato valore Hello per hello `scope` parametro in questa richiesta deve essere l'identificatore di risorsa hello (URI ID applicazione) della risorsa hello desiderato, provvisto hello `.default` suffisso. Ad esempio Microsoft Graph hello hello è `https://graph.microsoft.com/.default`. Questo valore indica l'endpoint v 2.0 hello che di tutte le autorizzazioni applicazione diretta di hello che è stato configurato per l'app, è necessario emettere un token per hello quelli associati alla risorsa hello da toouse. |
| client_assertion_type |Obbligatoria |il valore di Hello deve essere`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Obbligatoria | Un'asserzione (JSON Web Token) che è necessario toocreate e certificato di firma con hello è registrato come credenziali per l'applicazione. Conoscenza [credenziali del certificato](active-directory-certificate-credentials.md) toolearn come tooregister il formato di certificato e hello di asserzione hello.|
| grant_type |Obbligatorio |Deve essere `client_credentials`. |

Si noti che i parametri di hello sono quasi uguale a quello nel caso di hello della richiesta di hello hello dal segreto condiviso a ad eccezione del fatto che il parametro client_secret hello viene sostituito da due parametri: un client_assertion_type e client_assertion.

### Risposta con esito positivo
Una risposta con esito positivo ha un aspetto simile al seguente:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parametro | Descrizione |
| --- | --- |
| access_token |token di accesso richiesto Hello. app Hello è possibile utilizzare questo toohello tooauthenticate token risorsa, ad esempio tooa API Web protetta. |
| token_type |Indica il valore di tipo di token hello. Hello solo tipo di Azure AD supporta `bearer`. |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |

### Risposta di errore
La risposta di errore è simile alla seguente:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Una stringa di codice di errore che è possibile utilizzare per i tipi di errori che si verificano e tooreact tooerrors tooclassify. |
| error_description |Un messaggio di errore specifico che può aiutarti a identificare causa radice di hello di un errore di autenticazione. |
| error_codes |Elenco dei codici di errore specifici del servizio token di sicurezza utile per la diagnostica. |
| timestamp |ora di Hello in corrispondenza del quale si è verificato l'errore hello. |
| trace_id |Identificatore univoco per la richiesta di hello che potrebbe facilitare la diagnostica. |
| correlation_id |Identificatore univoco per la richiesta di hello che potrebbe contribuire alla diagnostica, tra i componenti. |

## Usare di un token
Ora che è stato acquisito un token, utilizzare hello toomake token richieste toohello risorse. Quando il token hello scade, ripetere hello richiesta toohello `/token` tooacquire endpoint un token di accesso aggiornata.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Esempio di codice
vedere un esempio di un'applicazione che implementa hello concessione di credenziali client utilizzando endpoint di autorizzazione Amministrazione hello, toosee nostri [nell'esempio di codice daemon v 2.0](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
