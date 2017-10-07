---
title: linee guida per Azure Active Directory l'accesso condizionale aaaDeveloper | Documenti Microsoft
description: Scenari e linee guida per gli sviluppatori per l'accesso condizionale di Azure AD
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Linee guida per gli sviluppatori per l'accesso condizionale di Azure Active Directory

Azure Active Directory (AD) offre diversi modi toosecure l'app e proteggere un servizio.  Una di queste funzionalità uniche è l'accesso condizionale.  Accesso condizionale consente agli sviluppatori e i servizi di tooprotect i clienti aziendali in svariati modi, ad esempio:

* Autenticazione a più fattori
* Consentire solo Intune registrati servizi specifici di dispositivi tooaccess
* Limitazione delle posizioni dell'utente e degli intervalli IP

Per ulteriori informazioni sulle funzionalità complete di hello di accesso condizionale, vedere [accesso condizionale nel portale di Azure classico hello](../active-directory-conditional-access.md). 

In questo articolo l'attenzione sul tipo di accesso condizionale significa toodevelopers creazione di applicazioni per Azure AD.  Si presuppone una conoscenza delle app a [tenant singolo](active-directory-integrating-applications.md) e [multi-tenant](active-directory-devhowto-multi-tenant-overview.md) e dei [modelli di autenticazione comuni](active-directory-authentication-scenarios.md).

Verranno esaminate impatto hello di accedere alle risorse non è possibile controllare che siano applicati criteri di accesso condizionale.  Inoltre, è esplorare implicazioni hello di accesso condizionale nel flusso di hello, per conto di applicazioni web, l'accesso di Microsoft Graph hello e chiamare le API.

## <a name="how-does-conditional-access-impact-an-app"></a>Qual è l'impatto dell'accesso condizionale su un'app?

### <a name="app-topologies-impacted"></a>Topologie di app interessate

Nella maggior parte dei casi, l'accesso condizionale non viene modificato il comportamento di un'app o richiede modifiche da Developer Edition hello.  Solo in alcuni casi, quando un'app in modalità invisibile all'utente o indirettamente richiede un token per un servizio, un'app richiede problematiche"toohandle accesso condizionale" di modifiche del codice.  L'operazione può essere semplice quanto l'esecuzione di una richiesta di accesso interattiva. 

In particolare, hello negli scenari seguenti richiedono accesso condizionale di codice toohandle "problematiche": 

* App che accedono hello Microsoft Graph
* Esecuzione di flusso di on-behalf-of hello App
* App che accedono a più servizi o risorse
* App a pagina singola che usano ADAL.js

Criteri di accesso condizionale può essere applicato toohello app, ma può inoltre essere applicate tooa web API app accede. altre informazioni sulle toolearn come tooconfigure un criterio di accesso condizionale, vedere [Introduzione a Azure Active Directory l'accesso condizionale](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

A seconda dello scenario di hello, clienti aziendali possono applicare e rimuovere i criteri di accesso condizionale in qualsiasi momento.  Per il funzionamento di toocontinue di app quando viene applicato un nuovo criterio, è necessario Gestione richiesta"tooimplement hello". Hello seguenti esempi illustrata Gestione richiesta. 

### <a name="conditional-access-examples"></a>Esempi di accesso condizionale

Alcuni scenari richiedono l'accesso condizionale toohandle modifiche al codice mentre altri funziona in modo corretto.  Ecco alcuni scenari con accesso condizionale toodo multi-factor authentication offre alcune informazioni dettagliate sulla differenza hello.

* Si sta creando un'app iOS a tenant singolo e si applicano criteri di accesso condizionale.  app Hello accede un utente e non richiedere l'accesso tooan API.  Quando l'accesso dell'utente hello, criteri hello sono richiamato automaticamente e hello deve tooperform autenticazione a più fattori (MFA). 
* Si sta compilando un'applicazione web multi-tenant che usa hello Microsoft Graph tooaccess Exchange, tra gli altri servizi.  Un cliente aziendale che usa questa app imposta criteri in SharePoint Online.  Quando l'app web hello richiede un token di Microsoft Graph, viene applicato un criterio in qualsiasi Microsoft Service (in particolare i servizi che è possibile accedere tramite graph).  All'utente finale viene richiesta l'autenticazione a più fattori (MFA). In caso di hello, per l'utente finale hello è connesso con un token valido, una richiesta"attestazioni" viene restituita toohello web app.  
* Si sta compilando un'applicazione nativa che utilizza un hello tooaccess servizio di livello intermedio Microsoft Graph.  Clienti aziendali società hello utilizzando questa applicazione si applicano un tooExchange criteri Online.  Quando un utente finale accede, app nativa hello le richieste di livello intermedio toohello di accesso e invia il token di hello.  livello intermedio Hello esegue per conto di flusso toorequest accesso toohello Microsoft Graph.  A questo punto, una richiesta"attestazioni" viene presentata toohello di livello intermedio. livello intermedio Hello invia hello challenge toohello indietro app nativa, che deve toocomply con criteri di accesso condizionale hello.

### <a name="complying-with-a-conditional-access-policy"></a>Conformità ai criteri di accesso condizionale

Per diverse topologie di app diversi, i criteri di accesso condizionale viene valutato quando viene stabilita la sessione hello.  Come criteri di accesso condizionale opera su hello granularità App e servizi, notevolmente influenzate dalla punto hello in corrispondenza del quale viene richiamato in uno scenario di hello si sta tentando di tooaccomplish.

Quando l'app prova tooaccess un servizio con un criterio di accesso condizionale, potrebbe verificarsi un problema di accesso condizionale.  Questo problema è codificato in hello `claims` parametro che viene fornito in una risposta da Azure AD o hello Microsoft Graph.  Ecco un esempio del parametro della richiesta: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Gli sviluppatori possono richiedere questo problema e li aggiunge in un nuovo tooAzure richiesta Active Directory.  Il passaggio di questo stato richiede hello dell'utente finale tooperform qualsiasi toocomply necessarie azione con i criteri di accesso condizionale hello. In seguito gli scenari di hello, vengono spiegate specifiche dell'errore hello e come tooextract hello parametro. 

## <a name="scenarios"></a>Scenari

### <a name="prerequisites"></a>Prerequisiti

L'accesso condizionale di Azure AD è una funzionalità inclusa in [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Maggiori informazioni sulle licenze di requisiti di hello [report di utilizzo senza licenza](../active-directory-conditional-access-unlicensed-usage-report.md).  Gli sviluppatori possono unirsi hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), che include un toohello sottoscrizione gratuita Enterprise Mobility Suite, che include Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Considerazioni per scenari specifici

le seguenti informazioni solo Hello si applica in questi scenari di accesso condizionale:

* App che accedono hello Microsoft Graph
* Esecuzione di flusso di on-behalf-of hello App
* App che accedono a più servizi o risorse
* App a pagina singola che usano ADAL.js

Nelle seguenti sezioni di hello, parleremo comuni scenari nei quali sono più complessi.  core Hello il principio di funzionamento è l'accesso condizionale criteri vengono valutati in fase di hello hello token viene richiesto per il servizio di hello che dispone di un criterio di accesso condizionale a meno che non si accede tramite hello Microsoft Graph.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Scenario: App l'accesso a Microsoft Graph hello

In questo scenario, vengono illustrate le case hello quando un'app web richiede l'accesso toohello Microsoft Graph. criteri di accesso condizionale Hello potrebbero essere assegnati in questo caso tooSharePoint, Exchange o qualche altro servizio che si accede come carico di lavoro tramite hello Microsoft Graph.  In questo esempio si presuppone che i criteri di accesso condizionale siano applicati a SharePoint Online.

![App l'accesso a diagramma di flusso Microsoft Graph hello](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

app Hello richiede innanzitutto autorizzazione toohello Microsoft Graph che richiede l'accesso a un carico di lavoro a valle senza accesso condizionale.  richiesta di Hello venga eseguita senza richiamare tutti i criteri e app hello riceve i token di Microsoft Graph.  A questo punto, hello app potrebbe usare hello token di accesso in una richiesta di connessione per l'endpoint di hello richiesto. A questo punto, hello app deve tooaccess un endpoint di Sharepoint Online di Microsoft Graph, ad esempio:`https://graph.microsoft.com/v1.0/me/mySite`

applicazione Hello dispone già di un token valido per hello Microsoft Graph, pertanto è possibile eseguire nuova richiesta di hello senza viene rilasciato un nuovo token. Questa richiesta non riesce e viene generata una richiesta di attestazioni da Microsoft Graph sotto forma di hello di un HTTP 403-accesso negato con un ```WWW-Authenticate``` richiesta.
Di seguito è riportato un esempio di risposta hello: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Hello attestazioni sfida è all'interno di hello ```WWW-Authenticate``` intestazione, che può essere analizzato tooextract hello attestazioni parametro per la richiesta successiva hello.  Una volta aggiunto toohello nuova richiesta, Azure AD conosce criteri di accesso condizionale hello tooevaluate quando l'accesso utente hello e app hello è ora compatibile con i criteri di accesso condizionale hello.  Ripetizione di hello richiesta toohello Sharepoint Online endpoint ha esito positivo.

Per esempi di codice che illustrano come toohandle hello attestazioni di richiesta di verifica, fare riferimento toohello [nell'esempio di codice .NET Desktop](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) per .NET ADAL o hello [nell'esempio di codice per conto di](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) per .NET ADAL.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Scenario: App esecuzione flusso hello di on-behalf-of

In questo scenario, vengono illustrate le case hello in cui un'applicazione nativa chiama un'API o un servizio web.  A sua volta, questo servizio effettua [hello flusso "on-behalf-of"](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall un servizio a valle.  In questo caso, è stato applicato l'accesso condizionale criteri toohello downstream servizio (API Web 2) e si utilizza un'applicazione nativa anziché un'app/daemon del server. 

![App hello on-behalf-of diagramma di flusso di esecuzione](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

richiesta token Hello iniziale per l'API Web 1 non viene richiesta dell'utente finale hello multi-factor Authentication come API Web 1 non può raggiungere sempre hello downstream API.  Una volta API Web 1 tenta toorequest un utente di token hello on-behalf-of per API Web 2, richiesta di hello ha esito negativo perché l'utente hello non ha sottoscritto con multi-factor authentication.

Azure AD restituisce una risposta HTTP con alcuni dati interessanti: 

> [!NOTE]
> In questa istanza è una descrizione dell'errore di autenticazione a più fattori, ma è un'ampia gamma di `interaction_required` accessi tooconditional relativi possibili.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Nel nostro API Web 1, si intercetta l'errore hello `error=interaction_required`e inviare hello Indietro `claims` app desktop toohello di richiesta di verifica.  A questo punto, può creare un nuovo app desktop hello `acquireToken()` chiamare e accodare hello `claims`challenge come parametro di stringa di query aggiuntive.  Questa nuova richiesta richiede l'autenticazione a più fattori di hello utente toodo e quindi inviare questo token nuovo indietro tooWeb 1 API e un flusso di on-behalf-of hello completo.

tootry out questo scenario, vedere il nostro [nell'esempio di codice .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Viene illustrato come toopass hello richiesta di attestazioni da app nativa di API Web 1 toohello e creare una nuova richiesta all'interno di app client hello. 

### <a name="scenario-app-accessing-multiple-services"></a>Scenario: App che accede a più servizi

In questo scenario, vengono illustrate le case hello in cui un'app web accede a due servizi di cui uno è assegnato un criterio di accesso condizionale.  A seconda della logica di app, potrebbe esistere un percorso in cui l'applicazione non richiede servizi web di accesso tooboth.  In questo scenario, in cui si richiesta un token di ordine di hello svolge un ruolo importante nell'esperienza utente finale di hello.

Si supponga di avere i servizi Web A e B e che al servizio Web B siano applicati i criteri di accesso condizionale.  Mentre la richiesta di autenticazione interattiva iniziale hello richiede il consenso per entrambi i servizi, criteri di accesso condizionale hello non sono necessario in tutti i casi.  Se l'applicazione hello richiede un token per il servizio web B, quindi richiamare i criteri di hello e le successive richieste di servizio web viene eseguita anche come indicato di seguito.

![Diagramma di flusso per le app che accedono a più servizi](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

In alternativa, se l'applicazione hello inizialmente richiede un token per il servizio web, dell'utente finale hello non richiama i criteri di accesso condizionale hello.  Questo consente allo sviluppatore di app di hello esperienza dell'utente finale di toocontrol hello e non forzare toobe criteri di accesso condizionale hello richiamato in tutti i casi. Hello complessa si verifica se app hello successivamente richiede un token per il servizio web B. A questo punto, per l'utente finale hello deve toocomply con criteri di accesso condizionale hello.  Quando tenta di app hello troppo`acquireToken`, potrebbero essere generati hello (illustrato nel seguente diagramma hello) di errore seguente: 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![App che accede a più servizi e richiede un nuovo token](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Se l'applicazione hello utilizza la libreria ADAL hello, un token di hello tooacquire errore viene sempre ripetuto in modo interattivo.  Quando si verifica questa richiesta interattiva, degli utenti finali hello sono hello opportunità toocomply con accesso condizionale hello.  Questo è vero, a meno che non è richiesta hello un `AcquireTokenSilentAsync` o `PromptBehavior.Never` nel qual caso è necessario tooperform interattivo hello app ```AcquireToken``` richiesta toogive hello utilizzo finale hello opportunità toocomply con i criteri di hello. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Scenario: App a pagina singola che usa ADAL.js

In questo scenario, esaminare i case di hello quando si dispone di un'applicazione a pagina singola (SPA), ADAL.js toocall utilizzando un accesso condizionale protetti API web.  Si tratta di un'architettura semplice ma dispone di alcuni aspetti correlati che è necessario tenere conto durante lo sviluppo dell'accesso condizionale toobe.

In ADAL.js ci sono poche funzioni che ottengono token: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)` e `acquireTokenRedirect(…)`. 

* `login()` ottiene un token ID tramite una richiesta di accesso interattiva, ma non ottiene token di accesso per alcun servizio (inclusa un'API Web protetta con accesso condizionale).  
* `acquireToken(…)`può quindi essere utilizzato toosilently ottenere un token di accesso, ovvero l'interfaccia utente non viene visualizzato in nessuna circostanza.  
* `acquireTokenPopup(…)`e `acquireTokenRedirect(…)` vengono entrambi utilizzati toointeractively richiedere un token per una risorsa, ovvero presentano sempre l'interfaccia utente di accesso.

Quando un'app richiede un toocall token di accesso un'API Web, viene effettuato un tentativo un `acquireToken(…)`.  Se la sessione di hello token è scaduta o è necessario toocomply con un criterio di accesso condizionale, hello *acquireToken* funzione ha esito negativo e hello app utilizza `acquireTokenPopup()` o `acquireTokenRedirect()`.

![Diagramma di flusso per le app a pagina singola che usano ADAL](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Verrà ora esaminato un esempio con lo scenario di accesso condizionale.  per l'utente finale Hello sufficiente ottenuto nel sito hello e non dispone di una sessione.  Si esegue una chiamata a `login()` e si ottiene un token ID senza autenticazione a più fattori.  Utente hello raggiunge quindi un pulsante che richiede hello app toorequest dati da un'API web.  app Hello tenta toodo un `acquireToken()` chiamata ma ha esito negativo poiché utente hello non ha eseguito l'autenticazione a più fattori ancora e deve toocomply con criteri di accesso condizionale hello.

Azure AD invia Indietro hello risposta HTTP seguenti: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

L'app deve hello toocatch `error=interaction_required`.  Hello applicazione può quindi utilizzare uno `acquireTokenPopup()` o `acquireTokenRedirect()` hello nella stessa risorsa.  utente Hello è forzato toodo un'autenticazione a più fattori. Al termine dell'autenticazione a più fattori hello utente hello, app hello viene rilasciato un nuovo token di accesso per hello la risorsa richiesta.

tootry out questo scenario, vedere il nostro [nell'esempio di codice per conto di SPA JS](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  In questo esempio di codice Usa Criteri di accesso condizionale hello e web API è registrato in precedenza con un toodemonstrate SPA JS questo scenario. Viene illustrato come tooproperly handle hello crediti affrontare e ottenere un token di accesso che può essere utilizzato per l'API Web. In alternativa, hello estrazione generale [nell'esempio di codice Angular.js](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) per informazioni aggiuntive su un SPA Angular


## <a name="see-also"></a>Vedere anche

* toolearn ulteriori informazioni su funzionalità hello, vedere [accesso condizionale di Azure AD](../active-directory-conditional-access.md).
* Per altri esempi di codice di Azure AD, vedere il [repository GitHub di esempi di codice](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Per ulteriori informazioni su hello la documentazione di riferimento hello ADAL SDK e di accesso, vedere [Guida libreria](active-directory-authentication-libraries.md).
* toolearn ulteriori informazioni su scenari multi-tenant, vedere [come toosign utenti usando il modello di multi-tenant hello](active-directory-devhowto-multi-tenant-overview.md).
