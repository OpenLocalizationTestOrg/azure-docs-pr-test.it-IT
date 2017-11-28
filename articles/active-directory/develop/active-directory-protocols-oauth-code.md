---
title: hello aaaUnderstand flusso di codice di autorizzazione OAuth 2.0 in Azure AD | Documenti Microsoft
description: In questo articolo viene descritto come accedere a toouse HTTP messaggi tooauthorize tooweb applicazioni e API web nel tenant di utilizzo di Azure Active Directory e OAuth 2.0.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Autorizzare l'accesso tooweb applicazioni tramite OAuth 2.0 e Azure Active Directory
Azure Active Directory (Azure AD) utilizza OAuth 2.0 tooenable tooauthorize accesso tooweb applicazioni si e API web nel tenant di Azure AD. Questa guida è indipendente dal linguaggio e viene descritto come toosend e ricevere messaggi HTTP senza utilizzare uno dei nostri librerie open source.

flusso di codice di autorizzazione OAuth 2.0 Hello è descritta in [sezione 4.1 della specifica OAuth 2.0 hello](https://tools.ietf.org/html/rfc6749#section-4.1). È utilizzato tooperform autenticazione e autorizzazione nella maggior parte dei tipi di applicazione, incluse le app web e le app installate in modo nativo.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Flusso di autorizzazione di OAuth 2.0
A un livello elevato, il flusso di autorizzazione intera hello per un'applicazione è un po' simile al seguente:

![Flusso del codice di autenticazione di OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Richiedere un codice di autorizzazione
flusso di codice di autorizzazione Hello inizia con il client di hello indirizzamento hello utente toohello `/authorize` endpoint. In questa richiesta, il client di hello indica hello autorizzazioni tooacquire utente hello. È possibile ottenere gli endpoint di OAuth 2.0 hello dalla pagina dell'applicazione nel portale di Azure classico, in hello **Visualizza endpoint** pulsante nel cassetto inferiore hello.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono identificatori di tenant, ad esempio, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` per i token indipendente dal tenant |
| client_id |Obbligatoria |Id applicazione assegnato tooyour app Hello quando è stato registrato con Azure AD. È possibile trovare questo nel portale di Azure hello. Fare clic su **Active Directory**, fare clic su directory hello, scegliere un'applicazione hello e fare clic su **Configura** |
| response_type |Obbligatoria |Deve includere `code` per flusso di codice di autorizzazione hello. |
| redirect_uri |consigliato |redirect_uri Hello dell'app, in cui le risposte di autenticazione possono essere inviate e ricevute dall'app.  Deve corrispondere esattamente uno dei redirect_uris hello che è stato registrato nel portale di hello, ad eccezione del fatto che deve essere codificato in url.  Per le app native e mobili, è necessario utilizzare il valore predefinito hello di `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |consigliato |Specifica il metodo hello che deve essere utilizzati toosend hello risultante token tooyour indietro app.  Può essere `query` o `form_post`. |
| state |consigliato |Un valore incluso nella richiesta di hello che viene inoltre restituito in risposta token hello. Per [evitare gli attacchi di richiesta intersito falsa](http://tools.ietf.org/html/rfc6749#section-10.12), viene in genere usato un valore univoco generato casualmente.  stato Hello è anche tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| resource |Facoltativa |Hello URI ID App hello API web (risorsa protetta). Fare clic su toofind hello URI ID App dell'API, web hello nel portale di Azure, hello **Active Directory**, fare clic su directory hello, fare clic su un'applicazione hello e quindi fare clic su **configura**. |
| prompt |Facoltativa |Indicare il tipo di hello dell'interazione dell'utente che è obbligatorio.<p> I valori validi sono: <p> *account di accesso*: utente hello deve essere tooreauthenticate richiesta. <p> *fornire il consenso*: il consenso dell'utente è stata concessa, ma deve toobe aggiornato. utente Hello deve essere tooconsent richiesta. <p> *admin_consent*: un amministratore deve essere tooconsent richieste per conto di tutti gli utenti dell'organizzazione |
| login_hint |Facoltativa |Può essere utilizzato toopre riempimento hello nome utente/posta elettronica campo indirizzo hello-pagina di accesso per utente hello, se si conosce il nome utente anticipatamente.  Spesso le app di usare questo parametro durante la riautenticazione, con già estratto il nome utente hello da una precedente Accedi utilizzando hello `preferred_username` attestazione. |
| domain_hint |Facoltativa |Fornisce un hint sul tenant hello o un dominio che hello utente deve utilizzare toosign in. il valore di Hello di hello domain_hint è un dominio registrato per il tenant di hello. Se tenant hello è una directory locale tooan federato, Azure ad reindirizza server federativo di toohello tenant specificato. |

> [!NOTE]
> Se utente hello fa parte di un'organizzazione, un amministratore dell'organizzazione hello può fornire il consenso o rifiutare per conto dell'utente hello o consentire tooconsent utente hello. Hello l'utente hello opzione tooconsent solo quando l'amministratore di hello lo consente.
>
>

A questo punto, hello verrà chiesto tooenter le credenziali e autorizzazioni toohello consenso indicato in hello `scope` parametro di query. Una volta utente hello autentica e concede il consenso, Azure AD invia un'app tooyour risposta hello `redirect_uri` indirizzo nella richiesta.

### Risposta con esito positivo
Una risposta con esito positivo può avere un aspetto simile al seguente:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parametro | Descrizione |
| --- | --- |
| admin_consent |il valore di Hello è True se un amministratore ha accettato tooa richiesta di consenso. |
| code |codice di autorizzazione Hello che ha richiesto un'applicazione hello. un'applicazione Hello è possibile utilizzare toorequest codice di autorizzazione hello un token di accesso per la risorsa di destinazione hello. |
| session_state |Un valore univoco che identifica una sessione utente corrente hello. Questo valore è un GUID, ma deve essere trattato come un valore opaco passato senza alcun controllo. |
| state |Se un parametro di stato è incluso nella richiesta di hello, hello stesso valore verrà visualizzato nella risposta hello. È buona norma per tooverify applicazione hello che valori dello stato hello hello richiesta e risposta siano identici prima di utilizzare risposta hello. In questo modo toodetect [Cross-Site Request Forgery (CSRF) attacks](https://tools.ietf.org/html/rfc6749#section-10.12) con client hello. |

### Risposta di errore
Le risposte di errore è inoltre possibile inviare toohello `redirect_uri` in modo che un'applicazione hello possibile gestirli nel modo appropriato.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| . | Descrizione |
| --- | --- |
| error |Un valore di codice di errore definito nella sezione 5.2 del hello [Framework di autorizzazione OAuth 2.0](http://tools.ietf.org/html/rfc6749). la tabella successiva Hello descrive i codici di errore hello restituiti da Azure AD. |
| error_description |Una descrizione più dettagliata dell'errore hello. Questo messaggio non è adatto per l'utente finale toobe. |
| state |il valore di stato Hello è un valore non riutilizzabile generato casualmente che viene inviato nella richiesta di hello e restituito in attacchi di hello risposta tooprevent cross-site request forgery (CSRF). |

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

## Utilizzare toorequest codice di autorizzazione hello un token di accesso
Ora che è stato acquisito un codice di autorizzazione e dispongono dell'autorizzazione utente hello, è possibile riscattare il codice di hello per una risorsa di token toohello desiderato di accesso, inviando un toohello richiesta POST `/token` endpoint:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| . |  | Descrizione |
| --- | --- | --- |
| tenant |Obbligatoria |Hello `{tenant}` valore nel percorso di hello della richiesta di hello può essere utilizzato toocontrol che possono accedere a un'applicazione hello.  Hello i valori consentiti sono identificatori di tenant, ad esempio, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` per i token indipendente dal tenant |
| client_id |Obbligatoria |Id applicazione assegnato tooyour app Hello quando è stato registrato con Azure AD. È possibile trovare questo nel portale di Azure classico hello. Fare clic su **Active Directory**, fare clic su directory hello, scegliere un'applicazione hello e fare clic su **Configura** |
| grant_type |Obbligatoria |Deve essere `authorization_code` per flusso di codice di autorizzazione hello. |
| code |Obbligatoria |Hello `authorization_code` acquisito nella sezione precedente hello |
| redirect_uri |Obbligatoria |Hello stesso `redirect_uri` valore che è stato utilizzato tooacquire hello `authorization_code`. |
| client_secret |Obbligatorio per app Web |segreto dell'applicazione Hello creato nel portale di registrazione hello app per l'app.  È consigliabile non usarlo in un'app nativa, perché i segreti client non possono essere archiviati in modo affidabile nei dispositivi.  È necessario per le applicazioni web e web API, che hanno hello toostore possibilità di hello `client_secret` in modo sicuro sul lato server di hello. |
| resource |Obbligatorio se è specificato nella richiesta del codice di autorizzazione, altrimenti facoltativo |Hello URI ID App hello API web (risorsa protetta). |

Fare clic su toofind hello URI ID App nel portale di gestione di Azure, hello **Active Directory**, fare clic su directory hello, fare clic su un'applicazione hello e quindi fare clic su **configura**.

### Risposta con esito positivo
Azure AD restituisce un token di accesso in caso di risposta corretta. chiamate di rete toominimize dall'applicazione client hello e la relativa latenza associata, un'applicazione hello client deve memorizzare nella cache i token di accesso per la durata del token hello specificato nella risposta di OAuth 2.0 hello. durata del token hello toodetermine, utilizzare uno hello `expires_in` o `expires_on` i valori dei parametri.

Se una risorsa API web restituisce un `invalid_token` codice di errore, questo potrebbe indicare che la risorsa hello ha determinato token hello è scaduto. Se l'ora di orologio client e risorse di hello è diversa (noto come un "sfasamento dell'ora"), hello risorsa consideri hello toobe di token è scaduto prima che il token hello viene cancellato dalla cache di hello client. In questo caso, deselezionare il token hello dalla cache di hello, anche se è ancora in corso della sua durata calcolata.

Una risposta con esito positivo può avere un aspetto simile al seguente:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parametro | Descrizione |
| --- | --- |
| access_token |token di accesso richiesto Hello. app Hello è possibile utilizzare questo toohello tooauthenticate token risorsa, ad esempio un'API web protetta. |
| token_type |Indica il valore di tipo di token hello. Hello solo il tipo che supporta Azure AD connessione. Per altre informazioni sui token di connessione, vedere [OAuth2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |Quanto tempo il token di accesso di hello è valido (in secondi). |
| expires_on |ora di Hello scadenza token di accesso hello. Data di Hello è rappresentata dal numero di hello di secondi da 1970-01-01T0:0:0Z UTC fino a ora di scadenza hello. Questo valore è durata hello toodetermine utilizzati del token memorizzati nella cache. |
| resource |Hello URI ID App hello API web (risorsa protetta). |
| scope |Applicazione client toohello di concedere le autorizzazioni di rappresentazione. autorizzazione predefinita Hello `user_impersonation`. il proprietario di Hello di hello risorsa protetta può registrare valori aggiuntivi in Azure AD. |
| refresh_token |Token di aggiornamento di OAuth 2.0. app Hello è possibile usare questo token di accesso aggiuntivi tooacquire token alla scadenza del token di accesso corrente hello.  Aggiornare i token sono di lunga durati e possono essere utilizzati tooretain accesso tooresources per lunghi periodi di tempo. |
| id_token |Token JWT (Token Web JSON) non firmato. Hello app può base64Url decodificare segmenti hello di questo token toorequest informazioni utente hello che ha effettuato l'accesso. app Hello può memorizzare nella cache i valori hello e visualizzarli, ma deve fare affidamento su di essi per qualsiasi autorizzazione o i limiti di sicurezza. |

### Attestazioni nei token JWT
token JWT Hello valore hello hello `id_token` parametro può essere decodificato nelle seguenti attestazioni hello:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Per ulteriori informazioni sui token web JSON, vedere hello [bozza di specifica IETF JWT](http://go.microsoft.com/fwlink/?LinkId=392344). Per altre informazioni sui tipi di token hello e attestazioni, vedere [supportati Token e tipi di attestazione](active-directory-token-and-claims.md)

Hello `id_token` parametro include i seguenti tipi di attestazione hello:

| Tipo di attestazione | Descrizione |
| --- | --- |
| aud |Destinatari del token hello. Quando il token hello viene eseguito l'applicazione client tooa, destinatari hello sono hello `client_id` del client hello. |
| exp |Scadenza. ora di Hello scadenza token hello. Per hello toobe token valido, hello data/ora corrente deve essere minore o uguale toohello `exp` valore. tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino a quando non è stato rilasciato hello ora hello token. |
| family_name |Cognome dell'utente. un'applicazione Hello può visualizzare questo valore. |
| given_name |Nome dell'utente. un'applicazione Hello può visualizzare questo valore. |
| iat |Data e ora di rilascio. ora di Hello emissione hello JWT. tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino a quando non è stato rilasciato hello ora hello token. |
| iss |Identifica l'emittente del token hello |
| nbf |Inizio validità. ora di Hello quando il token hello diventa effettivo. Per hello toobe token valido, hello data/ora corrente deve essere maggiore o uguale toohello Nbf valore. tempo Hello è rappresentato come numero di secondi di hello dal 1 gennaio 1970 (1970-01-01T0:0:0Z) UTC fino a quando non è stato rilasciato hello ora hello token. |
| oid |Identificatore di oggetto (ID) dell'oggetto utente hello in Azure AD. |
| sub |Identificatore del soggetto del token. Si tratta di un identificatore permanente e non modificabile per utente hello hello token descrive. Usare questo valore nella logica di memorizzazione nella cache. |
| tid |Identificatore (ID) del tenant hello Azure AD che ha emesso il token hello del tenant. |
| unique_name |Identificatore univoco che può essere visualizzato toohello utente. È in genere il nome dell'entità utente (UPN). |
| upn |Nome dell'entità utente dell'utente hello. |
| ver |Versione. versione di Hello del token JWT hello, in genere 1.0. |

### Risposta di errore
errori di endpoint di rilascio dei token Hello sono codici di errore HTTP, poiché le chiamate client hello hello endpoint di rilascio dei token direttamente. Inoltre il codice di stato HTTP toohello, endpoint di rilascio dei token di Azure AD hello restituisce inoltre un documento JSON contenente oggetti che descrivono l'errore hello.

Una risposta di errore di esempio può avere un aspetto simile al seguente:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
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

#### Codici di stato HTTP
Hello nella tabella seguente sono elencati i codici di stato HTTP hello hello restituisce endpoint di rilascio dei token. In alcuni casi, il codice di errore hello è sufficiente risposta di hello toodescribe, ma se sono presenti errori, è necessario hello tooparse che accompagna JSON documento ed esaminare il codice di errore.

| Codice HTTP | Descrizione |
| --- | --- |
| 400 |Codice HTTP predefinito. Nella maggior parte dei casi viene in genere a causa di tooa formato della richiesta. Correggere e inviare di nuovo la richiesta hello. |
| 401 |Autenticazione non riuscita. Ad esempio, la richiesta hello hello client_secret parametro mancante. |
| 403 |Autorizzazione non riuscita. Ad esempio, hello insufficienti risorsa hello tooaccess di autorizzazione. |
| 500 |Si è verificato un errore interno nel servizio hello. Ripetere la richiesta hello. |

#### Codici per gli errori degli endpoint di token
| Codice di errore | Descrizione | Azione client |
| --- | --- | --- |
| invalid_request |Errore del protocollo, ad esempio un parametro obbligatorio mancante. |Correggere e inviare di nuovo la richiesta hello |
| invalid_grant |codice di autorizzazione Hello scaduto o non è valido. |Provare un nuovo toohello richiesta `/authorize` endpoint |
| unauthorized_client |Hello client autenticato non è autorizzato toouse tipo di concedere tale autorizzazione. |Ciò si verifica quando un'applicazione hello client non è registrata in Azure AD o non è stato aggiunto il tenant di Azure AD dell'utente toohello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |
| invalid_client |Autenticazione client non riuscita. |le credenziali di Hello del client non sono valide. toofix, l'amministratore dell'applicazione hello Aggiorna credenziali hello. |
| unsupported_grant_type |Hello autorizzazione server non supporta il tipo di hello autorizzazione grant. |Hello modifica concedere tipo nella richiesta di hello. Questo tipo di errore dovrebbe verificarsi solo durante lo sviluppo ed essere rilevato durante il test iniziale. |
| invalid_resource |risorsa di destinazione Hello è valido perché non esiste, Azure AD non riesce a trovarla o non sia configurato correttamente. |Indica la risorsa hello, se presente, non è stata configurata nel tenant di hello. un'applicazione Hello può richiedere utente hello istruzioni per l'installazione di un'applicazione hello e aggiungerlo tooAzure Active Directory. |
| interaction_required |richiesta di Hello richiede l'intervento dell'utente. Ad esempio, è necessario un passaggio di autenticazione aggiuntivo. | Invece di una richiesta non interattivo, riprovare con una richiesta di autorizzazione interattiva per hello stessa risorsa. |
| temporarily_unavailable |server Hello è temporaneamente richiesta hello toohandle troppo occupato. |Ripetere la richiesta hello. un'applicazione Hello client potrebbe spiegare toohello utente che la risposta è in ritardo a causa di condizione temporanea tooa. |

## Utilizzare hello accesso token tooaccess hello risorsa
Ora che è stato acquistato un `access_token`, è possibile utilizzare token hello in tooWeb richieste API, se viene incluso nel hello `Authorization` intestazione. Hello [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) documento spiega in che modo i token di connessione toouse in tooaccess le richieste HTTP protetto risorse.

### Richiesta di esempio
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Risposta di errore
Le risorse protette che implementano RFC 6750 rilasciano codici di stato HTTP. Se la richiesta di hello non include le credenziali di autenticazione o non presenta alcuna risposta hello token, hello include un `WWW-Authenticate` intestazione. Quando una richiesta ha esito negativo, il server di risorse hello risponde con il codice di stato HTTP hello e un codice di errore.

Hello Ecco un esempio di una risposta di esito negativo quando hello client richiesta non include il token di connessione hello:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Parametri dell'errore
| Parametro | Descrizione |
| --- | --- |
| authorization_uri |URI (endpoint fisico) del server di autorizzazione hello Hello. Questo valore viene inoltre utilizzato come una ricerca chiave tooget ulteriori informazioni su server hello da un endpoint di individuazione. <p><p> client Hello deve convalidare tale hello server autorizzazione sia attendibile. Quando la risorsa hello è protetto da Azure AD, è sufficiente tooverify che hello URL inizia con https://login.microsoftonline.com o un altro nome host che supporta Azure AD. Una risorsa specifica del tenant deve sempre restituire un URI di autorizzazione specifico del tenant. |
| error |Un valore di codice di errore definito nella sezione 5.2 del hello [Framework di autorizzazione OAuth 2.0](http://tools.ietf.org/html/rfc6749). |
| error_description |Una descrizione più dettagliata dell'errore hello. Questo messaggio non è adatto per l'utente finale toobe. |
| resource_id |Restituisce hello identificatore univoco della risorsa hello. un'applicazione Hello client è possibile utilizzare questo identificatore come valore di hello di hello `resource` parametro quando si richiede un token per la risorsa hello. <p><p> È importante per hello client applicazione tooverify questo valore, in caso contrario un servizio dannoso potrebbe essere in grado di tooinduce un **l'elevazione dei privilegi** attacco <p><p> Hello consigliato strategia per evitare un attacco è tooverify che hello `resource_id` corrispondenze hello base del web hello URL dell'API che si accede. Ad esempio, se si accede https://service.contoso.com/data, hello `resource_id` può essere htttps://service.contoso.com/. un'applicazione Hello client deve respingere un `resource_id` che non inizia con l'URL di base hello a meno che non è presente un id di hello tooverify modo alternativo attendibile. |

#### Codici errore dello schema di connessione
Hello specifica RFC 6750 definisce i seguenti errori di risorse che utilizzano lo schema di trasporto e di intestazione WWW-Authenticate hello in risposta hello hello.

| Codice di stato HTTP | Codice di errore | Descrizione | Azione client |
| --- | --- | --- | --- |
| 400 |invalid_request |richiesta di Hello non è corretto. Ad esempio, è possibile che sia disponibile un parametro o utilizzando hello stesso parametro due volte. |Correggere l'errore hello e ripetere hello richiesta. Questo tipo di errore dovrebbe verificarsi solo durante lo sviluppo ed essere rilevato nel test iniziale. |
| 401 |invalid_token |token di accesso Hello è mancante, non è valido o è stato revocato. il valore di Hello del parametro error_description hello vengono forniti dettagli aggiuntivi. |Richiedere un nuovo token dal server di autorizzazione hello. Se il nuovo token di hello non riesce, si è verificato un errore imprevisto. Invio di un utente toohello messaggio di errore e riprovare dopo ritardi casuali. |
| 403 |insufficient_scope |token di accesso Hello non contiene hello rappresentazione delle autorizzazioni necessarie tooaccess hello risorsa. |Inviare un nuovo endpoint di autorizzazione toohello richiesta autorizzazione. Se la risposta hello contiene il parametro di ambito hello, utilizzare il valore di ambito hello nella risorsa di toohello richiesta hello. |
| 403 |insufficient_access |oggetto Hello del token di hello non dispone di autorizzazioni hello che sono necessari tooaccess hello risorsa. |Hello prompt utente toouse un account diverso o toorequest autorizzazioni toohello risorsa specificata. |

## Aggiornamento dei token di accesso hello
I token di accesso sono di breve durati e devono essere aggiornati dopo la scadenza toocontinue l'accesso alle risorse. È possibile aggiornare hello `access_token` inviando un'altra `POST` richiesta toohello `/token` endpoint, ma questa volta fornendo hello `refresh_token` anziché hello `code`.

I token di aggiornamento non hanno una durata specificata. In genere, la durata di hello del token di aggiornamento è relativamente lunga. Tuttavia, in alcuni casi, i token di aggiornamento scadono, vengono revocati o dispongono di privilegi sufficienti per l'azione di hello desiderato. L'applicazione deve tooexpect e handle di errori restituiti dall'endpoint di rilascio dei token hello correttamente.

Quando si riceve una risposta con un errore di token di aggiornamento, eliminare il token di aggiornamento corrente hello e richiedere un nuovo codice di autorizzazione o token di accesso. In particolare, quando tramite un aggiornamento del token in hello del flusso di concessione del codice di autorizzazione, se si riceve una risposta con hello `interaction_required` o `invalid_grant` codici di errore, annullare il token di aggiornamento hello e richiedere un nuovo codice di autorizzazione.

Un toohello di richiesta di esempio **specifico del tenant** endpoint (è anche possibile usare hello **comuni** endpoint) tooget un nuovo token di accesso usando un token di aggiornamento è simile al seguente:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Risposta con esito positivo
Una risposta token con esito positivo ha un aspetto simile al seguente:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parametro | Descrizione |
| --- | --- |
| token_type |tipo di token Hello. è supportato solo Hello **connessione**. |
| expires_in |Hello rimanente durata del token di hello in secondi. Un valore tipico è 3600 (un'ora). |
| expires_on |Data di Hello e l'ora di scadenza del token hello. Data di Hello è rappresentata dal numero di hello di secondi da 1970-01-01T0:0:0Z UTC fino a ora di scadenza hello. |
| resource |Identifica hello risorsa protetta il token di accesso hello può essere utilizzato tooaccess. |
| scope |Applicazione client nativa toohello di concedere le autorizzazioni di rappresentazione. autorizzazione predefinita Hello **user_impersonation**. il proprietario di Hello della risorsa di destinazione hello può registrare valori alternativi in Azure AD. |
| access_token |Hello nuovo token di accesso che è stato richiesto. |
| refresh_token |Un aggiornamento OAuth 2.0 che possono essere utilizzati toorequest nuovi token di accesso quando scade hello nella risposta. |

### Risposta di errore
Una risposta di errore di esempio può avere un aspetto simile al seguente:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
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
