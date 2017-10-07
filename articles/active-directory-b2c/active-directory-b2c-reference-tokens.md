---
title: 'Azure Active Directory B2C: Riferimento token | Documentazione Microsoft'
description: tipi di Hello del token emesso in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: informazioni di riferimento sui token
Azure Active Directory B2C (Azure AD B2C) rilascia tipi diversi di token di sicurezza durante l'elaborazione di ogni [flusso di autenticazione](active-directory-b2c-apps.md). Questo documento descrive il formato di hello, caratteristiche di sicurezza e contenuto di ogni tipo di token.

## <a name="types-of-tokens"></a>Tipi di token
Azure Active Directory B2C supporta hello [protocollo di autorizzazione OAuth 2.0](active-directory-b2c-reference-protocols.md), che si avvale di entrambi i token di accesso e token di aggiornamento. Supporta inoltre l'autenticazione e accesso tramite [OpenID Connect](active-directory-b2c-reference-protocols.md), cui è stato introdotto un terzo tipo di token: token ID hello. Ognuno di questi token viene rappresentato come token di connessione.

Un token di connessione è una risorsa protetta un token di sicurezza leggero che concede hello tooa accesso "bearer". connessione Hello è qualsiasi entità che possono presentare token hello. Per poter ricevere un token di connessione, Azure AD deve prima autenticare una parte. Tuttavia, se il token hello toosecure durante la trasmissione e di archiviazione non vengono eseguite operazioni hello necessario può essere intercettato e usato da parti non autorizzate. Alcuni token di sicurezza hanno un meccanismo predefinito che ne impedisce l'uso da parti non autorizzate, ma i token di connessione non presentano questo meccanismo. Devono essere trasportati usando un canale protetto, ad esempio il protocollo Transport Layer Security (HTTPS).

Se un token viene trasmesso all'esterno di un canale sicuro, un malintenzionato può usare un token di hello tooacquire attacco man-in-the-middle e usarlo risorsa tooa protetto di accesso toogain non autorizzato. Hello stessi principi di sicurezza si applicano quando i token di connessione vengono archiviati o memorizzate nella cache per un uso successivo. Assicurarsi sempre che l'app trasmetta e archivi i token di connessione in modo sicuro.

Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Molti dei token di hello Azure Active Directory B2C rilasciati da vengono implementati come token web JSON (Jwt). Un token JWT è un modo compatto e indipendente dall'URL di trasferimento delle informazioni tra due parti. I token JWT contengono informazioni note come attestazioni. Si tratta di asserzioni di informazioni sulla connessione hello e l'oggetto di hello del token hello. le attestazioni di Hello in Jwt sono oggetti JSON che sono codificati e serializzati per la trasmissione. Poiché è firmato ma non crittografato hello Jwt emesso da Azure Active Directory B2C, è possibile controllare facilmente il contenuto di hello di toodebug un JWT è. Sono disponibili diversi strumenti adatti a questo scopo, ad esempio [calebb.net](http://calebb.net). Per ulteriori informazioni su Jwt, vedere troppo[specifiche JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Token ID
Un token ID è un tipo di token di sicurezza che l'applicazione riceve da Azure AD B2C hello `authorize` e `token` gli endpoint. Token ID vengono rappresentati come [Jwt](#types-of-tokens), e che contengano le attestazioni che è possibile utilizzare gli utenti tooidentify nell'app. Quando i token di ID vengono acquisiti da hello `authorize` endpoint, sono spesso toosign usati nelle applicazioni tooweb gli utenti. Quando i token di ID vengono acquisiti da hello `token` endpoint, e possono essere inviati nelle richieste HTTP durante la comunicazione tra due componenti di hello stessa applicazione o servizio. È possibile utilizzare le attestazioni hello in un ID token nel modo desiderato. Sono comunemente usate toodisplay account informazioni o toomake accesso decisioni relative al controllo in un'applicazione.  

Attualmente i token ID sono firmati, ma non crittografati. Quando l'app o l'API riceve un ID token, è necessario [convalidare la firma hello](#token-validation) tooprove che hello token è autentica. L'app o l'API inoltre necessario convalidare alcuni attestazioni in tooprove di hello token è valido. A seconda dei requisiti di scenario hello, attestazioni hello convalidate da un'app possono variare, ma l'app deve eseguire alcune [convalide attestazione comuni](#token-validation) in ogni scenario.

#### <a name="sample-id-token"></a>Token ID di esempio
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Token di accesso
Un token di accesso è anche un tipo di token di sicurezza che l'applicazione riceve da Azure AD B2C hello `authorize` e `token` gli endpoint. I token di accesso sono rappresentati anche come [Jwt](#types-of-tokens), e che contengano le attestazioni che è possibile utilizzare hello tooidentify concessa autorizzazioni tooyour API. Attualmente i token di accesso sono firmati, ma non crittografati. I token di accesso devono essere server di accesso utilizzato tooprovide tooAPIs e risorse. Per ulteriori informazioni su troppo[utilizzare i token di accesso](active-directory-b2c-access-tokens.md). 

Quando l'API riceve un token di accesso, è necessario [convalidare la firma hello](#token-validation) tooprove che hello token è autentica. L'API è inoltre necessario convalidare alcuni attestazioni in tooprove di hello token è valido. A seconda dei requisiti di scenario hello, attestazioni hello convalidate da un'app possono variare, ma l'app deve eseguire alcune [convalide attestazione comuni](#token-validation) in ogni scenario.

### <a name="claims-in-id-and-access-tokens"></a>Attestazioni nei token di accesso e ID
Quando si usa Azure Active Directory B2C, si dispone di un controllo accurato sul contenuto hello dei token. È possibile configurare [criteri](active-directory-b2c-reference-policies.md) toosend determinati set di dati utente nelle attestazioni che richiede l'app per le relative operazioni. Queste attestazioni possono includere proprietà standard, ad esempio utente hello `displayName` e `emailAddress`. Possono includere anche [attributi utente personalizzati](active-directory-b2c-reference-custom-attr.md) che è possibile definire nella directory B2C. Ogni token ID e di accesso ricevuto contiene un determinato set di attestazioni relative alla sicurezza. Le applicazioni possono utilizzare queste attestazioni toosecurely autenticare gli utenti e richieste.

Si noti che hello attestazioni nei token ID non vengono restituite in un ordine particolare. Si noti anche che possono essere introdotte nuove attestazioni nei token ID in qualsiasi momento. L'introduzione delle nuove attestazioni non deve interrompere il funzionamento dell'app. Di seguito sono hello attestazioni che si prevede tooexist ID e token di accesso rilasciato da Azure Active Directory B2C. Eventuali attestazioni aggiuntive sono determinate dai criteri. Per procedure consigliate, provare a controllo hello attestazioni nel token di ID di esempio hello incollandoli in [calebb.net](http://calebb.net). Ulteriori informazioni, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html).

| Nome | Attestazione | Valore di esempio | Descrizione |
| --- | --- | --- | --- |
| Audience |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Un'attestazione destinatari identifica destinatario previsto hello del token hello. Per Azure Active Directory B2C, destinatari hello sono ID applicazione dell'app come app tooyour assegnato nel portale di registrazione applicazione hello. L'app deve convalidare questo valore e rifiutare il token di hello se non corrispondono. |
| Issuer |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Questa attestazione identifica hello servizio token di sicurezza (STS) che crea e restituisce il token hello. Vengono inoltre identificati directory di Azure AD hello in cui hello è stato autenticato l'utente. L'app deve convalidare l'attestazione autorità di certificazione hello tooensure che hello token provenienza hello Azure v 2.0 endpoint di Active Directory. |
| Ora di emissione |`iat` |`1438535543` |Questa attestazione è hello ora in cui hello token è stato inviato, rappresentato in valore epoch. |
| Scadenza |`exp` |`1438539443` |Hello attestazione ora di scadenza è hello tempo in cui hello token diventa non valido, rappresentato in valore epoch. L'app deve usare la validità di hello tooverify attestazione della durata del token hello. |
| Non prima |`nbf` |`1438535543` |Questa attestazione è ora di hello in cui hello token diventa valido, rappresentato in valore epoch. Questo è in genere hello stesso come hello ora hello token è stato rilasciato. L'app deve usare la validità di hello tooverify attestazione della durata del token hello. |
| Versione |`ver` |`1.0` |Si tratta di versione di hello del token ID hello, come definito da Azure AD. |
| Hash del codice |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hash di codice è incluso in un ID token solo quando viene rilasciato il token di hello insieme a un codice di autorizzazione OAuth 2.0. Un hash di codice può essere utilizzato toovalidate hello autenticità di un codice di autorizzazione. Per ulteriori informazioni su come tooperform questa convalida, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html).  |
| Hash del token di accesso |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hash di token di accesso è incluso in un ID token solo quando viene rilasciato il token di hello insieme a un token di accesso OAuth 2.0. Un hash di token di accesso può essere utilizzato toovalidate hello autenticità di un token di accesso. Per ulteriori informazioni su come tooperform questa convalida, vedere hello [specifica OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Nonce |`nonce` |`12345` |Un nonce è che usare una strategia di attacchi di riproduzione token toomitigate. L'app può specificare un parametro nonce in una richiesta di autorizzazione con hello `nonce` parametro di query. il valore di Hello fornito nella richiesta di hello verrà creato senza modificarli in hello `nonce` di un solo ID token di attestazione. In questo modo il valore di hello app tooverify con valore hello che è specificato in una richiesta di hello, che associa la sessione dell'applicazione hello con un token ID specificato. L'app deve eseguire la convalida durante il processo di convalida del token ID hello. |
| Oggetto |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Si tratta di entità hello sui quali hello token rilascia informazioni, ad esempio utente hello di un'app. Questo valore non è modificabile e non può essere riassegnato o riutilizzato. Controlli di autorizzazione tooperform utilizzato in modo sicuro, può essere ad esempio quando il token hello viene utilizzato tooaccess una risorsa. Per impostazione predefinita, hello soggetto attestazione viene popolata con ID di oggetto hello di utente hello nella directory di hello. vedere, più toolearn [Azure Active Directory B2C: Token di sessione e configurazione di single sign-on](active-directory-b2c-token-session-sso.md). |
| Riferimento alla classe contesto di autenticazione |`acr` |Non applicabile |Non in uso, tranne che in caso di hello dei criteri precedenti. vedere, più toolearn [Azure Active Directory B2C: Token di sessione e configurazione di single sign-on](active-directory-b2c-token-session-sso.md). |
| Criteri del framework di attendibilità |`tfp` |`b2c_1_sign_in` |Questo è il nome di hello di criteri hello tooacquire utilizzati token di ID hello. |
| Ora di autenticazione |`auth_time` |`1438535543` |Questa attestazione è hello ora in cui un ultimo immesso le credenziali utente, in forma di valore epoch. |

### <a name="refresh-tokens"></a>Token di aggiornamento
Aggiornare i token sono token di sicurezza per l'app può utilizzare tooacquire nuovi token di ID e i token in un flusso OAuth 2.0 di accesso. Forniscono l'app con tooresources accesso a lungo termine per conto degli utenti senza interazione con gli utenti.

tooreceive un token di aggiornamento in una risposta di token, l'applicazione deve richiedere hello `offline_acesss` ambito. altre informazioni sulle hello toolearn `offline_access` ambito, fare riferimento toohello [riferimento al protocollo Azure Active Directory B2C](active-directory-b2c-reference-protocols.md).

Token di aggiornamento sono e sarà sempre, app tooyour completamente opaco. Vengono rilasciati da Azure AD e possono essere controllati e interpretati solo da Azure AD. Sono di lunga durate, ma l'app non deve essere scritto previsione hello che durata un token di aggiornamento per un periodo di tempo specifico. I token di aggiornamento possono essere annullati in qualsiasi momento per vari motivi. Hello solo per i tooknow app se è valido un token di aggiornamento è tooattempt tooredeem, rendendo tooAzure una richiesta di token Active Directory.

Quando si Riscatta un token di aggiornamento di un nuovo token (e se l'app è stata concessa hello `offline_access` ambito), si riceverà un nuovo token di aggiornamento in risposta token hello. È consigliabile salvare il token di aggiornamento hello appena rilasciato. È necessario sostituire i token di aggiornamento hello che è utilizzato in precedenza nella richiesta di hello. In questo modo, il token di aggiornamento rimarrà valido il più a lungo possibile.

## <a name="token-validation"></a>Convalida dei token
toovalidate un token, l'applicazione deve controllare firma hello e attestazioni del token hello.

Sono disponibili molte librerie open source per la convalida dei token JWT, a seconda del linguaggio preferito. È consigliabile prendere in esame tali opzioni anziché implementare una logica di convalida personalizzata. informazioni di Hello in questa guida consentono di scoprire come tooproperly utilizzare tali raccolte.

### <a name="validate-hello-signature"></a>Convalidare la firma hello
Un token JWT contiene tre segmenti, separati da hello `.` carattere. il primo segmento Hello è hello *intestazione*, hello in secondo luogo è hello *corpo*, il terzo, hello è hello *firma*. segmento di firma Hello può essere utilizzato toovalidate hello autenticità del token hello in modo che possono essere considerati attendibili dall'app.

I token Azure AD B2C vengono firmati usando algoritmi di crittografia asimmetrica standard del settore, come RSA 256. intestazione Hello del token hello contiene informazioni sulla chiave di hello e metodo di crittografia utilizzato token hello toosign:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Hello `alg` attestazione indica l'algoritmo hello non utilizzati toosign hello token. Hello `kid` attestazione indica hello particolare chiave pubblica che è stata token hello toosign utilizzato.

In qualsiasi momento Azure AD può firmare un token usando un determinato set di coppie di chiavi pubblica/privata. Azure AD ruota periodicamente, i set di possibili hello di chiavi in modo che l'app deve essere scritto toohandle tali chiave viene modificata automaticamente. Toocheck una frequenza ragionevole per gli aggiornamenti toohello le chiavi pubbliche usate da Azure Active Directory è di 24 ore.

Azure AD B2C include un endpoint dei metadati di OpenID Connect. Questo consente alle App toofetch informazioni su Azure Active Directory B2C in fase di esecuzione. Queste informazioni includono endpoint, contenuti del token e chiavi per la firma dei token. La directory B2C contiene un documento metadati JSON per ogni criterio. Ad esempio, hello documento di metadati per hello `b2c_1_sign_in` criteri in `fabrikamb2c.onmicrosoft.com` si trova in:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`è una directory B2C hello utilizzato tooauthenticate hello, e `b2c_1_sign_in` è token hello tooacquire utilizzati i criteri di hello. toodetermine quali criteri è stato utilizzato toosign un token (e in cui toogo toofetch hello metadati), sono disponibili due opzioni. In primo luogo, il nome di criterio hello è incluso in hello `acr` attestazione nel token hello. È possibile analizzare le attestazioni dal corpo hello di hello JWT dal corpo hello decodifica Base64 e la deserializzazione di hello che causa di stringa JSON. Hello `acr` attestazione corrisponderà al nome hello di criteri hello token hello tooissue utilizzato.  L'altra opzione è criteri hello tooencode valore hello hello `state` parametro quando si invia la richiesta hello e decodificarlo in toodetermine quali criteri è stato utilizzato. Entrambi i metodi sono validi.

documento di metadati Hello è un oggetto JSON che contiene numerose utile di informazioni. Questi includono il percorso di hello del hello gli endpoint necessari tooperform autenticazione OpenID Connect. È inoltre incluso `jwks_uri`, che offre una posizione di hello di hello set di chiavi pubbliche che sono utilizzati toosign token. Tale percorso viene fornito di seguito, ma è percorso migliore di hello toofetch dinamicamente utilizzando il documento di metadati hello e l'analisi di `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

documento JSON Hello si trova in corrispondenza dell'URL contiene tutte le informazioni di chiave pubblica hello in uso in un determinato momento. L'app è possibile utilizzare hello `kid` di attestazione in hello JWT intestazione tooselect hello chiave pubblica nel documento JSON hello che viene utilizzato toosign il token. Quindi possibile eseguire la convalida della firma con chiave pubblica corretta hello e l'algoritmo indicato hello.

Una descrizione di come la convalida della firma tooperform è di fuori ambito hello di questo documento. Molte librerie open source sono toohelp disponibile con questa opzione se è necessario.

### <a name="validate-hello-claims"></a>Convalidare le attestazioni hello
Quando l'app o l'API riceve un token di ID, deve anche eseguire diversi controlli di base hello attestazioni nel token ID hello. Sono incluse, ad esempio:

* Hello **destinatari** attestazione: in questo modo si verifica tale token ID hello è stato previsto toobe tooyour app specificato.
* Hello **non prima** e **scadenza** attestazioni: questi verificare tale token ID hello è scaduto.
* Hello **dell'autorità di certificazione** attestazione: in questo modo si verifica tale token hello è stato rilasciato app tooyour da Azure AD.
* Hello **nonce**: si tratta di una strategia per l'attenuazione di attacchi di riproduzione token.

Per un elenco completo delle convalide deve eseguire l'app, vedere toohello [OpenID Connect specifica](https://openid.net). I dettagli dei valori previsti hello per le attestazioni sono inclusi in hello precedente [token sezione](#types-of-tokens).  

## <a name="token-lifetimes"></a>Durata dei token
Hello durata dei token di seguito è fornite toofurther la conoscenza. Queste informazioni possono risultare utili durante lo sviluppo e il debug delle app. Si noti che le app non devono essere scritto tooexpect uno di questi costante tooremain durate. La durata dei token può variare. Altre informazioni su hello [personalizzazione di durata dei token](active-directory-b2c-token-session-sso.md) in Azure Active Directory B2C.

| token | Durata | Descrizione |
| --- | --- | --- |
| Token ID |Un'ora |I token ID sono in genere validi per un'ora. L'app web è possibile utilizzare questo toomaintain durata proprie sessioni con gli utenti (scelta consigliati). È anche possibile scegliere una durata di sessione diversa. Se l'app deve tooget un nuovo token di ID, è soltanto necessario toomake un nuovo tooAzure richiesta di accesso Active Directory. Se un utente dispone di una sessione del browser valido con Azure AD, che l'utente potrebbe non essere le credenziali necessarie tooenter nuovamente. |
| Token di aggiornamento |Impostare i giorni too14 |Un singolo token di aggiornamento è valido per un periodo massimo di 14 giorni. Tuttavia, un token di aggiornamento potrebbe non essere più valido in qualsiasi momento per diversi motivi. L'app deve continuare tootry toouse un token di aggiornamento, fino a quando non si verifica un errore di richiesta di hello o fino a quando l'app sostituisce il token di aggiornamento hello con uno nuovo. Un token di aggiornamento può diventare anche in caso di 90 giorni trascorsi dall'utente hello ultima credenziali immesse. |
| Codici di autorizzazione |Cinque minuti |I codici di autorizzazione hanno intenzionalmente una breve durata. Alla ricezione devono essere riscattati immediatamente con token di accesso, token ID o token di aggiornamento. |

