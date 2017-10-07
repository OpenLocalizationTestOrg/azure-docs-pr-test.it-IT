---
title: aaaLearn sulle hello token diverso e Azure AD supportati i tipi di attestazione | Documenti Microsoft
description: Una Guida per la comprensione e valutazione delle attestazioni hello in hello SAML 2.0 e i token JSON Web token (JWT) rilasciati da Azure Active Directory (AAD)
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Riferimento al token di Azure AD
Azure Active Directory (Azure AD) genera tipi diversi di token di sicurezza durante l'elaborazione di hello di ogni flusso di autenticazione. Questo documento descrive il formato di hello, caratteristiche di sicurezza e contenuto di ogni tipo di token.

## <a name="types-of-tokens"></a>Tipi di token
Azure AD supporta hello [protocollo di autorizzazione OAuth 2.0](active-directory-protocols-oauth-code.md), che si avvale di access_tokens e refresh_tokens.  Supporta inoltre l'autenticazione e accesso tramite [OpenID Connect](active-directory-protocols-openid-connect-code.md), cui è stato introdotto un terzo tipo di token, id_token hello.  Ognuno di questi token viene rappresentato come "token di connessione".

Un token di connessione è una risorsa protetta un token di sicurezza leggero che concede hello tooa accesso "bearer". In questo senso, hello "bearer" è qualsiasi entità che possono presentare token hello. Anche se è necessaria l'autenticazione con Azure AD in ordine tooreceive un token di connessione, effettuare i passaggi intercettazione di tooprevent toosecure hello token, da parti non autorizzate. I token di connessione non dispone di parti di tooprevent non autorizzato un meccanismo integrato di usarli, essi devono essere trasportati in un canale protetto, ad esempio transport level security (HTTPS). Se un token viene trasmesso in crittografato hello, un attacco man-in hello può essere token hello tooacquire utilizzato e ottenere risorse tooa protetto da accessi non autorizzati. Hello stessi principi di sicurezza si applicano quando l'archiviazione o la memorizzazione nella cache i token di connessione per un uso successivo. Assicurarsi sempre che l'app trasmetta e archivi i token di connessione in modo sicuro. Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [sezione 5 della specifica RFC 6750](http://tools.ietf.org/html/rfc6750).

Molte di hello token rilasciati da Azure AD vengono implementate come token Web JSON o Jwt.  Un token JWT è un modo compatto e indipendente dall'URL di trasferimento delle informazioni tra due parti.  informazioni di Hello in Jwt sono noti come "attestazioni", o asserzioni di informazioni sulla connessione hello e l'oggetto del token hello.  le attestazioni di Hello in Jwt sono oggetti JSON codificati e serializzati per la trasmissione.  Poiché hello Jwt rilasciati da Azure AD sono firmati, ma non crittografato, è possibile controllare facilmente il contenuto di hello di un token JWT a scopo di debug.  Sono disponibili diversi strumenti per questa operazione, ad esempio [jwt.calebb.net](http://jwt.calebb.net). Per ulteriori informazioni su Jwt, è possibile fare riferimento toohello [specifica JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Token ID
I token ID sono un tipo di token di sicurezza di accesso che l'app riceve quando esegue l'autenticazione usando [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Vengono rappresentati come [Jwt](#types-of-tokens)e contiene le attestazioni che è possibile utilizzare per la firma utente hello nell'app.  È possibile utilizzare le attestazioni hello in un id_token come desiderato, in genere vengono utilizzati per la visualizzazione di informazioni dell'account o per prendere decisioni di controllo di accesso in un'applicazione.

Attualmente i token ID sono firmati, ma non crittografati.  Quando l'applicazione riceve un id_token, deve [convalidare la firma hello](#validating-tokens) tooprove hello autenticità del token e convalidare alcuni le attestazioni in token tooprove di hello la validità.  Hello attestazioni convalidate da un'app variano a seconda dei requisiti di scenario, ma esistono alcune [convalide attestazione comuni](#validating-tokens) che l'app deve eseguire in ogni scenario.

Vedere la seguente sezione per informazioni su attestazioni id_tokens, nonché un id_token esempio hello.  Si noti che le attestazioni hello in id_tokens non vengono restituite in un ordine particolare.  Inoltre, nei token ID è possibile introdurre nuove attestazioni in qualsiasi momento. L'app non deve interrompersi quando vengono introdotte nuove attestazioni.  Hello elenco seguente include le attestazioni hello in modo affidabile in grado di interpretare l'app in fase di hello della redazione del presente documento.  Se necessario, ancora più dettagliate, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Token ID di esempio
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Per procedure consigliate, provare a controllo attestazioni hello nella richiesta id_token esempio hello incollandoli in [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Attestazioni nei token ID
> [!div class="mx-codeBreakAll"]
| Attestazione JWT | Nome | Descrizione |
| --- | --- | --- |
| `appid` |ID applicazione |Identifica un'applicazione hello che utilizza hello token tooaccess una risorsa. un'applicazione Hello può agire autonomamente o per conto dell'utente. ID dell'applicazione Hello in genere rappresenta un oggetto applicazione, ma può anche rappresentare un oggetto entità servizio in Azure AD. <br><br> **Valore token JWT di esempio**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Audience |Hello destinatario del token hello. un'applicazione Hello che riceve il token hello è necessario verificare che il valore di destinatari hello sia corretto e rifiutare eventuali token specifici per destinatari diversi. <br><br> **Valore SAML di esempio**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Valore token JWT di esempio**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Riferimento alla classe contesto di autenticazione applicazione |Indica la modalità di autenticazione client hello. Per un client pubblico, il valore di hello è 0. Se vengono utilizzati l'ID client e il segreto client, il valore di hello è 1. <br><br> **Valore token JWT di esempio**: <br> `"appidacr": "0"` |
| `acr` |Riferimento alla classe contesto di autenticazione |Indica come è stato autenticato soggetto hello client toohello anziché nell'attestazione riferimento alla classe contesto di autenticazione applicazione hello. Il valore "0" indica l'autenticazione dell'utente finale di hello non soddisfa i requisiti di hello di ISO/IEC 29115. <br><br> **Valore token JWT di esempio**: <br> `"acr": "0"` |
| Istante di autenticazione |Record hello data e ora quando si è verificato durante l'autenticazione. <br><br> **Valore SAML di esempio**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Metodo di autenticazione |Identifica la modalità di autenticazione soggetto hello del token hello. <br><br> **Valore SAML di esempio**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Valore token JWT di esempio**: `“amr”: ["pwd"]` |
| `given_name` |Nome |Fornisce hello prima o "nome dell'utente di hello, Data" come impostato sull'oggetto utente hello Azure AD. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"given_name": "Frank"` |
| `groups` |Gruppi |Fornisce l'ID di oggetti che rappresentano appartenenze hello dell'oggetto. Questi valori sono univoci (vedere l'ID di oggetto) e possono essere utilizzati in modo sicuro per la gestione dell'accesso, ad esempio autorizzazione tooaccess una risorsa. gruppi di Hello inclusi nell'attestazione gruppi hello sono configurati in base all'applicazione, tramite proprietà "groupMembershipClaims" hello del manifesto dell'applicazione hello. Un valore null escluderà tutti i gruppi, un valore "SecurityGroup" includerà solo le appartenenze al gruppo di sicurezza di Active Directory e un valore "All" includerà sia i gruppi di sicurezza che le liste di distribuzione di Office 365. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Provider di identità |Record hello provider di identità che ha autenticato hello oggetto del token hello. Questo valore è identico toohello di hello dell'autorità di certificazione di attestazioni, a meno che l'account utente di hello è in un tenant diverso rispetto dell'autorità di certificazione hello. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Archivia l'ora di hello in cui hello token è stato rilasciato. È spesso utilizzato toomeasure validità del token. <br><br> **Valore SAML di esempio**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Valore token JWT di esempio**: <br> `"iat": 1390234181` |
| `iss` |Issuer |Identifica hello servizio token di sicurezza (STS) che crea e restituisce il token hello. Nei token hello restituiti da Azure AD, autorità emittente di hello è sts.windows.net. Hello GUID nel valore dell'attestazione autorità di certificazione hello è hello ID tenant di directory di Azure AD hello. ID tenant Hello è un identificatore non modificabile e attendibile della directory hello. <br><br> **Valore SAML di esempio**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Valore token JWT di esempio**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Cognome |Fornisce il cognome di hello, cognome o cognome dell'utente di hello come definito nell'oggetto utente di Azure AD hello. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"family_name": "Miller"` |
| `unique_name` |Nome |Fornisce un valore leggibile umano che identifica l'oggetto hello del token hello. Questo valore non è garantito toobe univoco all'interno di un tenant ed è progettato toobe usato solo per scopi di visualizzazione. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |ID oggetto |Contiene un identificatore univoco di un oggetto in Azure AD. Questo valore non è modificabile e non può essere riassegnato o riutilizzato. Utilizzare tooidentify ID di oggetto hello oggetto tooAzure query Active Directory. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Ruoli |Rappresenta tutti i ruoli applicazione hello soggetto è stata concessa direttamente e indirettamente tramite l'appartenenza al gruppo e può essere utilizzato tooenforce basata sui ruoli di controllo di accesso. Ruoli applicazione sono definiti in base all'applicazione, tramite hello `appRoles` proprietà del manifesto dell'applicazione hello. Hello `value` proprietà di ogni ruolo applicazione è valore hello visualizzato nell'attestazione ruoli hello. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Scope |Indica la rappresentazione delle autorizzazioni concesse toohello client applicazione hello. autorizzazione predefinita Hello `user_impersonation`. il proprietario di Hello di hello risorsa protetta può registrare valori aggiuntivi in Azure AD. <br><br> **Valore token JWT di esempio**: <br> `"scp": "user_impersonation"` |
| `sub` |Oggetto |Identifica l'entità hello sui quali hello token rilascia informazioni, ad esempio utente hello di un'applicazione. Questo valore non è modificabile e non può essere riassegnato o riutilizzato, in modo che siano utilizzati tooperform controlli di autorizzazione in modo sicuro. Poiché l'oggetto hello è sempre presente in hello i token rilasciati da Azure AD hello, si consiglia di utilizzare questo valore in un sistema di autorizzazione generale. <br> `SubjectConfirmation` non è un'attestazione. Descrive la modalità di verifica soggetto hello del token hello. `Bearer`indica che tale oggetto hello viene confermato tramite il possesso del token hello. <br><br> **Valore SAML di esempio**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Valore token JWT di esempio**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |ID tenant |Un identificatore non modificabile e non riutilizzabile che identifica i tenant di directory hello che ha emesso il token hello. È possibile utilizzare le risorse di directory specifico del tenant tooaccess questo valore in un'applicazione multi-tenant. Ad esempio, è possibile utilizzare questo tenant di valore tooidentify hello in toohello una chiamata API Graph. <br><br> **Valore SAML di esempio**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Valore token JWT di esempio**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Durata del token |Definisce l'intervallo di tempo hello entro il quale un token è valido. servizio Hello che convalida il token hello è necessario verificare che hello data corrente è all'interno di hello durata del token, else che dovrebbe rifiutare il token hello. Hello servizio potrebbe consentire di toofive minuti oltre tooaccount intervallo di durata del token hello eventuali differenze di orario ("sfasamento") tra Azure AD e servizio hello. <br><br> **Valore SAML di esempio**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Valore token JWT di esempio**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Nome dell'entità utente |Archivi hello nome utente dell'entità utente hello.<br><br> **Valore token JWT di esempio**: <br> `"upn": frankm@contoso.com` |
| `ver` |Versione |Archivia il numero di versione hello del token hello. <br><br> **Valore token JWT di esempio**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Token di accesso
Quando l'autenticazione ha esito positivo, Azure AD restituisce un token di accesso, può essere utilizzati tooaccess protetto risorse. token di accesso Hello è una base 64 codificata JSON Web Token (JWT) e il relativo contenuto può essere esaminato eseguendolo mediante un decodificatore.

Se l'app solo *Usa* tooget accesso tooAPIs token di accesso, è possibile (e consigliabile) trattare i token di accesso come completamente opaco - sono semplici stringhe che propria app possa superare tooresources nelle richieste HTTP.

Quando si richiede un token di accesso, Azure AD restituisce anche alcuni metadati relativi token di accesso di hello per l'utilizzo dell'app.  Queste informazioni includono ora di scadenza hello di token di accesso hello e ambiti di hello per le quali è valido.  In questo modo intelligente la memorizzazione nella cache dei token di accesso senza aprire hello i token di accesso stesso tooparse tooperform l'app.

Se l'app è un'API protetta con Azure AD che si prevede che i token di accesso in richieste HTTP, è consigliabile eseguire la convalida e l'ispezione dei token hello che viene visualizzato. L'app deve eseguire la convalida del token di accesso hello prima di utilizzare le risorse tooaccess. Per altre informazioni sulla convalida, vedere [Convalida dei token](#validating-tokens).  
Per informazioni dettagliate su come toodo con .NET, vedere [proteggere un'API Web tramite i token di connessione da Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Token di aggiornamento

Aggiornare i token sono token di sicurezza, che è possibile usare l'app tooacquire accedere nuovi token in un flusso OAuth 2.0.  Consente l'app tooachieve a lungo termine accesso tooresources per conto dell'utente senza interazione utente hello.

Si tratta di token a più risorse,  Ovvero toosay che ha ricevuto un token di aggiornamento durante una richiesta di token per una risorsa può essere riscattata per tooa completamente diverse risorse di token di accesso. toodo, hello set `resource` parametro hello richiesta toohello risorse di destinazione.

I token di aggiornamento sono completamente opachi tooyour app. Sono di lunga durate, ma l'app non deve essere scritto tooexpect che durata un token di aggiornamento per qualsiasi periodo di tempo.  I token di aggiornamento possono essere annullati in qualsiasi momento per vari motivi.  Hello solo per i tooknow app se è valido un token di aggiornamento è tooattempt tooredeem, rendendo l'endpoint del token tooAzure AD una richiesta di token.

Quando si Riscatta un token di aggiornamento di un nuovo token di accesso, si riceverà un nuovo token di aggiornamento in risposta token hello.  È consigliabile salvare il token di aggiornamento hello appena emesso, sostituendo hello usato nella richiesta di hello.  In questo modo, il token di aggiornamento rimarrà valido più a lungo possibile.

## <a name="validating-tokens"></a>Convalida dei token

In ordine toovalidate id_token o access_token, l'applicazione deve convalidare le attestazioni hello e di firma del token entrambi hello. Nei token di accesso toovalidate ordine, l'app deve convalidare anche dell'autorità di certificazione hello, destinatari hello e hello la firma di token. Questi devono toobe convalidato in base a valori hello nel documento di individuazione OpenID hello. Ad esempio, hello tenant indipendente dalla versione documento hello si trova in [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Middleware di Azure AD include funzionalità predefinite per la convalida i token di accesso e che è possibile esplorare il nostro [esempi](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind language hello di propria scelta. Per ulteriori informazioni su come tooexplicitly convalidare un token JWT, vedere hello [manuali dell'esempio convalida JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Vengono forniti esempi di codice che illustrano come tooeasily gestiscono la convalida dei token - e librerie hello sotto informazioni semplicemente viene fornito per coloro che desiderano hello toounderstand processo sottostante.  Sono disponibili anche numerose librerie open source di terze parti per la convalida dei token JWT. Esiste almeno un'opzione per ogni piattaforma e linguaggio disponibili. Per altre informazioni sulle librerie di autenticazione di Azure AD e per ottenere esempi di codice, vedere [Azure Active Directory Authentication Library](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>La convalida della firma hello

Un token JWT contiene tre segmenti, separati da hello `.` carattere.  primo segmento Hello è noto come hello **intestazione**, hello secondo come hello **corpo**, hello terzo come hello e **firma**.  segmento di firma Hello può essere utilizzato toovalidate hello autenticità del token hello in modo che possono essere considerati attendibili dall'app.

I token emessi da Azure AD vengono firmati usando algoritmi di crittografia asimmetrica standard del settore, come RSA 256. intestazione Hello di hello JWT contiene informazioni sulla chiave di hello e metodo di crittografia utilizzato token hello toosign:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Hello `alg` attestazione indica l'algoritmo hello che era token hello toosign usato durante hello `x5t` attestazione indica hello particolare chiave pubblica che è stata token hello toosign utilizzato.

In qualsiasi momento, Azure AD può firmare un token ID usando un determinato set di coppie di chiavi pubbliche/private. Azure AD ruota i set di possibili hello di chiavi con cadenza periodica, in modo che l'app deve essere scritto toohandle tali chiave viene modificata automaticamente.  Toocheck una frequenza ragionevole per gli aggiornamenti toohello le chiavi pubbliche usate da Azure Active Directory è di 24 ore.

È possibile acquisire hello firma hello toovalidate necessarie di dati della chiave di firma utilizzando hello OpenID Connect documento dei metadati si trova in:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Provare questo URL in un browser.
> 
> 

Questo documento di metadati è un oggetto JSON contenente diverse parti utile di informazioni, ad esempio percorso hello di hello vari endpoint necessari per eseguire l'autenticazione OpenID Connect.  

Include inoltre un `jwks_uri`, che offre una posizione di hello di hello set di chiavi pubbliche utilizzate toosign token.  documento JSON Hello disponibile all'indirizzo hello `jwks_uri` contiene le informazioni sulla chiave pubblica hello in uso in quel momento specifico nel tempo.  L'app è possibile utilizzare hello `kid` di attestazione in hello JWT intestazione tooselect la chiave pubblica in questo documento è stato utilizzato toosign il token.  Quindi possibile eseguire la convalida della firma con chiave pubblica corretta hello e l'algoritmo indicato hello.

Eseguire la convalida della firma è di fuori ambito hello del presente documento, sono disponibili molte librerie open source che aiuta a tale scopo, se necessario.

#### <a name="validating-hello-claims"></a>Convalida delle attestazioni hello

Quando l'applicazione riceve un token (un id_token all'account utente o un token di accesso come un token di connessione nella richiesta HTTP hello) deve anche eseguire alcuni controlli hello attestazioni nel token hello.  Sono incluse, ad esempio:

* Hello **destinatari** attestazione - tooverify che hello token è stato previsto toobe tooyour app specificato.
* Hello **non prima** e **scadenza** attestazioni - tooverify che hello token non sia scaduto.
* Hello **dell'autorità di certificazione** attestazione - tooverify che hello token è stato emesso effettivamente app tooyour da Azure AD.
* Hello **Nonce** -toomitigate attacchi di tipo replay di token.
* E altro ancora...

Per un elenco completo delle app deve eseguire per i token ID convalide di attestazione, vedere toohello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). I dettagli dei valori previsti hello per le attestazioni sono inclusi in hello precedente [id_token sezione](#id-tokens) sezione.

## <a name="sample-tokens"></a>Token di esempio

Questa sezione consente di visualizzare esempi di token SAML e JWT restituiti da Azure AD. Questi esempi consentono di visualizzare hello attestazioni nel contesto.

### <a name="saml-token"></a>Token SAML

Questo è un esempio di un tipico token SAML.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Token JWT: rappresentazione dell'utente
Questo è un esempio di un tipico token JSON Web (JWT) usato in un flusso di concessione del codice di autorizzazione.
In aggiunta tooclaims, token hello include un numero di versione in **ver** e **appidacr**, hello autenticazione riferimento alla classe contesto, che indica la modalità di autenticazione client hello. Per un client pubblico, il valore di hello è 0. Se è stato utilizzato un ID client o un segreto client, il valore di hello è 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Contenuti correlati
* Vedere hello Azure AD Graph [operazioni di criteri](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) hello e [entità criteri](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn ulteriori informazioni sulla gestione dei criteri di durata del token tramite hello API Azure AD Graph.
* Per altre informazioni ed esempi sulla gestione dei criteri tramite i cmdlet PowerShell, vedere [Configurable token lifetimes in Azure AD](../active-directory-configurable-token-lifetimes.md) (Durata dei token configurabile in Azure AD). 
