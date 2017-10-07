---
title: Active Directory aaaAzure ambiti v 2.0, autorizzazioni e consenso | Documenti Microsoft
description: Descrizione dell'endpoint v 2.0 hello Azure AD, inclusi il consenso, autorizzazioni e ambiti di autorizzazione.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Consenso hello Azure v 2.0 endpoint di Active Directory, autorizzazioni e ambiti
Le app che si integrano con Azure Active Directory (Azure AD) seguono un modello di autorizzazione che consente agli utenti di controllare la modalità di accesso ai dati da parte di un'app. implementazione v 2.0 Hello del modello di autorizzazione hello è stata aggiornata e viene modificato come un'app deve interagire con Azure AD. In questo articolo vengono illustrati i concetti di base di questo modello di autorizzazione, inclusi gli ambiti, autorizzazioni e consenso hello.

> [!NOTE]
> endpoint di Hello v 2.0 non supporta tutti gli scenari di Azure Active Directory e le funzionalità. toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Ambiti e autorizzazioni
Azure AD implementa hello [OAuth 2.0](active-directory-v2-protocols.md) protocollo di autorizzazione. OAuth 2.0 è un metodo tramite cui un'applicazione di terze parti può accedere alle risorse ospitate sul Web per conto dell'utente. Qualsiasi risorsa ospitata sul Web che si integra con Azure AD dispoen di un identificatore di risorsa o di un *URI ID dell'applicazione*. Ad esempio, alcune delle risorse ospitate sul Web di Microsoft includono:

* Hello API di Office 365 unificata posta elettronica:`https://outlook.office.com`
* Hello API Azure AD Graph:`https://graph.windows.net`
* Microsoft Graph: `https://graph.microsoft.com`

Hello che lo stesso vale per tutte le risorse di terze parti che sono integrate con Azure AD. Una di queste risorse inoltre possibile definire un set di autorizzazioni che possono essere utilizzati toodivide hello di funzionalità di tale risorsa in blocchi più piccoli. Ad esempio, [Microsoft Graph](https://graph.microsoft.io) definito hello toodo le autorizzazioni seguenti attività, tra gli altri:

* Lettura del calendario dell'utente
* Calendario dell'utente di scrittura tooa
* Invio di messaggi di posta elettronica come utente

La definizione di questi tipi di autorizzazioni di risorsa hello è un controllo accurato dei dati e come dati hello esposti. Un'app di terze parti può richiedere tali autorizzazioni da un utente del'app. utente applicazione Hello necessario approvare autorizzazioni hello prima applicazione hello può agire per conto dell'utente hello. Da suddivisione in blocchi di funzionalità della risorsa hello in set di autorizzazioni più piccoli, App di terze parti possono essere toorequest compilato solo hello autorizzazioni specifiche necessarie tooperform le relative funzioni. Gli utenti di App possono sapere esattamente come un'app utilizzerà i propri dati e possono essere più sicuri che app hello non funziona con malintenzionati.

In Azure AD e OAuth queste autorizzazioni vengono definite *ambiti* o Sono anche tooas cui *oAuth2Permissions*. Un ambito è rappresentato in Azure AD come valore stringa. Riprendendo l'esempio di Microsoft Graph hello, hello valore ambito per ogni autorizzazione è:

* Lettura del calendario dell'utente tramite `Calendar.Read`
* Calendario dell'utente di scrittura tooa utilizzando`Mail.ReadWrite`
* Invio di messaggi di posta elettronica come utente tramite `Mail.Send`

Un'applicazione può richiedere tali autorizzazioni specificando gli ambiti di hello nell'endpoint di richieste toohello v 2.0.

## <a name="openid-connect-scopes"></a>Ambiti di OpenID Connect
implementazione di v 2.0 Hello di OpenID Connect presenta alcuni ambiti ben definiti che si applicano risorsa specifica tooa: `openid`, `email`, `profile`, e `offline_access`.

### <a name="openid"></a>openid
Se un'applicazione esegue l'accesso tramite [OpenID Connect](active-directory-v2-protocols.md), deve richiedere hello `openid` ambito. Hello `openid` Mostra ambito account lavoro hello come autorizzazione "Accedi" hello, pagina di consenso e account Microsoft personale hello pagina di consenso come hello autorizzazione per "visualizzare il profilo e connettere tooapps e servizi con account Microsoft". Con questa autorizzazione, un'app può ricevere un identificatore univoco per l'utente hello in forma di hello di hello `sub` attestazione. Fornisce inoltre un endpoint UserInfo toohello di hello app l'accesso. Hello `openid` ambito può essere utilizzato in hello v 2.0 endpoint token tooacquire ID token, che può essere utilizzato toosecure HTTP chiamate tra i diversi componenti di un'app.

### <a name="email"></a>email
Hello `email` ambito può essere utilizzato con hello `openid` ambito e tutte le altre. Fornisce l'indirizzo di posta elettronica principale dell'utente di hello app accesso toohello sotto forma di hello di hello `email` attestazione. Hello `email` attestazione è incluso in un token solo se un indirizzo di posta elettronica è associato l'account utente hello, che non rappresenta sempre vere hello. Se utilizza hello `email` ambito, l'applicazione deve essere preparato toohandle un caso in cui hello `email` attestazione non esiste nel token hello.

### <a name="profile"></a>Profilo
Hello `profile` ambito può essere utilizzato con hello `openid` ambito e tutte le altre. Offre hello app accesso tooa notevole quantità di informazioni utente hello. può accedere a informazioni di Hello includono, ma non sono limitate a, hello nome dell'utente, cognome, nome utente preferito, ID di oggetto Per un elenco completo di attestazioni di hello profilo nel parametro id_tokens hello disponibili per un utente specifico, vedere hello [v 2.0 token riferimento](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Hello [ `offline_access` ambito](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) fornisce il tooresources accesso app per conto di utente hello per un periodo di tempo prolungato. Nella pagina di consenso account lavoro hello, questo ambito viene visualizzato come "Accedere ai dati in qualsiasi momento" autorizzazione hello. Pagina hello personale Microsoft account consenso, venga visualizzato come "Accedere alle tue info in qualsiasi momento" autorizzazione hello. Quando un utente approva hello `offline_access` ambito, l'app può ricevere i token di aggiornamento dall'endpoint token di hello v 2.0. I token di aggiornamento sono di lunga durata. L'applicazione può ottenere nuovi token di accesso quando i vecchi scadono.

Se l'app non viene richiesta hello `offline_access` ambito, non riceve i token di aggiornamento. Ciò significa che quando si Riscatta un codice di autorizzazione in hello [flusso di codice di autorizzazione OAuth 2.0](active-directory-v2-protocols.md), verrà visualizzato solo un token di accesso da hello `/token` endpoint. token di accesso Hello è valida per un breve periodo di tempo. token di accesso Hello scade in genere in un'ora. A questo punto, l'app deve tooredirect hello utente indietro toohello `/authorize` endpoint tooget un nuovo codice di autorizzazione. Durante questo reindirizzamento, a seconda dell'app, tipo di hello hello utente necessario tooenter nuovamente le proprie credenziali o toopermissions nuovamente di consenso.

Per ulteriori informazioni sulla modalità di tooget e utilizzare token di aggiornamento, vedere hello [riferimento al protocollo v 2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Richiesta di consenso per un singolo utente
In un [OpenID Connect o OAuth 2.0](active-directory-v2-protocols.md) richiesta di autorizzazione, un'applicazione può richiedere le autorizzazioni di hello necessarie tramite hello `scope` parametro di query. Ad esempio, quando un utente accede tooan app, l'applicazione hello invia una richiesta come hello di esempio seguente (con interruzioni di riga aggiunte per migliorare la leggibilità):

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Hello `scope` parametro è richiesto un elenco separato da spazi di ambiti che hello app. Ogni ambito è indicato aggiungendo hello ambito valore toohello identificatore risorsa (Buongiorno URI ID applicazione). Nell'esempio di richiesta hello, hello necessario app del calendario dell'utente di autorizzazione tooread hello e inviare un messaggio come utente hello.

Dopo che l'utente hello immette le credenziali, endpoint v 2.0 hello Cerca un record corrispondente di *il consenso dell'utente*. Se l'utente hello non ha accettato le condizioni tooany di hello richieste le autorizzazioni in versioni precedenti di hello endpoint v 2.0 hello chiede hello utente toogrant hello autorizzazioni richieste.

![Consenso dell'account aziendale](../../media/active-directory-v2-flows/work_account_consent.png)

Quando l'utente hello Approva autorizzazione hello, consenso hello verrà registrato in modo che hello utente non dispone di tooconsent nuovamente per account successivi accessi.

## <a name="requesting-consent-for-an-entire-tenant"></a>Richiesta di consenso per un intero tenant
Spesso, quando un'organizzazione acquista una licenza o una sottoscrizione per un'applicazione, hello organizzazione vuole che un'applicazione hello toofully il provisioning per tutti i dipendenti. Come parte di questo processo, un amministratore può concedere il consenso per tooact applicazione hello per conto di qualsiasi dipendente. Se salve concede il consenso per tenant intera hello, i dipendenti dell'organizzazione hello non verranno visualizzata una pagina di consenso per un'applicazione hello.

consenso toorequest per tutti gli utenti in un tenant, l'app è possibile utilizzare endpoint di autorizzazione Amministrazione hello.

## <a name="admin-restricted-scopes"></a>Ambiti riservati all'amministratore
È possibile impostare alcune autorizzazioni con privilegi elevati nell'ecosistema Microsoft hello troppo*admin con restrizioni*. Esempi di questi tipi di ambiti hello queste autorizzazioni:

* Lettura di dati in una directory aziendale tramite `Directory.Read`
* Directory dell'organizzazione di scrittura dati tooan tramite`Directory.ReadWrite`
* Lettura dei gruppi di sicurezza nella directory aziendale tramite `Groups.Read.All`

Anche se un utente di consumer potrebbe consentire un toothis di accesso dell'applicazione di tipo di dati, gli utenti dell'organizzazione sono limitati dalla concessione di accesso toohello stesso set di dati sensibili della società. Se l'applicazione richiede accesso tooone di tali autorizzazioni da un utente aziendale, l'utente hello riceve un messaggio di errore indicante che non sono le autorizzazioni dell'app tooyour tooconsent autorizzati.

Se l'app richiede l'accesso con restrizioni tooadmin ambiti per le organizzazioni, è necessario richiedere li direttamente da un amministratore della società, anche tramite l'endpoint di autorizzazione Amministrazione hello, descritto di seguito.

Quando un amministratore concede che queste autorizzazioni tramite salve consenso all'endpoint, viene fornito il consenso per tutti gli utenti nel tenant di hello.

## <a name="using-hello-admin-consent-endpoint"></a>Hello endpoint consenso dell'amministratore
Seguendo questa procedura, l'applicazione può ottenere le autorizzazioni per tutti gli utenti di un tenant, inclusi gli ambiti riservati all'amministratore. un esempio di codice che implementa i passaggi di hello, toosee vedere hello [esempio ambiti admin con restrizioni](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Richiedere le autorizzazioni di hello nel portale di registrazione applicazione hello
1. Passare tooyour applicazione hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o [creare un'app](active-directory-v2-app-registration.md) se hai già fatto.
2. Individuare hello **Microsoft Graph autorizzazioni** sezione e quindi aggiungere le autorizzazioni di hello che richiede l'app.
3. Assicurarsi di aver **salvare** hello registrazione dell'app.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Consigliato: Sign hello utente tooyour app
In genere, quando si compila un'applicazione che utilizza l'endpoint di autorizzazione Amministrazione hello, hello app richiede una pagina o una vista in cui hello amministratore può approvare le autorizzazioni dell'applicazione hello. Questa pagina può essere parte del flusso di iscrizione dell'applicazione hello, parte di impostazioni dell'applicazione hello o può essere dedicato flusso "connect". In molti casi, è opportuno per hello app tooshow questo "connect" visualizzazione solo dopo che un utente ha eseguito l'accesso con un lavoro o scuola account Microsoft.

Quando si accede utente hello in tooyour app, è possibile identificare l'organizzazione hello salve toowhich appartiene prima che richiede le autorizzazioni necessarie tooapprove hello. Sebbene non sia strettamente necessario, questo consente di creare un'esperienza più intuitiva per gli utenti dell'organizzazione. toosign hello utente, seguire il nostro [esercitazioni protocollo v 2.0](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Richiedere le autorizzazioni di hello da un amministratore di directory
Quando sarai pronto toorequest autorizzazioni da amministratore dell'organizzazione, è possibile reindirizzare hello utente toohello 2.0 *admin consenso endpoint*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| . | Condizione | Descrizione |
| --- | --- | --- |
| tenant |Obbligatorio |tenant di directory Hello che si desidera toorequest autorizzazioni. Può essere fornito nel formato di nome descrittivo o GUID. |
| client_id |Obbligatorio |l'ID applicazione Hello che hello [portale di registrazione applicazione](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assegnato tooyour app. |
| redirect_uri |Obbligatorio |Hello URI in cui si desidera hello toobe di risposta inviato per l'app toohandle di reindirizzamento. Deve corrispondere esattamente uno di reindirizzamento hello URI a cui è stato registrato nel portale di registrazione applicazione hello. |
| state |Consigliato |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. Utilizzare tooencode le informazioni sullo stato di hello sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio si trovassero nelle pagina hello o vista. |

A questo punto, Azure AD richiede un toosign amministratore tenant nella richiesta di hello toocomplete. messaggio per l'amministratore ha richiesto tooapprove che tutti hello autorizzazioni richieste per l'app nel portale di registrazione applicazione hello.

#### <a name="successful-response"></a>Risposta con esito positivo
Se salve Approva autorizzazioni hello per l'app, la risposta corretta hello simile al seguente:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| . | Descrizione |
| --- | --- | --- |
| tenant |tenant di directory Hello concesse le autorizzazioni per l'applicazione hello richiesti, in formato GUID. |
| state |Un valore incluso nella richiesta di hello che verrà anche restituito nella risposta token hello. Può trattarsi di una stringa di qualsiasi contenuto. lo stato di Hello è tooencode utilizzati informazioni sullo stato dell'utente hello in app hello prima dell'esecuzione della richiesta di autenticazione hello, ad esempio pagina hello o fossero nella vista. |
| admin_consent |Verrà impostato troppo**true**. |

#### <a name="error-response"></a>Risposta di errore
Se salve non approvare le autorizzazioni di hello per le app, hello Impossibile risposta ha un aspetto simile al seguente:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| . | Descrizione |
| --- | --- | --- |
| error |Una stringa di codice di errore che può essere utilizzati tooclassify tipi di errori che si verificano e può essere utilizzati tooreact tooerrors. |
| error_description |Un messaggio di errore specifico che consente a uno sviluppatore di identificare causa radice di hello di un errore. |

Dopo aver ricevuto una risposta corretta dall'endpoint di consenso dell'amministratore hello, l'app ha ottenuto le autorizzazioni di hello che quando richiesto. Successivamente, è possibile richiedere un token per la risorsa hello desiderato.

## <a name="using-permissions"></a>Uso delle autorizzazioni
Dopo che l'utente hello acconsente toopermissions per l'app, l'app può acquisire i token di accesso che rappresentano tooaccess di autorizzazione dell'app una risorsa in alcune capacità. Un token di accesso può essere utilizzato solo per una singola risorsa, ma infatti codificato all'interno di token di accesso hello è ogni autorizzazione che l'app è stata concessa per tale risorsa. tooacquire un token di accesso, l'app può effettuare un richiesta toohello v 2.0 token endpoint simile al seguente:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

È possibile utilizzare il token di accesso risultante hello nella risorsa di toohello le richieste HTTP. Indica in modo affidabile toohello risorse che l'app abbia hello delle autorizzazioni appropriate tooperform un'attività specifica.  

Per ulteriori informazioni su OAuth 2.0 hello del protocollo e tooget i token di accesso, vedere hello [riferimento protocollo dell'endpoint v 2.0](active-directory-v2-protocols.md).
