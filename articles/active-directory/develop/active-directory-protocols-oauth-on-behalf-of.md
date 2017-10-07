---
title: aaaAzure AD servizio tooservice autenticazione tramite OAuth 2.0 On-Behalf-Of bozza di specifica | Documenti Microsoft
description: In questo articolo viene descritto come toouse HTTP messaggi tooimplement servizio tooservice l'autenticazione usando hello OAuth 2.0 On-Behalf-Of flusso.
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Servizio tooservice chiama utilizzando l'identità utente delegato in hello flusso On-Behalf-Of
Hello flusso OAuth 2.0 On-Behalf-Of serve il caso d'uso di hello in cui un'applicazione richiama un servizio o API web, che a sua volta deve toocall un altro servizio web API. l'idea Hello è hello toopropagate delega di identità dell'utente e le autorizzazioni mediante una catena di richieste di hello. Per hello servizio di livello intermedio toomake autenticato richieste toohello servizio downstream, è necessario toosecure un token di accesso da Azure Active Directory (Azure AD), per conto di utente hello.

## Diagramma del flusso on-behalf-of
Si supponga che l'utente hello è stato autenticato in un'applicazione utilizzando hello [flusso di concessione del codice di autorizzazione OAuth 2.0](active-directory-protocols-oauth-code.md). A questo punto, un'applicazione hello ha un token di accesso (A token) con attestazioni dell'utente hello e web di livello intermedio di consenso tooaccess hello API (API A). API A questo punto, è necessario toomake un'API web downstream di richiesta autenticata toohello (API B).

passaggi Hello costituiscono flusso di On-Behalf-Of hello e vengono descritte insieme hello hello seguente diagramma.

![Flusso on-behalf-of di OAuth2.0](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. un'applicazione client Hello rende tooAPI una richiesta con r. token hello
2. API A autentica toohello endpoint di rilascio dei token di Azure AD e richiede un token tooaccess B. API
3. endpoint di rilascio dei token di Azure AD Hello convalida le credenziali dell'API A con un token e problemi hello token di accesso per le API B (token B).
4. il token di Hello B viene impostato nell'intestazione di autorizzazione hello hello richiesta tooAPI B.
5. Dati da hello risorsa protetta viene restituiti dall'API B.

## Registrare un'applicazione hello e il servizio in Azure AD
Registrare un'applicazione hello client e servizio di livello intermedio hello in Azure AD.
### Registrare il servizio di livello intermedio hello
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Registrazione nuova applicazione**.
5. Immettere un nome descrittivo per l'applicazione hello e selezionare il tipo di applicazione hello. Basata sul tipo di applicazione hello set hello sign-on URL o l'URL di base toohello URL di reindirizzamento. Fare clic su **crea** toocreate un'applicazione hello.
6. Durante l'hello portale di Azure, scegliere l'applicazione e fare clic su **impostazioni**. Scegliere dal menu Impostazioni hello **chiavi** e aggiungere una chiave, selezionare la durata di chiave dell'anno 1 o 2 anni. Quando si salva questa pagina, valore della chiave hello verranno visualizzati, copiare e salvare il valore di hello in un luogo sicuro, poiché sarà necessario questo impostazioni delle chiavi applicazione hello tooconfigure più avanti nell'implementazione - valore di questa chiave non sarà nuovamente visualizzata, né recuperabili da qualsiasi altri mezzi, pertanto si prega di record che non appena è visibile all'hello portale di Azure.

### Registrare un'applicazione hello client
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account e in hello **Directory** elenco, scegliere hello tenant di Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello barra di spostamento a sinistra, quindi scegliere **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Registrazione nuova applicazione**.
5. Immettere un nome descrittivo per l'applicazione hello e selezionare il tipo di applicazione hello. Basata sul tipo di applicazione hello set hello sign-on URL o l'URL di base toohello URL di reindirizzamento. Fare clic su **crea** toocreate un'applicazione hello.
6. Configurare le autorizzazioni per l'applicazione, nel menu Impostazioni hello, scegliere hello **delle autorizzazioni necessarie** sezione, fare clic su **Aggiungi**, quindi **selezionare un'API**e hello di tipo nome del servizio di livello intermedio hello nella casella di testo hello. Fare quindi clic su **Selezionare le autorizzazioni** e selezionare "Accedi a *nome servizio*".

### Configurare applicazioni client note
In questo scenario, il servizio di livello intermedio hello non dispone di alcuna interazione tooobtain hello utente consenso tooaccess hello downstream API. Pertanto, hello opzione toogrant accesso toohello downstream API devono essere presentati iniziale come parte del passaggio di consenso hello durante l'autenticazione.
tooachieve, passaggi hello seguenti di sotto di registrazione dell'app di tooexplicitly binding hello client in Azure AD con la registrazione di hello del servizio di livello intermedio hello, che unisce il consenso hello richiesto dal client hello e di livello intermedio in una singola finestra di dialogo.
1. Passare la registrazione del servizio di livello intermedio di toohello e fare clic su **manifesto** tooopen editor del manifesto hello.
2. Nel manifesto di hello, individuare hello `knownClientApplications` proprietà di matrice e aggiungere l'ID Client dell'applicazione client hello hello come un elemento.
3. Salvare il manifesto hello facendo hello pulsante Salva.

## Richiesta di token di servizio tooservice accesso
toorequest un token di accesso, rendere un endpoint di toohello specifico del tenant di Azure AD HTTP POST con hello seguenti parametri.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Esistono due casi, a seconda se un'applicazione hello client sceglie toobe protetto da un segreto condiviso o un certificato.

### Primo caso: richiesta del token di accesso con un segreto condiviso
Quando si utilizza un segreto condiviso, una richiesta di token di accesso da servizio a servizio contiene hello seguenti parametri:

| . |  | Descrizione |
| --- | --- | --- |
| grant_type |Obbligatoria | tipo di Hello di richiesta di token hello. Per una richiesta usando un token JWT, hello valore deve essere **urn: ietf:params:oauth:grant-tipo: jwt-connessione**. |
| assertion |Obbligatoria | valore di Hello del token hello utilizzato nella richiesta di hello. |
| client_id |Obbligatoria | Hello App assegnato ID servizio chiamante toohello durante la registrazione con Azure AD. Fare clic su toofind hello ID App nel portale di gestione di Azure, hello **Active Directory**, fare clic su directory hello e quindi fare clic su nome dell'applicazione hello. |
| client_secret |Obbligatoria | chiave Hello registrato per la chiamata di servizio in Azure AD hello. Questo valore annotato in fase di hello della registrazione. |
| resource |Obbligatoria | URI ID App del servizio (risorsa protetta) che riceve hello Hello. Fare clic su toofind hello URI ID App nel portale di gestione di Azure, hello **Active Directory**, fare clic su directory hello, fare clic sul nome dell'applicazione hello, fare clic su **tutte le impostazioni** e quindi fare clic su **proprietà** . |
| requested_token_use |Obbligatoria | Specifica la modalità di elaborazione richiesta hello. Nel flusso di On-Behalf-Of hello, hello valore deve essere **on_behalf_of**. |
| scope |Obbligatoria | Elenco di ambiti per richiesta di token hello separati da uno spazio. Per OpenID Connect, hello ambito **openid** deve essere specificato.|

#### Esempio
Hello POST HTTP seguente richiede un token di accesso per l'API web di https://graph.windows.net hello. Hello `client_id` identifica servizio hello che richiede un token di accesso hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Secondo caso: richiesta del token di accesso con un certificato
Una richiesta di token di accesso da servizio a servizio con un certificato contiene hello seguenti parametri:

| . |  | Descrizione |
| --- | --- | --- |
| grant_type |Obbligatoria | tipo di Hello di richiesta di token hello. Per una richiesta usando un token JWT, hello valore deve essere **urn: ietf:params:oauth:grant-tipo: jwt-connessione**. |
| assertion |Obbligatoria | valore di Hello del token hello utilizzato nella richiesta di hello. |
| client_id |Obbligatoria | Hello App assegnato ID servizio chiamante toohello durante la registrazione con Azure AD. Fare clic su toofind hello ID App nel portale di gestione di Azure, hello **Active Directory**, fare clic su directory hello e quindi fare clic su nome dell'applicazione hello. |
| client_assertion_type |Obbligatoria |il valore di Hello deve essere`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Obbligatoria | Un'asserzione (JSON Web Token) che è necessario toocreate e certificato di firma con hello è registrato come credenziali per l'applicazione.  Conoscenza [credenziali del certificato](active-directory-certificate-credentials.md) toolearn come tooregister il formato di certificato e hello di asserzione hello.|
| resource |Obbligatoria | URI ID App del servizio (risorsa protetta) che riceve hello Hello. Fare clic su toofind hello URI ID App nel portale di gestione di Azure, hello **Active Directory**, fare clic su directory hello, fare clic sul nome dell'applicazione hello, fare clic su **tutte le impostazioni** e quindi fare clic su **proprietà** . |
| requested_token_use |Obbligatoria | Specifica la modalità di elaborazione richiesta hello. Nel flusso di On-Behalf-Of hello, hello valore deve essere **on_behalf_of**. |
| scope |Obbligatoria | Elenco di ambiti per richiesta di token hello separati da uno spazio. Per OpenID Connect, hello ambito **openid** deve essere specificato.|

Si noti che i parametri di hello sono quasi uguale a quello nel caso di hello della richiesta di hello hello dal segreto condiviso a ad eccezione del fatto che il parametro client_secret hello viene sostituito da due parametri: un client_assertion_type e client_assertion.

#### Esempio
Hello POST HTTP seguente richiede un token di accesso per l'API web https://graph.windows.net hello con un certificato. Hello `client_id` identifica servizio hello che richiede un token di accesso hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Risposta di token di accesso di servizio tooservice
Una risposta con esito positivo è una risposta JSON OAuth 2.0 con hello seguenti parametri.

| . | Descrizione |
| --- | --- |
| token_type |Indica il valore di tipo di token hello. Hello solo tipo di Azure AD supporta **connessione**. Per ulteriori informazioni sui token di connessione, vedere hello [Framework di autorizzazione OAuth 2.0: utilizzo dei Token di connessione (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| scope |ambito Hello di accesso concesso nel token hello. |
| expires_in |lunghezza Hello ora hello token di accesso è valido (in secondi). |
| expires_on |ora di Hello scadenza token di accesso hello. Data di Hello è rappresentata dal numero di hello di secondi da 1970-01-01T0:0:0Z UTC fino a ora di scadenza hello. Questo valore è durata hello toodetermine utilizzati del token memorizzati nella cache. |
| resource |URI ID App del servizio (risorsa protetta) che riceve hello Hello. |
| access_token |token di accesso richiesto Hello. Hello la chiamata di servizio è possibile utilizzare questo servizio di token tooauthenticate toohello ricevente. |
| id_token |token id richiesto Hello. Utilizzare il tooverify hello identità dell'utente e iniziare una sessione utente hello Hello la chiamata di servizio. |
| refresh_token |token di aggiornamento Hello hello richiesta token di accesso. Hello chiamata servizio toorequest questo token può utilizzare un altro token di accesso alla scadenza del token di accesso corrente hello. |

### Esempio di risposta di esito positivo
Hello esempio seguente mostra una richiesta di tooa risposta di esito positivo per un token di accesso per l'API web di https://graph.windows.net hello.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Esempio di risposta con errore
Una risposta di errore viene restituita dall'endpoint token Azure AD durante il tentativo di tooacquire un token di accesso per l'API a valle hello, se un criterio di accesso condizionale, ad esempio l'autenticazione a più fattori impostato su tale API downstream hello. il servizio di livello intermedio Hello deve area dell'applicazione client toohello errore in modo che un'applicazione hello client può fornire criteri di accesso condizionale hello toosatisfy interazione utente hello.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Utilizzare hello tooaccess token di accesso hello risorsa protetta
Ora il servizio di livello intermedio hello è possibile usare toohello le richieste di token toomake acquisiti in precedenza autenticato hello a valle web API, l'impostazione di token hello in hello `Authorization` intestazione.

### Esempio
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Passaggi successivi
Ulteriori informazioni su protocollo hello OAuth 2.0 e le auth tooservice servizio tooperform modo un altro utilizzando le credenziali del client.
* [Servizio tooservice auth con concessione di credenziali client OAuth 2.0 in Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 in Azure AD](active-directory-protocols-oauth-code.md)
