---
title: versione 2.0 di Active Directory aaaAzure token riferimento | Documenti Microsoft
description: i tipi di Hello di attestazioni e token emessi da hello endpoint v 2.0 di Azure AD
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Informazioni di riferimento sui token di Azure Active Directory 2.0
endpoint di Azure Active Directory (Azure AD) v 2.0 Hello genera tipi diversi di token di sicurezza in ogni [flusso di autenticazione](active-directory-v2-flows.md). Questo riferimento viene formato hello, caratteristiche di sicurezza e di contenuto di ogni tipo di token.

> [!NOTE]
> endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità. toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Tipi di token
v 2.0 endpoint Hello supporta hello [protocollo di autorizzazione OAuth 2.0](active-directory-v2-protocols.md), che utilizza i token di accesso e token di aggiornamento. endpoint di Hello v 2.0 supporta inoltre l'autenticazione e accesso tramite [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect introduce un terzo tipo di token, token di ID hello. Ognuno di questi token viene rappresentato come *token di connessione*.

Un token di connessione è un token di sicurezza leggero che concede hello tooa accesso connessione risorsa protetta. connessione Hello è qualsiasi entità che possono presentare token hello. Anche se un'entità deve eseguire l'autenticazione con token di connessione di Azure AD tooreceive hello, se passaggi non vengono acquisiti i token hello toosecure durante la trasmissione e di archiviazione, può essere intercettato e usato da parti non autorizzate. Alcuni token di sicurezza presenti un entità di tooprevent non autorizzato meccanismo incorporato dall'utilizzo non li ma non i token di connessione. e devono essere trasportati usando un canale protetto, ad esempio il protocollo Transport Layer Security (HTTPS). Se un token viene trasmesso senza questo tipo di sicurezza, un malintenzionato potrebbe utilizzare un token di hello tooacquire "attacco man-in-the-middle" e usarlo per risorsa tooa protetto da accessi non autorizzati. Hello stessi principi di sicurezza si applicano quando l'archiviazione o la memorizzazione nella cache i token di connessione per un uso successivo. Assicurarsi sempre che l'app trasmetta e archivi i token di connessione in modo sicuro. Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [sezione 5 della specifica RFC 6750](http://tools.ietf.org/html/rfc6750).

Molti dei token hello rilasciati dall'endpoint v 2.0 hello vengono implementati come token Web JSON (Jwt). Un token JWT è un informazioni tootransfer modo compatto e URL safe tra due parti. informazioni di Hello in un token JWT viene chiamate un *attestazione*. È un'asserzione di informazioni sulla connessione hello e l'oggetto del token hello. le attestazioni di Hello in un JWT sono gli oggetti JavaScript Object Notation (JSON) con codifica e serializzati per la trasmissione. Poiché hello Jwt emesso da endpoint v 2.0 hello sono firmati, ma non crittografato, è possibile controllare facilmente il contenuto di hello di un token JWT per scopi di debug. Per ulteriori informazioni su Jwt, vedere hello [specifica JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Token ID
I token ID sono un tipo di token di sicurezza di accesso che l'app riceve quando esegue l'autenticazione usando [OpenID Connect](active-directory-v2-protocols.md). Token ID vengono rappresentati come [Jwt](#types-of-tokens), e che contengano le attestazioni che è possibile utilizzare utente hello toosign nell'app tooyour. È possibile utilizzare le attestazioni hello in un ID token in svariati modi. Gli amministratori utilizzano in genere, informazioni sull'account di ID token toodisplay o toomake decisioni relative al controllo accesso in un'applicazione. endpoint v 2.0 Hello emette un solo tipo di token ID, che dispone di un set coerenza di attestazioni, indipendentemente dal tipo di hello dell'utente che ha effettuato l'accesso. formato Hello e il contenuto di token ID sono hello uguale per gli utenti dell'account Microsoft personali e per gli account aziendali o dell'istituto di istruzione.

Attualmente i token ID sono firmati, ma non crittografati. Quando l'applicazione riceve un ID token, è necessario [convalidare la firma hello](#validating-tokens) tooprove hello autenticità del token e convalidare alcuni le attestazioni in token tooprove di hello la validità. Hello attestazioni convalidate da un'app variano a seconda dei requisiti di scenario, ma l'app deve eseguire alcune [convalide attestazione comuni](#validating-tokens) in ogni scenario.

Si consentono i dettagli completi hello attestazioni nei token ID hello seguenti sezioni inoltre token ID di esempio tooa. Si noti che le attestazioni nei token ID non vengono restituite in un ordine specifico. Si noti anche che possono essere introdotte nuove attestazioni nei token ID in qualsiasi momento. L'introduzione di nuove attestazioni non deve interrompere il funzionamento dell'app. Hello seguente elenco include le attestazioni di hello app attualmente possibile in modo affidabile di interpretare. È possibile trovare altre informazioni in hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Token ID di esempio
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Per procedure consigliate, tooinspect hello attestazioni in token ID esempio hello incollare token ID di esempio hello in [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Attestazioni nei token ID
| Nome | Attestazione | Valore di esempio | Descrizione |
| --- | --- | --- | --- |
| audience |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identifica il destinatario previsto hello del token hello. Nei token ID, destinatari hello sono ID applicazione dell'app, app tooyour nel portale di registrazione dell'applicazione Microsoft hello assegnato. L'app deve convalidare questo valore e rifiutare il token di hello se hello valore non corrisponde. |
| autorità di certificazione |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identifica hello servizio token di sicurezza (STS) che crea e restituisce il token hello e tenant di Azure AD hello in cui hello è stato autenticato l'utente. L'app deve convalidare l'attestazione autorità di certificazione hello tooensure che hello token proveniente dall'endpoint di hello v 2.0. È inoltre necessario utilizzare hello toorestrict hello attestazione di tenant che è possibile accedere nell'app toohello parte GUID hello. GUID che indica che l'utente hello Hello è un utente di consumer di un account di Microsoft `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| ora di emissione |`iat` |`1452285331` |Hello ora in cui hello token è stato inviato, rappresentato in valore epoch. |
| scadenza |`exp` |`1452289231` |ora di Hello in cui hello diventa non valido, token rappresentato in valore epoch. L'app deve usare la validità di hello tooverify attestazione della durata del token hello. |
| non prima |`nbf` |`1452285331` |ora di Hello in cui hello token diventa valida, rappresentato in valore epoch. È in genere hello stesso come ora di emissione hello. L'app deve usare la validità di hello tooverify attestazione della durata del token hello. |
| version |`ver` |`2.0` |versione di Hello del token ID hello, come definito da Azure AD. Per l'endpoint di hello v 2.0, il valore di hello è `2.0`. |
| ID tenant |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |È un GUID che rappresenta i tenant di Azure AD hello hello utente. Per gli account di lavoro e dell'istituto di istruzione, hello GUID è tenant non modificabile di hello ID organizzazione hello che hello utente a cui appartiene. Per gli account personali, il valore di hello è `9188040d-6c67-4c5b-b112-36a304b66dad`. Hello `profile` è necessario un ambito in ordine tooreceive questa attestazione. |
| hash del codice |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash di codice Hello è inclusa nei token di ID solo quando il token di ID hello viene eseguito con un codice di autorizzazione OAuth 2.0. Può essere utilizzato toovalidate hello autenticità di un codice di autorizzazione. Per informazioni dettagliate sull'esecuzione di questa convalida, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html). |
| hash del token di accesso |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hash token di accesso Hello è inclusa nei token di ID solo quando il token di ID hello viene eseguito con un token di accesso OAuth 2.0. Può essere utilizzato toovalidate hello autenticità di un token di accesso. Per informazioni dettagliate sull'esecuzione di questa convalida, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html). |
| nonce |`nonce` |`12345` |parametro nonce Hello è una strategia per prevenire gli attacchi di riproduzione token. L'app può specificare un parametro nonce in una richiesta di autorizzazione con hello `nonce` parametro di query. il valore di Hello fornito nella richiesta di hello viene emesso nei token hello ID `nonce` attestazione, senza modificata. L'app è possibile verificare il valore di hello con valore hello che è specificato in una richiesta di hello, che associa la sessione dell'applicazione hello con un token ID specifico. L'app deve eseguire la convalida durante il processo di convalida del token ID hello. |
| name |`name` |`Babe Ruth` |attestazione nome Hello fornisce un valore leggibile che identifica l'oggetto hello del token hello. il valore di Hello non è garantito toobe univoco è modificabile ed è progettato toobe usato solo per scopi di visualizzazione. Hello `profile` è necessario un ambito in ordine tooreceive questa attestazione. |
| email |`email` |`thegreatbambino@nyy.onmicrosoft.com` |indirizzo di posta elettronica primario Hello associata con l'account utente di hello, se presente. Il valore è modificabile e può variare nel tempo. Hello `email` è necessario un ambito in ordine tooreceive questa attestazione. |
| nome utente preferito |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Hello nome utente primario che rappresenta l'utente hello nell'endpoint di hello v 2.0. Potrebbe trattarsi di un indirizzo di posta elettronica, di un numero di telefono o di un nome utente generico senza un formato specificato. Il valore è modificabile e può variare nel tempo. Hello `profile` è necessario un ambito in ordine tooreceive questa attestazione. |
| subject |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | Hello principale su cui hello token rilascia informazioni, ad esempio utente hello di un'app. Questo valore non è modificabile e non può essere riassegnato o riutilizzato. Controlli di autorizzazione tooperform utilizzato in modo sicuro, può essere ad esempio quando il token hello è tooaccess utilizzati una risorsa e può essere utilizzato come chiave nelle tabelle di database. Poiché l'oggetto hello è sempre presente nel token hello che problemi di Azure AD, è consigliabile utilizzare questo valore in un sistema di autorizzazioni di uso generale. oggetto Hello è, tuttavia, un identificatore pairwise: è l'ID univoco tooa applicazione particolare.  Pertanto, se un singolo utente accede a due diverse App utilizzando due client diversi ID, tali App riceverà due diversi valori di attestazione subject hello.  Questa condizione può non essere appropriata a seconda dei requisiti a livello di architettura e di privacy. |
| ID oggetto |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Hello identificatore non modificabile di un oggetto in hello sistema di identità Microsoft, in questo caso, un account utente.  Può essere anche i controlli di autorizzazione tooperform utilizzato come chiave nelle tabelle di database e in modo sicuro. Questo ID identifica in modo univoco l'utente hello tutte le applicazioni: due diverse applicazioni hello riceverà stesso utente l'accesso hello stesso valore in hello `oid` attestazione.  Ciò significa che può essere utilizzato quando si creano interrogazioni tooMicrosoft online services, come hello Microsoft Graph.  Hello Microsoft Graph restituirà l'ID come hello `id` proprietà per un account utente specificato.  Poiché hello `oid` consente più App toocorrelate, hello `profile` è necessario un ambito in ordine tooreceive questa attestazione. Si noti che se un singolo utente esiste in più tenant, utente hello conterrà un ID di oggetto diverso in ogni tenant, vengono considerate come account diversi, anche se i log utente hello ogni conto con hello stesse credenziali. |

### <a name="access-tokens"></a>Token di accesso
Attualmente, i token di accesso rilasciati dall'endpoint di hello v 2.0 possono essere utilizzati solo da Microsoft Services. Le app non dovrebbero necessario tooperform qualsiasi convalida o l'ispezione dei token di accesso per uno degli scenari di hello attualmente supportato. I token di accesso possono essere considerati completamente opachi. Sono semplici stringhe che l'app possa superare tooMicrosoft nelle richieste HTTP.

In hello quasi future, v 2.0 hello endpoint introdurrà il possibilità hello per i token di accesso app tooreceive da altri client. In quel momento, hello informazioni in questo argomento di riferimento verranno aggiornate con le informazioni di hello necessarie per la convalida dei token accesso tooperform app e altre operazioni.

Quando si richiede un token di accesso dall'endpoint di hello v 2.0, endpoint v 2.0 hello restituisce inoltre i metadati relativi a token di accesso hello toouse l'app. Queste informazioni includono ora di scadenza hello di token di accesso hello e ambiti di hello per le quali è valido. L'app Usa questa metadati tooperform intelligente la memorizzazione nella cache dei token di accesso senza token di accesso di hello aprire tooparse stesso.

### <a name="refresh-tokens"></a>Token di aggiornamento
Token di aggiornamento sono token di sicurezza che l'applicazione può utilizzare tooget new token in un flusso OAuth 2.0 di accesso. L'app è possibile utilizzare aggiornamento token tooachieve a lungo termine accesso tooresources per conto dell'utente senza interazione dell'utente hello.

Si tratta di token a più risorse, Un token di aggiornamento ricevuto durante una richiesta di token per una risorsa può essere riscattato per la risorsa completamente diverse tooa i token di accesso.

tooreceive un aggiornamento in una risposta di token, l'app deve richieda e ottenga hello `offline_acesss` ambito. altre informazioni sulle hello toolearn `offline_access` ambito, vedere hello [consenso e gli ambiti](active-directory-v2-scopes.md) articolo.

Token di aggiornamento sono e sempre saranno, app tooyour completamente opaco. Essi vengono rilasciati dall'endpoint di v 2.0 hello Azure AD e può solo essere ispezionati e interpretati dall'endpoint di hello v 2.0. Sono di lunga durate, ma l'app non deve essere scritto tooexpect che durata un token di aggiornamento per qualsiasi periodo di tempo. I token di aggiornamento possono essere annullati in qualsiasi momento per vari motivi. Hello solo per i tooknow app se è valido un token di aggiornamento è tooattempt tooredeem, rendendo un endpoint di richiesta di token toohello v 2.0.

Quando si Riscatta un token di aggiornamento di un nuovo token di accesso (e se l'app è state concesse hello `offline_access` ambito), viene visualizzato un nuovo token di aggiornamento in risposta token hello. Salvare hello appena emesso aggiornamento token, tooreplace hello usato nella richiesta di hello. In questo modo è possibile prolungare la validità dei token di aggiornamento.

## <a name="validating-tokens"></a>Convalida dei token
Attualmente, hello solo la convalida token App dovrebbe essere necessario tooperform convalida i token ID. toovalidate un ID token, l'applicazione deve convalidare le attestazioni del token ID entrambi hello di firma e hello in token ID hello.

<!-- TODO: Link -->
Microsoft fornisce esempi di codice che illustrano come tooeasily gestiscono la convalida dei token e librerie. Nelle sezioni successive hello descritti hello processo sottostante. Sono anche disponibili varie librerie open source di terze parti per la convalida dei token JWT. È disponibile almeno una libreria per ogni piattaforma e linguaggio.

### <a name="validate-hello-signature"></a>Convalidare la firma hello
Un token JWT contiene tre segmenti, separati da hello `.` carattere. primo segmento Hello è noto come hello *intestazione*, secondo segmento hello è hello *corpo*, e il terzo segmento hello è hello *firma*. segmento di firma Hello può essere utilizzato toovalidate hello autenticità del token ID hello in modo che possono essere considerati attendibili dall'app.

I token ID vengono firmati usando algoritmi di crittografia asimmetrica standard del settore, come RSA 256. intestazione del token ID hello Hello contiene informazioni sulla chiave hello e metodo di crittografia utilizzato token hello toosign. ad esempio:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Hello `alg` attestazione indica l'algoritmo hello non utilizzati toosign hello token. Hello `kid` attestazione indica una chiave pubblica hello che era token hello toosign utilizzato.

In qualsiasi momento, endpoint v 2.0 hello può accedere un ID token utilizzando uno di un set specifico di coppie di chiavi pubblica / privata. endpoint v 2.0 Hello ruota periodicamente i set di possibili hello di chiavi, in modo che l'app deve essere scritto toohandle tali chiave viene modificata automaticamente. Toocheck una frequenza ragionevole per gli aggiornamenti toohello le chiavi pubbliche utilizzata dall'endpoint v 2.0 hello è di 24 ore.

È possibile acquisire hello firma i dati principali che è necessario firma hello toovalidate utilizzando hello OpenID Connect documento dei metadati si trova in:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Prova URL hello in un browser.
>
>

Questo documento di metadati è un oggetto JSON che è utile di varie informazioni, ad esempio percorso hello di hello vari endpoint necessari per l'autenticazione OpenID Connect.  documento Hello include anche un *jwks_uri*, che offre una posizione di hello di hello set di chiavi pubbliche utilizzate toosign token. documento JSON Hello in hello jwks_uri ha tutti hello informazioni sulla chiave pubblica che è attualmente in uso. L'app è possibile utilizzare hello `kid` di attestazione in hello JWT intestazione tooselect la chiave pubblica in questo documento è stato utilizzato toosign un token. Quindi viene eseguita la convalida della firma con chiave pubblica corretta hello e l'algoritmo indicato hello.

Eseguire la convalida della firma è l'ambito hello di fuori di questo documento. Molte librerie open source sono disponibili toohelp si con questo oggetto.

### <a name="validate-hello-claims"></a>Convalidare le attestazioni hello
Quando l'applicazione riceve un ID token all'account utente, deve anche eseguire alcuni controlli hello attestazioni nel token ID hello. Sono incluse, ad esempio:

* **gruppo di destinatari** attestazione, tooverify che hello token ID è stato previsto toobe dato tooyour app
* **non prima** e **scadenza** attestazioni, tooverify che hello token ID non sia scaduto.
* **autorità di certificazione** attestazione, tooverify che hello token emesso da endpoint v 2.0 hello tooyour app
* Attestazione **nonce**: per ridurre gli attacchi di riproduzione dei token.

Per un elenco completo delle convalide di attestazione che deve eseguire l'app, vedere hello [OpenID Connect specifica](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

I dettagli dei valori previsti hello per le attestazioni sono inclusi in hello [token ID](# ID tokens) sezione.

## <a name="token-lifetimes"></a>Durata dei token
Offriamo hello seguente durata dei token solo a scopo informativo. informazioni di Hello risultano utili durante lo sviluppo e debug di applicazioni. Le app non devono essere scritto tooexpect uno di questi costante tooremain durate. La durata del token può cambiare in qualsiasi momento.

| Token | Durata | Descrizione |
| --- | --- | --- |
| Token ID (account aziendale o dell'istituto di istruzione) |1 ora |I token ID hanno in genere una validità di un'ora. L'app web è possibile utilizzare questo stesso toomaintain durata una propria sessione con utente hello (scelta consigliata), oppure è possibile scegliere una durata della sessione completamente diverse. Se l'app deve tooget un nuovo token di ID, è necessario toomake sign-in una nuova richiesta toohello 2.0 autorizza un endpoint. Se l'utente di hello dispone di una sessione del browser valido con endpoint v 2.0 hello, utente hello potrebbe non essere necessari tooenter nuovamente le proprie credenziali. |
| Token ID (account personale) |24 ore |I token ID per gli account personali hanno in genere una validità di 24 ore. L'app web è possibile utilizzare questo stesso toomaintain durata una propria sessione con utente hello (scelta consigliata), oppure è possibile scegliere una durata della sessione completamente diverse. Se l'app deve tooget un nuovo token di ID, è necessario toomake sign-in una nuova richiesta toohello 2.0 autorizza un endpoint. Se l'utente di hello dispone di una sessione del browser valido con endpoint v 2.0 hello, utente hello potrebbe non essere necessari tooenter nuovamente le proprie credenziali. |
| Token di accesso (account aziendale o dell'istituto di istruzione) |1 ora |Come parte dei metadati token hello, indicato nelle risposte token. |
| Token di accesso (account personale) |1 ora |Come parte dei metadati token hello, indicato nelle risposte token. I token di accesso generati per conto di account personali possono essere configurati con una durata diversa, ma la durata tipica è un'ora. |
| Token di aggiornamento (account aziendale o dell'istituto di istruzione) |Impostare i giorni too14 |Un singolo token di aggiornamento è valido per un periodo massimo di 14 giorni. Tuttavia, il token di aggiornamento hello potrebbe diventare non valido in qualsiasi momento per vari motivi, in modo che l'app deve continuare tootry toouse un token di aggiornamento fino a quando non riesce o fino a quando l'app lo sostituisce con un nuovo token di aggiornamento. Viene inoltre valido se sono trascorsi 90 giorni dall'utente di hello ha immesso le credenziali di un token di aggiornamento. |
| Token di aggiornamento (account personale) |Backup too1 anno |Un singolo token di aggiornamento è valido per un periodo massimo di 1 anno. Tuttavia, il token di aggiornamento hello potrebbe diventare non valido in qualsiasi momento per vari motivi, in modo che l'app deve continuare tootry toouse un token di aggiornamento fino a quando si verifica un errore. |
| Codici di autorizzazione (account aziendale o dell'istituto di istruzione) |10 minuti |I codici di autorizzazione sono intenzionalmente breve durati e devono essere utilizzati immediatamente per i token di accesso e i token di aggiornamento quando vengono ricevuti i token hello. |
| Codici di autorizzazione (account personale) |5 minuti |I codici di autorizzazione sono intenzionalmente breve durati e devono essere utilizzati immediatamente per i token di accesso e i token di aggiornamento quando vengono ricevuti i token hello. I codici di autorizzazione generati per conto degli account personali possono essere usati una sola volta. |
