---
title: Scenari per Azure AD aaaAuthentication | Documenti Microsoft
description: "Una panoramica degli scenari di autenticazione più comuni di hello cinque per Azure Active Directory (AAD)"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Scenari di autenticazione per Azure AD
Azure Active Directory (Azure AD) semplifica l'autenticazione per gli sviluppatori fornendo l'identità come servizio, con supporto per protocolli standard del settore, ad esempio OAuth 2.0 e OpenID Connect, nonché librerie open source per diverse piattaforme toohelp è iniziare rapidamente a codificare. Questo documento consente di comprendere hello vari supporta scenari AD Azure e illustra le modalità di avvio tooget. È suddiviso in hello le sezioni seguenti:

* [Nozioni di base sull'autenticazione in Azure AD.](#basics-of-authentication-in-azure-ad)
* [Attestazioni nei token di sicurezza di Azure AD](#claims-in-azure-ad-security-tokens)
* [Nozioni di base sulla registrazione di un'applicazione in Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Scenari e tipi di applicazione](#application-types-and-scenarios)
  
  * [Web Browser tooWeb applicazione](#web-browser-to-web-application)
  * [Applicazione a singola pagina (SPA)](#single-page-application-spa)
  * [TooWeb applicazione nativa API](#native-application-to-web-api)
  * [TooWeb di applicazione Web API](#web-application-to-web-api)
  * [Applicazione daemon o Server tooWeb API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Nozioni di base sull'autenticazione in Azure AD.
Se non si ha familiarità con i concetti di base dell'autenticazione in Azure AD, leggere questa sezione. In caso contrario, è opportuno tooskip verso il basso troppo[scenari e tipi di applicazione](#application-types-and-scenarios).

Si consideri lo scenario di base hello in cui è necessaria l'identità: un utente in un web browser deve applicazione web di tooauthenticate tooa. Questo scenario viene descritto più dettagliatamente in hello [Web Browser tooWeb applicazione](#web-browser-to-web-application) sezione, ma un utile punto tooillustrate avvio hello funzionalità di Azure AD e definire i principi funzionamento scenario hello. Prendere in considerazione hello seguente diagramma per questo scenario:

![Panoramica dell'applicazione tooweb sign-on](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Diagramma di hello sopra presente, ecco cosa occorre tooknow sui vari componenti:

* Azure AD è hello provider di identità, responsabile della verifica dell'identità di utenti e applicazioni presenti nelle directory dell'organizzazione hello e infine rilascia i token di sicurezza alla riuscita dell'autenticazione di tali applicazioni e utenti.
* Un'applicazione che richiede l'autenticazione di toooutsource tooAzure AD deve essere registrata in Azure AD, che registra e identifica in modo univoco l'applicazione hello nella directory hello.
* Gli sviluppatori possono utilizzare hello open source di Azure AD autenticazione librerie toomake autenticazione semplice gestendo i dettagli del protocollo hello automaticamente. Per altre informazioni, vedere [Librerie di autenticazione di Azure Active Directory](active-directory-authentication-libraries.md) .

• Una volta a un utente è stato autenticato, l'applicazione hello deve convalidare tooensure token di sicurezza dell'utente hello che l'autenticazione è riuscita per hello destinati parti. Gli sviluppatori possono utilizzare hello fornito convalida toohandle librerie di autenticazione dei token da Azure AD, inclusi i token Web JSON (JWT) o SAML 2.0. Se si desidera tooperform convalida manualmente, vedere hello [gestore dei Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) documentazione.

> [!IMPORTANT]
> Azure AD Usa i token di crittografia a chiave pubblica toosign e verificare che siano validi. Vedere [importanti informazioni sulla firma Rollover della chiave di Azure AD](active-directory-signing-key-rollover.md) per ulteriori informazioni sulla logica necessaria hello è necessario tooensure l'applicazione viene sempre aggiornata con chiavi più recenti di hello.
> 
> 

• il flusso di hello di richieste e risposte per il processo di autenticazione hello è determinato dal protocollo di autenticazione hello che è stato utilizzato, ad esempio OAuth 2.0, OpenID Connect, WS-Federation o SAML 2.0. Questi protocolli sono descritti in dettaglio in hello [protocolli di autenticazione di Azure Active Directory](active-directory-authentication-protocols.md) argomento e nelle sezioni hello.

> [!NOTE]
> Azure AD supporta hello OAuth 2.0 e OpenID Connect gli standard modo diffuso utilizzano dei token di connessione, inclusi i token di connessione rappresentati come Jwt. Un token di connessione è una risorsa protetta un token di sicurezza leggero che concede hello tooa accesso "bearer". In questo senso, hello "bearer" è qualsiasi entità che possono presentare token hello. Se un'entità deve prima autenticarsi con token di connessione di Azure AD tooreceive hello, se necessario di hello token hello toosecure durante la trasmissione e di archiviazione non vengono eseguite operazioni, può essere intercettato e usato da parti non autorizzate. Molti token di sicurezza hanno meccanismi integrati per prevenire l'uso non autorizzato, ma i token di connessione ne sono sprovvisti e devono essere trasportati su un canale protetto, ad esempio Transport Layer Security (HTTPS). Se un token viene trasmesso in crittografato hello, un attacco man-in hello può essere utilizzato da un token di hello tooacquire malintenzionato e utilizzarlo per una risorsa tooa protetto da accessi non autorizzati. Hello stessi principi di sicurezza si applicano quando l'archiviazione o la memorizzazione nella cache i token di connessione per un uso successivo. Assicurarsi sempre che l'applicazione trasmetta ed archivi i token di connessione in modo sicuro. Per altre considerazioni sulla sicurezza dei token di connessione, vedere la [sezione 5 della specifica RFC 6750](http://tools.ietf.org/html/rfc6750).
> 
> 

Dopo aver creato una panoramica dei concetti di base di hello, leggere le sezioni di hello sotto toounderstand come funzionamento del provisioning in Azure AD e supporta gli scenari comuni di hello Azure AD.

## <a name="claims-in-azure-ad-security-tokens"></a>Attestazioni nei token di sicurezza di Azure AD
I token di sicurezza emessi da Azure AD contengono attestazioni o asserzioni di informazioni sull'oggetto hello che è stato autenticato. Queste attestazioni sono utilizzabile da un'applicazione hello per le varie attività. Ad esempio, sono può essere token hello toovalidate usato, identificare il tenant di directory del soggetto hello, visualizzare le informazioni utente, determinare l'autorizzazione dell'oggetto hello e così via. Hello attestazioni presenti in un determinato token di sicurezza dipendono dal tipo di hello del token, il tipo di hello delle credenziali utilizzate tooauthenticate hello utente e configurazione dell'applicazione hello. Nella seguente tabella hello, viene fornita una breve descrizione di ogni tipo di attestazione generati da Azure AD. Per ulteriori informazioni, vedere troppo[supportati Token e tipi di attestazione](active-directory-token-and-claims.md).

| Attestazione | Descrizione |
| --- | --- |
| ID applicazione |Identifica un'applicazione hello che usa token hello. |
| Audience |Identifica una risorsa di destinazione hello è destinato il token hello. |
| Riferimento alla classe contesto di autenticazione applicazione |Indica come client hello è stato autenticato (client pubblico e client riservato). |
| Istante di autenticazione |Record hello data e ora quando si è verificato durante l'autenticazione di hello. |
| Metodo di autenticazione |Indica la modalità di autenticazione soggetto hello del token hello (password, certificato e così via). |
| Nome |Fornisce hello nome dell'utente hello come impostato in Azure AD. |
| Gruppi |Contiene i gruppi di ID di Azure AD oggetto hello utente è membro di. |
| Provider di identità |Record hello provider di identità che ha autenticato hello oggetto del token hello. |
| Issued At |Ora di hello record in cui hello token è stato inviato, spesso usato per la validità del token. |
| Issuer |Identifica hello servizio token di sicurezza che ha emesso il token hello, nonché il tenant di Azure AD hello. |
| Cognome |Fornisce il cognome di hello dell'utente hello come impostato in Azure AD. |
| Nome |Fornisce un valore leggibile umano che identifica l'oggetto hello del token hello. |
| ID oggetto |Contiene un identificatore univoco e non modificabile del soggetto hello in Azure AD. |
| Ruoli |Contiene i nomi descrittivi dei ruoli di Azure AD applicazione ha ottenuto tale utente hello. |
| Scope |Indica le autorizzazioni concesse toohello client un'applicazione hello. |
| Oggetto |Indica l'entità hello sui quali hello token rilascia informazioni. |
| ID tenant |Contiene un identificatore univoco e non modificabile del tenant di directory hello che ha emesso il token hello. |
| Durata del token |Definisce l'intervallo di tempo hello entro il quale un token è valido. |
| Nome dell'entità utente |Contiene hello user principal name dell'oggetto hello. |
| Versione |Contiene il numero di versione hello del token hello. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Nozioni di base sulla registrazione di un'applicazione in Azure AD 
Tutte le applicazioni che usano l'outsourcing per l'autenticazione tooAzure che Active Directory deve essere registrato in una directory. Questo passaggio prevede la fornitura di Azure AD informazioni sull'applicazione, inclusi URL hello in cui è disponibile, hello URL toosend risposte dopo l'autenticazione, hello URI tooidentify l'applicazione e altro ancora. Queste informazioni sono necessarie per alcune ragioni fondamentali:

* Azure AD deve toocommunicate coordinate con un'applicazione hello quando si gestiscono i token di accesso o lo scambio. Sono incluse di hello seguenti:
  
  * URI ID applicazione: hello identificatore per un'applicazione. Questo valore viene inviato tooAzure AD durante l'autenticazione tooindicate quali chiamante hello applicazione richiede un token. Inoltre, questo valore viene incluso nel token hello in modo che un'applicazione hello sa che era hello previsto target.
  * Rispondi a URL e l'URI di reindirizzamento: nel caso di hello di un'API web o applicazione web, hello URL di risposta è toowhich percorso hello Azure AD invierà risposta di autenticazione hello, compreso un token se l'autenticazione è riuscita. Nel caso di hello di un'applicazione nativa, hello URI di reindirizzamento è che toowhich un identificatore univoco Azure AD reindirizzerà l'agente utente hello in una richiesta OAuth 2.0.
  * ID applicazione: hello ID per un'applicazione, che viene generata da Azure AD quando un'applicazione hello è registrata. Quando viene richiesto un codice di autorizzazione o token, hello ID applicazione e la chiave vengono inviati tooAzure AD durante l'autenticazione.
  * : Hello chiave che viene inviata insieme a un ID applicazione per l'autenticazione toocall tooAzure AD un'API web.
* Azure esigenze di Active Directory è un'applicazione hello tooensure hello tooaccess delle autorizzazioni necessarie ai dati della directory, altre applicazioni dell'organizzazione e così via

Per comprendere meglio il provisioning, è utile chiarire che esistono due categorie di applicazioni che possono essere sviluppate e integrate con Azure AD:

* Applicazione con un singolo tenant: un'applicazione con un singolo tenant è destinata all'uso in una organizzazione. In genere si tratta di applicazioni line-of-business scritte da uno sviluppatore aziendale. Un'applicazione single-tenant deve solo toobe accedere gli utenti in una directory e di conseguenza, è necessario solo toobe il provisioning in una directory. Queste applicazioni sono generalmente registrate da uno sviluppatore organizzazione hello.
* Applicazione multi-tenant: un'applicazione multi-tenant è destinata all'uso in molte organizzazioni, non solo in una. Si tratta generalmente di applicazioni SaaS (Software-as-a-Service) scritte da un fornitore di software indipendente (ISV). Applicazioni multi-tenant necessario toobe eseguito il provisioning in ogni directory in cui verranno utilizzati, che richiede tooregister consenso utente o un amministratore li. Questo processo di consenso inizia quando un'applicazione è stata registrata nella directory hello e viene fornita l'API di accesso toohello Graph o magari a un'altra API web. Quando un utente o un amministratore di un'altra organizzazione esegue la registrazione di un'applicazione hello toouse, viene visualizzata una finestra di dialogo che consente di visualizzare le autorizzazioni di hello richiede un'applicazione hello. Hello utente o un amministratore può quindi consenso toohello applicazione, che offre toohello di accesso dell'applicazione hello dichiarati dati e infine registri hello applicazione nella propria directory. Per ulteriori informazioni, vedere [Panoramica del Framework di consenso hello](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Quando si sviluppa un'applicazione multi-tenant invece di un'applicazione con un singolo tenant, occorre considerare qualche altro aspetto. Ad esempio, se si stanno apportando toousers di disponibile l'applicazione in più directory, è necessario un meccanismo toodetermine tenant in cui si trovano. Un'applicazione single-tenant deve solo toolook nella propria directory per un utente, mentre un'applicazione multi-tenant deve tooidentify un utente specifico in tutte le directory hello in Azure AD. tooaccomplish questa attività, Azure Active Directory fornisce un endpoint di autenticazione comune in cui qualsiasi applicazione multi-tenant può indirizzare le richieste di accesso, invece di un endpoint specifico del tenant. Questo endpoint è https://login.microsoftonline.com/common per tutte le directory in Azure AD, mentre un endpoint specifico del tenant potrebbe essere https://login.microsoftonline.com/contoso.onmicrosoft.com. endpoint comune Hello è particolarmente importante tooconsider quando si sviluppa l'applicazione perché occorrerà hello logica necessaria toohandle più tenant durante l'accesso, disconnessione e la convalida del token.

Se si sviluppa un'applicazione single-tenant ma che si desidera toomake è organizzazioni toomany disponibili, è possibile apportare facilmente modifiche toohello applicazione e la relativa configurazione in Azure AD toomake è in grado di multi-tenant. Inoltre, Azure AD Usa hello stessa chiave per tutti i token in tutte le directory per la firma, se si desidera fornire l'autenticazione in un singolo tenant o un'applicazione multi-tenant.

Ogni scenario indicati in questo documento include una sottosezione in cui sono descritti i relativi requisiti di provisioning. Per informazioni più dettagliate sul provisioning di un'applicazione in Azure AD e hello differenze tra applicazioni singole e multi-tenant, vedere [integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md) per ulteriori informazioni. Continuare la lettura toounderstand diversi scenari applicativi comuni hello in Azure AD.

## <a name="application-types-and-scenarios"></a>Scenari e tipi di applicazione
Ognuno di hello scenari descritti in questo documento può essere sviluppato con vari linguaggi e piattaforme. Sono tutte supportate per gli esempi di codice completo che sono disponibili nel nostro [esempi di codice della Guida](active-directory-code-samples.md), o direttamente dal corrispondente hello [repository di GitHub esempio](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Inoltre, se l'applicazione necessita di una parte o di un segmento specifico di uno scenario end-to-end, nella maggior parte dei casi è possibile aggiungere tale funzionalità in modo indipendente. Ad esempio, se si dispone di un'applicazione nativa che chiama un'API web, è possibile aggiungere facilmente un'applicazione web che chiama anche hello web API. Hello diagramma seguente illustra questi scenari e tipi di applicazioni, e come è possibile aggiungere diversi componenti:

![Scenari e tipi di applicazione](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Si tratta di hello cinque scenari di applicazione principali supportati da Azure AD:

* [Web Browser tooWeb applicazione](#web-browser-to-web-application): un utente deve toosign nell'applicazione web tooa protetta da Azure AD.
* [Singola applicazione pagina (SPA)](#single-page-application-spa): un utente deve toosign in tooa applicazione a pagina singola protetta da Azure AD.
* [TooWeb applicazione nativa API](#native-application-to-web-api): un'applicazione nativa che viene eseguito su un telefono, tablet o PC esigenze tooauthenticate tooget un utente le risorse da un'API web protetta da Azure AD.
* [Web Application tooWeb API](#web-application-to-web-api): un'applicazione web deve tooget risorse da un'API web protetta da Azure AD.
* [Applicazione daemon o Server tooWeb API](#daemon-or-server-application-to-web-api): un'applicazione daemon o un'applicazione server senza interfaccia utente web deve tooget risorse da un'API web protetta da Azure AD.

### <a name="web-browser-tooweb-application"></a>Web Browser tooWeb applicazione
Questa sezione descrive un'applicazione che autentica un utente in un'applicazione web tooa di web browser. In questo scenario, un'applicazione web hello indirizza toosign browser dell'utente hello tooAzure AD esse. Azure AD restituisce una risposta di accesso tramite il browser dell'utente hello, che contiene attestazioni sull'utente hello in un token di sicurezza. Questo scenario supporta sign-on utilizzando i protocolli WS-Federation, SAML 2.0 e OpenID Connect hello.

#### <a name="diagram"></a>Diagramma
![Flusso di autenticazione per applicazione tooweb browser](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrizione del flusso del protocollo
1. Quando un utente visita l'applicazione hello e richiede toosign in, vengono reindirizzati tramite un endpoint di autenticazione toohello richiesta di accesso di Azure AD.
2. Nella pagina di accesso hello accesso dell'utente Hello.
3. Se l'autenticazione ha esito positivo, Azure AD crea un token di autenticazione e restituisce l'URL di risposta dell'applicazione toohello una risposta di accesso che è stata configurata nel portale di Azure hello. Per un'applicazione di produzione, questo URL di risposta deve essere HTTPS. Hello ha restituito un token include le attestazioni sull'utente hello e Azure AD necessari dal token di hello toovalidate applicazione hello.
4. un'applicazione Hello convalida token hello tramite una chiave di firma pubblica e le informazioni dell'autorità di certificazione disponibile nel documento di metadati di federazione hello per Azure AD. Dopo l'applicazione hello convalida token hello, Azure AD avvia una nuova sessione utente hello. In questa sessione consente hello utente tooaccess applicazione hello fino alla scadenza.

#### <a name="code-samples"></a>Esempi di codice
Vedere gli esempi di codice hello Web Browser tooWeb scenari di applicazioni. E, consultare spesso questa pagina perché che vengono aggiunti nuovi esempi tutto il tempo hello. [Web Browser tooWeb applicazione](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Registrazione
* Single-Tenant: Se si compila un'applicazione solo per l'organizzazione, è necessario essere registrato nella directory dell'azienda tramite hello portale di Azure.
* Multi-Tenant: Se si compila un'applicazione che può essere utilizzata dagli utenti esterni all'organizzazione, deve essere registrato nella directory aziendale, ma deve anche essere registrato nella directory di ogni organizzazione che verrà utilizzato l'applicazione hello. toomake dell'applicazione disponibile nella propria directory, è possibile includere un processo di iscrizione per i clienti che consente loro tooconsent tooyour applicazione. Quando si effettua l'iscrizione per l'applicazione, viene visualizzata una finestra di dialogo che mostra un'applicazione hello autorizzazioni hello richiede e quindi hello tooconsent opzione. A seconda delle autorizzazioni hello necessarie, un amministratore hello un'altra organizzazione potrebbe essere necessario toogive consenso. Quando l'utente hello o l'amministratore acconsente, un'applicazione hello viene registrata nella propria directory. Per ulteriori informazioni, vedere [Integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Scadenza del token
la sessione dell'utente Hello scade quando scade la durata hello di hello token rilasciati da Azure AD. Se necessario, l'applicazione può abbreviare questo periodo di validità, ad esempio disconnettendo gli utenti dopo un determinato tempo di inattività. Quando la sessione hello scade, utente hello sarà richiesta toosign in nuovamente.

### <a name="single-page-application-spa"></a>Applicazione a singola pagina (SPA)
Questa sezione vengono descritte l'autenticazione per un'applicazione a pagina singola, che usa Azure AD e l'autorizzazione implicita OAuth 2.0 hello concedere toosecure terminare nuovamente l'API web. Applicazioni a pagina singola sono in genere strutturate come un livello di presentazione di JavaScript (front-end) che viene eseguito nel browser hello e un back-end Web API che viene eseguito in un server e implementa hello logica di business dell'applicazione. toolearn ulteriori informazioni su Concedi autorizzazione implicita hello e decidere se è adatta per lo scenario di applicazione, vedere [hello conoscenza implicita OAuth2 concedere del flusso di Azure Active Directory](active-directory-dev-understanding-oauth2-implicit-grant.md).

In questo scenario, quando l'accesso dell'utente hello, hello JavaScript front-end utilizza [Active Directory Authentication Library per JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) e autorizzazione implicita hello concedere tooobtain un ID token (id_token) da Azure AD. token di Hello è memorizzato nella cache e hello client lo associa toohello richiesta come token di connessione hello quando si effettuano chiamate tooits API Web back-end, che è protetta tramite middleware OWIN hello. 

#### <a name="diagram"></a>Diagramma
![Diagramma Applicazione a singola pagina (SPA)](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Descrizione del flusso del protocollo
1. utente Hello passa l'applicazione web toohello.
2. un'applicazione Hello restituisce toohello browser di hello JavaScript front-end (livello di presentazione).
3. utente Hello avvia l'accesso, ad esempio facendo clic su un collegamento di accesso. browser Hello invia un toorequest endpoint di autorizzazione di GET toohello Azure AD un ID token. Tale richiesta include l'URL di risposta e l'ID di applicazione hello nei parametri di query hello.
4. Azure AD convalida l'URL di risposta su hello registrato l'URL di risposta che è stata configurata nel portale di Azure hello hello.
5. Nella pagina di accesso hello accesso dell'utente Hello.
6. Se l'autenticazione ha esito positivo, Azure AD crea un token ID e lo restituisce come URL di risposta dell'applicazione di toohello (#) frammento URL. Per un'applicazione di produzione, questo URL di risposta deve essere HTTPS. Hello ha restituito un token include le attestazioni sull'utente hello e Azure AD necessari dal token di hello toovalidate applicazione hello.
7. il codice client Hello JavaScript in esecuzione nel browser hello estrae token hello da toouse risposta hello nella protezione delle chiamate end dell'API indietro di toohello dell'applicazione web.
8. Hello web dell'applicazione di browser chiamate hello end dell'API nuovamente con il token di accesso di hello nell'intestazione di autorizzazione hello.

#### <a name="code-samples"></a>Esempi di codice
Vedere gli esempi di codice hello per gli scenari di applicazione a pagina singola (SPA). Essere back toocheck che spesso questa pagina perché è aggiunti regolarmente nuovi esempi tutto il tempo hello. [Applicazione a singola pagina (SPA)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Registrazione
* Single-Tenant: Se si compila un'applicazione solo per l'organizzazione, è necessario essere registrato nella directory dell'azienda tramite hello portale di Azure.
* Multi-Tenant: Se si compila un'applicazione che può essere utilizzata dagli utenti esterni all'organizzazione, deve essere registrato nella directory aziendale, ma deve anche essere registrato nella directory di ogni organizzazione che verrà utilizzato l'applicazione hello. toomake dell'applicazione disponibile nella propria directory, è possibile includere un processo di iscrizione per i clienti che consente loro tooconsent tooyour applicazione. Quando si effettua l'iscrizione per l'applicazione, viene visualizzata una finestra di dialogo che mostra un'applicazione hello autorizzazioni hello richiede e quindi hello tooconsent opzione. A seconda delle autorizzazioni hello necessarie, un amministratore hello un'altra organizzazione potrebbe essere necessario toogive consenso. Quando l'utente hello o l'amministratore acconsente, un'applicazione hello viene registrata nella propria directory. Per ulteriori informazioni, vedere [Integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).

Dopo la registrazione di un'applicazione hello, deve essere configurato toouse protocollo di concessione implicita OAuth 2.0. Per impostazione predefinita, questo protocollo è disabilitato per le applicazioni. hello tooenable protocollo di concessione implicita OAuth2 per l'applicazione, modificare il manifesto dell'applicazione dal portale di Azure hello e impostare tootrue di valore "oauth2AllowImplicitFlow" hello. Per istruzioni dettagliare, vedere la sezione relativa all' [abilitazione della concessione implicita OAuth 2.0 per le applicazioni a singola pagina](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Scadenza del token
Quando si usa ADAL.js toomanage autenticazione con Azure AD, vantaggioso varie funzionalità che facilitano l'aggiornamento di un token scaduto, nonché di ottenere token per le risorse di API web aggiuntivi che possono essere chiamate da un'applicazione hello. Quando l'utente hello viene autenticato correttamente con Azure AD, viene stabilita una sessione protetta da un cookie per utente hello tra browser hello e Azure AD. È importante toonote che sessione hello esiste tra utente hello e Azure AD e non tra utente hello e un'applicazione web hello in esecuzione nel server di hello. Quando un token scade, ADAL.js Usa questa sessione toosilently ottenere un altro token. Questo non utilizzando toosend un iFrame nascosto e ricevere una richiesta di hello utilizzando il protocollo di concessione implicita OAuth hello. ADAL.js può inoltre usare lo stesso meccanismo toosilently ottenere token di accesso da Azure AD per gli altri web risorse dell'API che hello applicazione chiama, purché queste risorse supportino risorse multiorigine (CORS), di condivisione è registrate nella directory dell'utente hello e qualsiasi consenso richiesto è stato fornito dall'utente hello durante l'accesso.

### <a name="native-application-tooweb-api"></a>TooWeb applicazione nativa API
Questa sezione descrive un'applicazione nativa che chiama un'API Web per conto di un utente. Questo scenario è basato sul tipo di concessione codice di autorizzazione OAuth 2.0 hello con un client pubblico, come descritto nella sezione 4.1 di hello [specifica OAuth 2.0](http://tools.ietf.org/html/rfc6749). applicazione nativa Hello Ottiene un token di accesso per utente hello utilizzando il protocollo OAuth 2.0 hello. Questo token di accesso viene quindi inviato in hello richiesta toohello API web, che autorizza l'utente hello e restituisce la risorsa hello desiderato.

#### <a name="diagram"></a>Diagramma
![TooWeb applicazione nativa API diagramma](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Flusso di autenticazione per l'applicazione nativa tooAPI
#### <a name="description-of-protocol-flow"></a>Descrizione del flusso del protocollo
Se si utilizzano librerie di autenticazione AD hello, la maggior parte dei dettagli del protocollo hello descritti di seguito vengono gestita, ad esempio popup del browser hello, la memorizzazione nella cache di token e la gestione dei token di aggiornamento.

1. Utilizzando un popup del browser, un'applicazione nativa hello rende un endpoint di autorizzazione toohello richiesta in Azure AD. Tale richiesta include hello ID applicazione e URI di un'applicazione nativa hello di reindirizzamento hello come mostrato nel portale di Azure hello e URI ID applicazione hello per API web hello. Se hello utente non è già connesso, vengono richieste toosign in nuovo
2. Azure AD autentica l'utente hello. Se si tratta di un'applicazione multi-tenant, è un'applicazione hello toouse richiesto il consenso dell'utente di hello sarà tooconsent obbligatorio se è ancora stato fatto. Dopo aver concesso il consenso e alla riuscita dell'autenticazione, Azure AD rilascia l'URI di reindirizzamento di un'autorizzazione codice risposta toohello indietro dell'applicazione client.
3. Quando Azure AD rilascia un'autorizzazione codice di risposta toohello URI di reindirizzamento, hello codice dell'applicazione client si arresta browser interazione ed estrae hello autorizzazione dalla risposta hello. Con questo codice di autorizzazione, un'applicazione hello client invia endpoint token tooAzure una richiesta AD che include il codice di autorizzazione hello, dettagli sulle hello applicazione client (ID applicazione e URI di reindirizzamento) e la risorsa desiderata (ID applicazione hello URI per l'API web hello).
4. codice di autorizzazione Hello e informazioni sull'applicazione client hello e API web vengono convalidate da Azure AD. Se la convalida riesce, Azure AD restituisce tue token: un token di accesso JWT e un token di aggiornamento JWT. Inoltre, Azure AD restituisce le informazioni di base utente hello, ad esempio ID tenant e nome visualizzato
5. Su HTTPS, un'applicazione client hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.
6. Quando il token di accesso hello scade, un'applicazione hello client riceverà un errore che indica l'utente di hello deve tooauthenticate nuovamente. Se un'applicazione hello dispone di un token di aggiornamento valido, può essere utilizzato tooacquire un nuovo token di accesso senza chiedere conferma hello toosign utente nel nuovo. Se il token di aggiornamento hello scade, l'applicazione hello sarà necessario toointeractively nuovamente l'autenticazione utente hello una sola volta.

> [!NOTE]
> token di aggiornamento Hello emesso da Azure AD può essere utilizzato tooaccess più risorse. Ad esempio, se si dispone di un'applicazione client con l'API web toocall due di autorizzazione, il token di aggiornamento hello può essere tooget utilizzato un'accesso token toohello altre API web nonché.
> 
> 

#### <a name="code-samples"></a>Esempi di codice
Vedere gli esempi di codice hello per gli scenari di applicazione nativa tooWeb API. E, consultare spesso questa pagina perché che vengono aggiunti nuovi esempi tutto il tempo hello. [TooWeb applicazione nativa API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Registrazione
* Single-Tenant: Entrambi hello applicazione nativa e l'API web hello deve essere registrato in hello stessa directory in Azure AD. API web Hello può essere configurato tooexpose un set di autorizzazioni, che vengono utilizzati toolimit hello native accesso tooits alle risorse dell'applicazione. Hello applicazione client seleziona quindi le autorizzazioni di hello desiderato dal menu a discesa "Autorizzazioni tooOther applicazioni" hello nel hello portale di Azure.
* Multi-Tenant: Innanzitutto, un'applicazione nativa hello stata registrata solo nella developer hello o la directory del server di pubblicazione. In secondo luogo, un'applicazione nativa hello è configurato tooindicate hello autorizzazioni richieste toobe funzionale. Quando un utente o un amministratore nella directory di destinazione hello offre consenso toohello applicazione, che rende disponibili tootheir organizzazione, viene visualizzato l'elenco delle autorizzazioni necessarie in una finestra di dialogo. Alcune applicazioni richiedono autorizzazioni solo a livello di utente, che può accettare qualsiasi utente nell'organizzazione hello. Altre applicazioni richiedono autorizzazioni a livello di amministratore, che non può accettare un utente nell'organizzazione hello. Solo un amministratore di directory può concedere il consenso tooapplications che richiedono questo livello di autorizzazioni. Quando l'utente hello o l'amministratore acconsente, solo i API web di hello viene registrata nella propria directory. Per ulteriori informazioni, vedere [Integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Scadenza del token
Quando un'applicazione nativa hello Usa relativo tooget codice di autorizzazione un token di accesso JWT, riceve anche un token di aggiornamento JWT. Quando il token di accesso hello scade, token di aggiornamento hello può essere utilizzato toore-l'autenticazione utente hello senza richiederne toosign in nuovamente. Questo token di aggiornamento viene quindi utilizzato tooauthenticate hello utente, determinando un nuovo accesso del token e aggiorna token.

### <a name="web-application-tooweb-api"></a>TooWeb di applicazione Web API
Questa sezione descrive un'applicazione web che richiede risorse tooget da un'API web. In questo scenario, esistono due tipi di identità che hello applicazione web è possono utilizzare tooauthenticate e chiamare l'API web hello: identità di un'applicazione o un'identità utente delegato.

*Identità dell'applicazione:* utilizza questo scenario le credenziali client OAuth 2.0 concedono tooauthenticate come un'applicazione hello e hello accesso web API. Quando si utilizza l'identità di un'applicazione, web hello API può solo rilevare che un'applicazione web hello di chiamata, come hello web API non ricevere le informazioni su utente hello. Se un'applicazione hello riceve le informazioni sull'utente hello, verrà inviato tramite il protocollo di applicazione hello e non è firmato da Azure AD. API web Hello considera attendibile che un'applicazione web hello autenticato l'utente hello. Per questo motivo il modello è definito sottosistema attendibile.

*Identità utente delegato:* lo scenario può essere eseguito in due modi, ovvero OpenID Connect e concessione di codice di autorizzazione OAuth 2.0 con un client riservato. un'applicazione Hello web Ottiene un token di accesso per utente hello, che dimostra toohello web API applicazione web toohello hello utente autenticato correttamente e che un'applicazione web hello è stato in grado di tooobtain un utente delegato identità toocall hello API web. Questo token di accesso verrà inviato in hello richiesta toohello API web, che autorizza l'utente hello e restituisce la risorsa hello desiderato.

#### <a name="diagram"></a>Diagramma
![Diagramma di tooWeb API delle applicazioni Web](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrizione del flusso del protocollo
Entrambi hello identità dell'applicazione e vengono illustrati i tipi di identità utente delegato nel flusso di hello riportato di seguito. Hello chiave differenza è che l'identità utente delegato hello deve acquisire un codice di autorizzazione prima di hello utente può accedere e ottenere l'accesso toohello web API.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identità applicazione con concessione delle credenziali client OAuth 2.0
1. Un utente ha effettuato l'accesso tooAzure AD nell'applicazione web hello (vedere hello [tooWeb Web Browser applicazione](#web-browser-to-web-application) sopra).
2. un'applicazione web Hello deve tooacquire un token di accesso in modo che possa autenticare toohello web API e recuperare la risorsa hello desiderato. In questo modo l'endpoint token tooAzure una richiesta di AD, fornendo credenziali hello, ID dell'applicazione e URI ID applicazione dell'API web.
3. Azure AD autentica l'applicazione hello e restituisce un token di accesso JWT usato toocall hello web API.
4. Su HTTPS, un'applicazione web hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.

##### <a name="delegated-user-identity-with-openid-connect"></a>Identità utente delegato con OpenID Connect
1. Un utente ha effettuato l'accesso dell'applicazione web tooa mediante Azure AD (vedere hello [tooWeb Web Browser applicazione](#web-browser-to-web-application) sezione precedente). Se l'utente di hello dell'applicazione web hello non ha ancora acconsentito tooallowing hello web applicazione toocall hello API web per suo conto, utente hello sarà necessario tooconsent. un'applicazione Hello visualizzerà richiede le autorizzazioni di hello e se uno qualsiasi di queste autorizzazioni a livello di amministratore, utente normale nella directory di hello non sarà in grado di tooconsent. Questo processo di consenso si applica solo applicazioni toomulti-tenant, le applicazioni non single-tenant, come un'applicazione hello disporrà delle autorizzazioni necessarie hello. Quando hello utente connesso, un'applicazione web hello ha ricevuto un token ID con le informazioni sull'utente hello, nonché un codice di autorizzazione.
2. Con il codice di autorizzazione hello emesso da Azure AD, un'applicazione web hello invia endpoint token tooAzure una richiesta AD che include il codice di autorizzazione hello, dettagli sull'applicazione di hello client (ID applicazione e URI di reindirizzamento) e hello desiderato (risorsa URI ID applicazione per l'API web hello).
3. codice di autorizzazione Hello e informazioni sull'applicazione web hello e API web vengono convalidate da Azure AD. Se la convalida riesce, Azure AD restituisce tue token: un token di accesso JWT e un token di aggiornamento JWT.
4. Su HTTPS, un'applicazione web hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Identità utente delegato con concessione del codice di autorizzazione OAuth 2.0
1. Un utente è già firmato nell'applicazione web tooa, il cui meccanismo di autenticazione è indipendente da Azure AD.
2. Hello applicazione web richiede l'autorizzazione del codice tooacquire un token di accesso, quindi invia una richiesta tramite l'endpoint di autorizzazione hello browser tooAzure Active Directory, fornendo l'ID applicazione hello e URI di reindirizzamento per un'applicazione hello web dopo l'esito positivo autenticazione. utente Hello accede tooAzure Active Directory.
3. Se l'utente di hello dell'applicazione web hello non ha ancora acconsentito tooallowing hello web applicazione toocall hello API web per suo conto, utente hello sarà necessario tooconsent. un'applicazione Hello visualizzerà richiede le autorizzazioni di hello e se uno qualsiasi di queste autorizzazioni a livello di amministratore, utente normale nella directory di hello non sarà in grado di tooconsent. Il consenso si applica tooboth singolo e multi-tenant l'applicazione.  In caso di hello single-tenant, un amministratore può eseguire tooconsent consenso dell'amministratore per conto di utenti.  Questa operazione può essere eseguita utilizzando hello `Grant Permissions` pulsante hello [portale Azure](https://portal.azure.com). 
4. Dopo che l'utente hello ha accettato le condizioni, un'applicazione web hello riceve il codice di autorizzazione hello talmente tooacquire un token di accesso.
5. Con il codice di autorizzazione hello emesso da Azure AD, un'applicazione web hello invia endpoint token tooAzure una richiesta AD che include il codice di autorizzazione hello, dettagli sull'applicazione di hello client (ID applicazione e URI di reindirizzamento) e hello desiderato (risorsa URI ID applicazione per l'API web hello).
6. codice di autorizzazione Hello e informazioni sull'applicazione web hello e API web vengono convalidate da Azure AD. Se la convalida riesce, Azure AD restituisce tue token: un token di accesso JWT e un token di aggiornamento JWT.
7. Su HTTPS, un'applicazione web hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.

#### <a name="code-samples"></a>Esempi di codice
Vedere gli esempi di codice hello per gli scenari di applicazione Web tooWeb API. E, consultare spesso questa pagina perché che vengono aggiunti nuovi esempi tutto il tempo hello. Web [tooWeb applicazione API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Registrazione
* Single-Tenant: Hello applicazione web per l'identità dell'applicazione hello e case di identità utente delegato, e l'API web hello deve essere registrato in hello stessa directory in Azure AD. API web Hello può essere configurato tooexpose un set di autorizzazioni, che sono risorse tooits di accesso dell'applicazione web hello di toolimit utilizzati. Se viene utilizzato un tipo di identità utente delegato, un'applicazione hello web deve ottenere le autorizzazioni di tooselect hello desiderato dal menu a discesa "Autorizzazioni tooOther applicazioni" hello nel hello portale di Azure. Questo passaggio non è obbligatorio se viene utilizzato il tipo di identità applicazione hello.
* Multi-Tenant: in primo luogo, un'applicazione web hello è configurato tooindicate hello autorizzazioni richieste toobe funzionale. Quando un utente o un amministratore nella directory di destinazione hello offre consenso toohello applicazione, che rende disponibili tootheir organizzazione, viene visualizzato l'elenco delle autorizzazioni necessarie in una finestra di dialogo. Alcune applicazioni richiedono autorizzazioni solo a livello di utente, che può accettare qualsiasi utente nell'organizzazione hello. Altre applicazioni richiedono autorizzazioni a livello di amministratore, che non può accettare un utente nell'organizzazione hello. Solo un amministratore di directory può concedere il consenso tooapplications che richiedono questo livello di autorizzazioni. Quando le autorizzazioni utente o un amministratore, hello hello web hello e applicazione API web vengono registrate nella directory.

#### <a name="token-expiration"></a>Scadenza del token
Quando un'applicazione web hello Usa relativo tooget codice di autorizzazione un token di accesso JWT, riceve anche un token di aggiornamento JWT. Quando il token di accesso hello scade, token di aggiornamento hello può essere utilizzato toore-l'autenticazione utente hello senza richiederne toosign in nuovamente. Questo token di aggiornamento viene quindi utilizzato tooauthenticate hello utente, determinando un nuovo accesso del token e aggiorna token.

### <a name="daemon-or-server-application-tooweb-api"></a>Applicazione daemon o Server tooWeb API
Questa sezione descrive un'applicazione daemon o server che richiede risorse tooget da un'API web. Esistono due scenari secondario che si applicano sezione toothis: un'applicazione daemon che deve toocall un'API web, compilata per tipo di concessione delle credenziali client OAuth 2.0. e un'applicazione server (ad esempio un'API web) che deve toocall un'API web, basato su bozza di specifica OAuth 2.0 On-Behalf-Of.

Per uno scenario di hello quando un'applicazione daemon deve toocall un'API web, è importante toounderstand alcuni aspetti. In primo luogo, l'interazione dell'utente non è possibile con un'applicazione daemon, che richiede toohave applicazione hello la propria identità. Un esempio di un'applicazione daemon è un processo batch o un servizio del sistema operativo in esecuzione in background hello. Questo tipo di applicazione richiede un token di accesso utilizzando l'identità di applicazione e presentare il relativo ID applicazione, credenziali (password o certificato) e tooAzure URI ID applicazione Active Directory. Dopo l'autenticazione, il daemon hello riceve un token di accesso da Azure AD, che viene quindi utilizzato toocall hello API web.

Per uno scenario di hello quando un'applicazione server deve toocall un'API web, è utile toouse un esempio. Si supponga che un utente è autenticato in un'applicazione nativa e l'applicazione nativa deve toocall un'API web. Azure AD rilascia un JWT accesso token toocall hello API web. Se l'API web hello deve toocall un'altra API web downstream, può utilizzare l'identità dell'utente di hello on-behalf-of flusso toodelegate hello e l'autenticazione web di secondo livello toohello API.

#### <a name="diagram"></a>Diagramma
![Diagramma tooWeb API applicazione daemon o Server](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Descrizione del flusso del protocollo
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identità applicazione con concessione delle credenziali client OAuth 2.0
1. In primo luogo, un'applicazione server hello richiede tooauthenticate con Azure AD senza intervento dell'utente, ad esempio un dialogo interactive sign-on. In questo modo l'endpoint token tooAzure una richiesta di AD, fornendo credenziali hello, ID dell'applicazione e URI ID applicazione.
2. Azure AD autentica l'applicazione hello e restituisce un token di accesso JWT usato toocall hello web API.
3. Su HTTPS, un'applicazione web hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Identità utente delegato con la bozza di specifica OAuth 2.0 On-Behalf-Of
flusso Hello descritto di seguito si presuppone che un utente è stato autenticato in un'altra applicazione (ad esempio, un'applicazione nativa) e identità utente è stato utilizzato tooacquire un'API web di primo livello toohello token di accesso.

1. applicazione nativa Hello invia web di primo livello hello access token toohello API.
2. API web di primo livello Hello invia endpoint token tooAzure una richiesta di AD, fornendo l'ID applicazione e le credenziali, nonché il token di accesso dell'utente hello. Inoltre, hello inviata con un on_behalf_of parametro che indica hello web API richiede nuovi token toocall un'API web a valle per conto di utente originale hello.
3. Azure AD verifica tale API web di primo livello hello dispone di autorizzazioni tooaccess hello web di secondo livello API e convalida richiesta hello, restituendo che un token di accesso JWT e un JWT API web di primo livello toohello token di aggiornamento.
4. Su HTTPS, quindi chiamate all'API web di primo livello hello hello API web di secondo livello aggiungendo una stringa di token nell'intestazione di autorizzazione hello nella richiesta di hello hello. API web di primo livello Hello possibile continuare l'API web di secondo livello hello toocall come token di accesso hello e token di aggiornamento sono validi.

#### <a name="code-samples"></a>Esempi di codice
Vedere gli esempi di codice hello per gli scenari di tooWeb API applicazione Daemon o Server. E, consultare spesso questa pagina perché che vengono aggiunti nuovi esempi tutto il tempo hello. [Applicazione server o Daemon tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Registrazione
* Single-Tenant: A per l'identità dell'applicazione hello e case di identità utente delegato, un'applicazione daemon o server hello deve essere registrata in hello stessa directory in Azure AD. API web Hello può essere configurato tooexpose un set di autorizzazioni, che sono daemon hello toolimit usato o risorse tooits di accesso del server. Se viene utilizzato un tipo di identità utente delegato, un'applicazione hello server deve ottenere le autorizzazioni di tooselect hello desiderato dal menu a discesa "Autorizzazioni tooOther applicazioni" hello nel hello portale di Azure. Questo passaggio non è obbligatorio se viene utilizzato il tipo di identità applicazione hello.
* Multi-Tenant: in primo luogo, un'applicazione daemon o server hello è tooindicate configurato hello autorizzazioni richieste toobe funzionale. Quando un utente o un amministratore nella directory di destinazione hello offre consenso toohello applicazione, che rende disponibili tootheir organizzazione, viene visualizzato l'elenco delle autorizzazioni necessarie in una finestra di dialogo. Alcune applicazioni richiedono autorizzazioni solo a livello di utente, che può accettare qualsiasi utente nell'organizzazione hello. Altre applicazioni richiedono autorizzazioni a livello di amministratore, che non può accettare un utente nell'organizzazione hello. Solo un amministratore di directory può concedere il consenso tooapplications che richiedono questo livello di autorizzazioni. Quando l'utente hello o l'amministratore acconsente, entrambe le API web hello vengono registrati nella propria directory.

#### <a name="token-expiration"></a>Scadenza del token
Quando un'applicazione hello prima Usa relativo tooget codice di autorizzazione un token di accesso JWT, riceve anche un token di aggiornamento JWT. Quando il token di accesso hello scade, token di aggiornamento hello può essere utilizzato toore-l'autenticazione utente hello senza richiedere le credenziali. Questo token di aggiornamento viene quindi utilizzato tooauthenticate hello utente, determinando un nuovo accesso del token e aggiorna token.

## <a name="see-also"></a>Vedere anche
[Guida per gli sviluppatori di Azure Active Directory](active-directory-developers-guide.md)

[Esempi di codice di Azure Active Directory](active-directory-code-samples.md)

[Informazioni importanti sul rollover della chiave di firma in Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

