---
title: Active Directory Developer glossario aaaAzure | Documenti Microsoft
description: "Elenco di termini relativi ai concetti e alle funzionalità per sviluppatori di uso comune di Azure Active Directory."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Glossario per gli sviluppatori di Azure Active Directory
In questo articolo contiene le definizioni per alcune delle hello Azure Active Directory (AD) per sviluppatori concetti di base, che risultano utili informazioni sullo sviluppo di applicazioni per Azure AD.

## <a name="access-token"></a>token di accesso
Un tipo di [token di sicurezza](#security-token) emesso da un [server autorizzazione](#authorization-server)e utilizzato da un [applicazione client](#client-application) in ordine tooaccess un [risorse server protetto ](#resource-server). In genere sotto forma di hello di un [JSON Web Token (JWT)][JWT], token hello incorpora autorizzazione hello concesso hello client toohello [proprietario della risorsa](#resource-owner), per un livello di richiesto di accesso. Hello token contiene tutti i [attestazioni](#claim) sull'oggetto hello, abilitazione hello client applicazione toouse come un tipo di credenziali quando si accede a una determinata risorsa. Elimina anche hello del client di toohello credenziali hello risorsa proprietario tooexpose sia necessaria.

I token di accesso sono a volte denominata tooas "Utente + App" o "Solo App", a seconda di hello credenziali rappresentato. Ad esempio:

* [Concessione delle autorizzazioni "Codice di autorizzazione"](#authorization-grant), prima come proprietario della risorsa hello di autenticazione dell'utente finale di hello, la delega dell'autorizzazione toohello tooaccess client hello risorse. autentica il client di Hello in seguito quando si ottiene il token di accesso hello. token Hello può talvolta essere toomore cui viene fatto riferimento in modo specifico come un token di "Utente + App", in quanto rappresenta entrambi utente hello che ha autorizzato l'applicazione client hello e un'applicazione hello.
* [Concessione delle autorizzazioni "Le credenziali del client"](#authorization-grant)client hello fornisce autenticazione unico hello, funzionamento senza autenticazione/autorizzazione di hello-del proprietario della risorsa, in modo token hello può talvolta essere tooas di cui si fa riferimento un token di tipo "Solo App".

Per altri dettagli, vedere [Informazioni di riferimento sui token in Azure AD][AAD-Tokens-Claims].

## <a name="application-manifest"></a>manifesto dell'applicazione
Una funzionalità fornita da hello [portale di Azure][AZURE-portal], che produce una rappresentazione JSON della configurazione di identità dell'applicazione hello, utilizzato come meccanismo per l'aggiornamento associato [ Applicazione] [ AAD-Graph-App-Entity] e [ServicePrincipal] [ AAD-Graph-Sp-Entity] entità. Vedere [manifesto dell'applicazione Azure Active Directory di conoscenza hello] [ AAD-App-Manifest] per altri dettagli.

## <a name="application-object"></a>oggetto applicazione
Quando si registra o aggiornare un'applicazione hello [portale di Azure][AZURE-portal], portale hello Crea/aggiorna un oggetto applicazione e un oggetto corrispondente [oggetto entità servizio](#service-principal-object)per tenant. oggetto applicazione Hello *definisce* hello configurazione dell'identità dell'applicazione globale (tra tutti i tenant in cui ha accesso), fornendo un modello da cui sono relativi oggetti principale di servizio corrispondente  *derivato* per l'utilizzo in locale in fase di esecuzione (in un tenant specifico).

Per altre informazioni, vedere [Oggetti applicazione e oggetti entità servizio in Azure Active Directory][AAD-App-SP-Objects].

## <a name="application-registration"></a>registrazione dell'applicazione
In ordine tooallow un'applicazione toointegrate con e il delegato Identity and Access Management tooAzure funzioni AD, deve essere registrato con Azure Active Directory [tenant](#tenant). Quando si registra l'applicazione con Azure AD, si specifica una configurazione di identità per l'applicazione, in modo che toointegrate con Azure AD e utilizzano le funzionalità, ad esempio:

* Gestione affidabile dell'accesso Single Sign-On con l'implementazione del protocollo [OpenID Connect][OpenIDConnect] e la gestione delle identità di Azure AD
* Negoziata accesso troppo[risorse protette](#resource-server) da [applicazioni client](#client-application), tramite OAuth 2.0 Azure Active Directory [server autorizzazione](#authorization-server) implementazione
* [Framework di consenso](#consent) per la gestione delle risorse di tooprotected accesso client, in base alle autorizzazioni di proprietario di risorse.

Per altri dettagli, vedere [Integrazione di applicazioni con Azure Active Directory][AAD-Integrating-Apps].

## <a name="authentication"></a>authentication
atto di Hello di difficile un'entità per le credenziali legittime, fornendo la base hello per la creazione di un toobe dell'entità di sicurezza utilizzato per il controllo di identità e accessi. Durante un [concessione di autorizzazione OAuth2](#authorization-grant) , ad esempio, l'autenticazione di terze parti di hello riempie ruolo hello del [proprietario della risorsa](#resource-owner) o [applicazione client](#client-application), a seconda concessione di Hello utilizzato.

## <a name="authorization"></a>autorizzazione
atto di Hello concede un toodo autorizzazione dell'entità di sicurezza autenticato un elemento. Esistono due casi d'uso principali nel modello di programmazione di hello Azure AD:

* Durante un [concessione di autorizzazione OAuth2](#authorization-grant) flusso: hello quando [proprietario della risorsa](#resource-owner) concede l'autorizzazione toohello [applicazione client](#client-application), consentendo ai client di hello hello tooaccess risorse del proprietario della risorsa.
* Durante l'accesso alle risorse da parte di client hello: come implementato dalla hello [server delle risorse](#resource-server), utilizzando hello [attestazione](#claim) valori presenti in hello [token di accesso](#access-token) toomake il controllo di accesso decisioni basate su di esse.

## <a name="authorization-code"></a>codice di autorizzazione
Un breve durata "token" fornito tooa [applicazione client](#client-application) da hello [endpoint di autorizzazione](#authorization-endpoint), come parte del flusso di "codice di autorizzazione" hello, uno dei quattro OAuth2 di hello [concede l'autorizzazione ](#authorization-grant). codice Hello viene restituito l'applicazione client toohello in tooauthentication di risposta di un [proprietario della risorsa](#resource-owner), che indica il proprietario di risorse hello è delegata hello tooaccess autorizzazione delle risorse richieste. Come parte del flusso di hello, codice hello viene recuperato in un secondo momento per un [token di accesso](#access-token).

## <a name="authorization-endpoint"></a>endpoint di autorizzazione
Uno degli endpoint hello implementato da hello [server autorizzazione](#authorization-server), utilizzare toointeract con hello [proprietario della risorsa](#resource-owner) in ordine tooprovide un [autorizzazione grant](#authorization-grant) durante un flusso di concessione di autorizzazione OAuth2. A seconda delle autorizzazioni di hello flusso di concessione usato, hello effettivo può variare grant forniti, tra cui un [codice di autorizzazione](#authorization-code) o [token di sicurezza](#security-token).

Vedere della specifica di hello OAuth2 [tipi di concessione di autorizzazioni] [ OAuth2-AuthZ-Grant-Types] e [endpoint di autorizzazione] [ OAuth2-AuthZ-Endpoint] sezioni e hello [Specifica OpenIDConnect] [ OpenIDConnect-AuthZ-Endpoint] per altri dettagli.

## <a name="authorization-grant"></a>concessione di autorizzazione
Una credenziale che rappresenta hello [del proprietario della risorsa](#resource-owner) [autorizzazione](#authorization) tooaccess relativo alle risorse protette, concesse tooa [applicazione client](#client-application). Un'applicazione client può utilizzare uno dei hello [quattro concedere tipi definiti dal Framework di autorizzazione OAuth2 hello] [ OAuth2-AuthZ-Grant-Types] tooobtain un'istruzione grant, in base al tipo di requisiti: "concessione del codice", " concessione di credenziali client","concessione implicita"e"concessione di credenziali di password proprietario di risorse". credenziali Hello restituito toohello client è un [token di accesso](#access-token), o un [codice di autorizzazione](#authorization-code) (state scambiate in un secondo momento per un token di accesso), in base al tipo di hello di concessione di autorizzazioni utilizzato.

## <a name="authorization-server"></a>server di autorizzazione
Come definito da hello [Framework di autorizzazione OAuth2][OAuth2-Role-Def], server hello responsabile per il rilascio di access token toohello [client](#client-application) dopo l'autenticazione Hello [proprietario della risorsa](#resource-owner) e ottenere l'autorizzazione. A [applicazione client](#client-application) interagisce con il server di autorizzazione hello in fase di esecuzione tramite il relativo [autorizzazione](#authorization-endpoint) e [token](#token-endpoint) endpoint, in base alle hello OAuth2 definito [concede l'autorizzazione](#authorization-grant).

Nel caso di hello di integrazione dell'applicazione Azure AD, Azure AD implementa ruolo del server di autorizzazione hello per le applicazioni di Azure AD e il servizio Microsoft API, ad esempio [Microsoft Graph API][Microsoft-Graph].

## <a name="claim"></a>attestazione
Oggetto [token di sicurezza](#security-token) contiene le attestazioni, che forniscono le asserzioni su un'entità (ad esempio un [applicazione client](#client-application) o [proprietario della risorsa](#resource-owner)) tooanother entità (ad esempio hello [server delle risorse](#resource-server)). Le attestazioni sono coppie nome/valore che inoltrano i dati relativi a hello token argomento (ad esempio, hello entità di sicurezza che è stato autenticato da hello [server autorizzazione](#authorization-server)). Hello attestazioni presenti in un determinato token dipendono da variabili diverse, inclusi tipo di hello del token, hello tipo di credenziale utilizzata tooauthenticate hello soggetto, configurazione dell'applicazione hello e così via.

Per altri dettagli, vedere [Informazioni di riferimento sui token in Azure AD][AAD-Tokens-Claims].

## <a name="client-application"></a>applicazione client
Come definito da hello [Framework di autorizzazione OAuth2][OAuth2-Role-Def], un'applicazione che rende protetto da richieste di risorse per conto di hello [proprietario della risorsa](#resource-owner). il termine Hello "client" implica qualsiasi caratteristica di hardware particolare implementazione (ad esempio, se un'applicazione hello viene eseguita in un server, un desktop o altri dispositivi).  

Un'applicazione client richiede [autorizzazione](#authorization) da un tooparticipate proprietario di risorse in un [concessione di autorizzazione OAuth2](#authorization-grant) flusso e può accedere API/dati per conto del proprietario della risorsa hello. Il Framework di autorizzazione OAuth2 Hello [definisce due tipi di client][OAuth2-Client-Types], "riservati" e "public", a seconda possibilità toomaintain hello la riservatezza del client hello delle relative credenziali. Le applicazioni possono implementare un [client Web (riservato)](#web-client) eseguito in un server Web, un [client nativo (pubblico)](#native-client) installato in un dispositivo o un [client basato su agente utente (pubblico)](#user-agent-based-client) eseguito nel browser di un dispositivo.

## <a name="consent"></a>consenso
Hello processo di un [proprietario della risorsa](#resource-owner) concessione dell'autorizzazione tooa [applicazione client](#client-application), tooaccess protetto risorse specifiche [autorizzazioni](#permissions), per conto di hello proprietario della risorsa. A seconda delle autorizzazioni hello richieste da client hello, un amministratore o utente verrà richiesto per i dati dell'organizzazione o singoli consenso tooallow accesso tootheir rispettivamente. Si noti che in un [multi-tenant](#multi-tenant-application) scenario, dell'applicazione hello [dell'entità servizio](#service-principal-object) viene anche registrato nel tenant di hello dell'utente il consenso hello.

## <a name="id-token"></a>token ID
Un [OpenID Connect] [ OpenIDConnect-ID-Token] [token di sicurezza](#security-token) fornito da un [del server di autorizzazione](#authorization-server) [endpointdiautorizzazione](#authorization-endpoint), che contiene [attestazioni](#claim) relativi toohello autenticazione dell'utente finale [proprietario della risorsa](#resource-owner). Così come i token di accesso, i token ID sono rappresentati anche come [token JSON Web (token JWT)][JWT] con firma digitale. A differenza di un token di accesso, tuttavia, le attestazioni del token di un ID non vengono utilizzate per scopi correlati tooresource accesso e controllo di accesso in modo specifico.

Per altri dettagli, vedere [Informazioni di riferimento sui token in Azure AD][AAD-Tokens-Claims].

## <a name="multi-tenant-application"></a>applicazione multi-tenant
Una classe dell'applicazione che consente l'accesso e [consenso](#consent) dagli utenti, il provisioning in qualsiasi AD Azure [tenant](#tenant), tra cui tenant diversi da quelli hello in cui è registrata client hello. [Native client](#native-client) multi-tenant per impostazione predefinita, le applicazioni siano mentre [client web](#web-client) e [web API/risorse](#resource-server) applicazioni hanno hello possibilità tooselect tra singola o multi-tenant. Al contrario, un'applicazione web registrato come single-tenant, consentirebbe accessi da account utente, il provisioning in hello stesso tenant come hello uno in cui un'applicazione hello è registrata.

Vedere [come toosign in qualsiasi utente di Azure AD usando hello modello di applicazione multi-tenant] [ AAD-Multi-Tenant-Overview] per altri dettagli.

## <a name="native-client"></a>client nativo
Tipo di [applicazione client](#client-application) che è installato in modo nativo in un dispositivo. Poiché tutto il codice viene eseguito su un dispositivo, viene considerato un client "public" a causa di tooits impossibilità toostore credenziali privatamente/riservatezza. Per altri dettagli, vedere [i profili e i tipi di client di OAuth2][OAuth2-Client-Types].

## <a name="permissions"></a>autorizzazioni
Oggetto [applicazione client](#client-application) miglioramenti accedere tooa [server delle risorse](#resource-server) , dichiarando che le richieste di autorizzazione. Sono disponibili due tipi:

* Autorizzazioni, specificano "delega" [basata sull'ambito](#scopes) accesso mediante la delega di autorizzazioni da hello connesso [proprietario della risorsa](#resource-owner), vengono presentati toohello risorse in fase di esecuzione come ["scp "attestazioni](#claim) in client di hello [token di accesso](#access-token).
* Le autorizzazioni "Applicazione", che specificano [basata sui ruoli](#roles) accedere utilizzando le credenziali/identità dell'applicazione client hello, vengono presentati toohello risorse in fase di esecuzione come [attestazioni "ruoli"](#claim) in hello token di accesso del client.

Sono inoltre superficie durante hello [consenso](#consent) processo insieme a un messaggio per l'amministratore o risorse proprietario hello opportunità toogrant/deny hello client accesso tooresources al proprio tenant.

Le richieste di autorizzazione configurate in hello "Applicazioni" / "Impostazioni" scheda hello [portale di Azure][AZURE-portal], nella sezione "Autorizzazioni richieste", selezionando hello desiderato "Autorizzazioni delegate" e " Autorizzazioni per l'applicazione"(hello quest'ultimo richiede l'appartenenza al ruolo amministratore globale di hello). Poiché un [client pubblico](#client-application) non è possibile gestire in modo sicuro le credenziali, è possibile richiedere solo le autorizzazioni delegate, mentre un [client riservato](#client-application) ha hello possibilità toorequest applicazione e delegata autorizzazioni. client Hello [oggetto applicazione](#application-object) hello archivi dichiarato autorizzazioni nel relativo [requiredResourceAccess proprietà][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>proprietario delle risorse
Come definito da hello [Framework di autorizzazione OAuth2][OAuth2-Role-Def], un'entità in grado di concedere l'accesso tooa la risorsa protetta. Quando un utente proprietario della risorsa hello è è tooas cui un utente finale. Ad esempio, quando un [applicazione client](#client-application) richiede la cassetta postale dell'utente tramite hello tooaccess [Microsoft Graph API][Microsoft-Graph], richiede l'autorizzazione dal proprietario della risorsa di hello cassetta postale Hello.

## <a name="resource-server"></a>server di risorse
Come definito da hello [Framework di autorizzazione OAuth2][OAuth2-Role-Def], un server che ospita risorse protette, in grado di accettare e rispondere tooprotected risorse richieste da [client applicazioni](#client-application) che presenti un [token di accesso](#access-token). È detto anche server di risorse protette o applicazione della risorsa.

Un server delle risorse espone le API e applica accedere alle risorse protette tooits tramite [ambiti](#scopes) e [ruoli](#roles), utilizzando hello Framework di autorizzazione OAuth 2.0. Esempi di API di Azure AD Graph hello che fornisce i dati del tenant tooAzure AD accesso e hello API di Office 365 che forniscono accesso toodata, ad esempio posta elettronica e al calendario. Entrambi sono accessibili anche tramite hello [Microsoft Graph API][Microsoft-Graph].  

Analogamente a un'applicazione client, la configurazione di identità dell'applicazione della risorsa viene stabilita tramite [registrazione](#application-registration) in un tenant di Azure AD, fornendo sia un'applicazione hello e oggetto entità servizio. Alcune API fornita da Microsoft, ad esempio hello API Graph di Azure AD sono pre-registrato le entità servizio rese disponibile in tutti i tenant durante il provisioning.

## <a name="roles"></a>roles
Ad esempio [ambiti](#scopes), ruoli forniscono un modo per un [server delle risorse](#resource-server) toogovern accesso tooits risorse protette. Esistono due tipi: un ruolo "user" implementa il controllo di accesso basato sui ruoli per gli utenti o gruppi che richiedono accesso toohello risorse, mentre implementa un ruolo "applicazione" hello uguale per [applicazioni client](#client-application) che richiedono l'accesso.

I ruoli sono stringhe di risorsa definita (ad esempio "Expense responsabile dell'approvazione", "Sola lettura", "Directory.ReadWrite.All") e gestire in hello [portale di Azure] [ AZURE-portal] tramite della risorsa hello [applicazione manifesto](#application-manifest)e archiviati nella risorsa di hello [appRoles proprietà][AAD-Graph-Sp-Entity]. Hello portale di Azure è inoltre usato tooassign utenti troppo ruoli "user" e configurare i client [autorizzazioni applicazione](#permissions) tooaccess un ruolo "applicazione".

Per una descrizione dettagliata dei ruoli applicazione hello esposti dall'API Graph di Azure AD, vedere [ambiti di autorizzazione dell'API Graph][AAD-Graph-Perm-Scopes]. Per un esempio dettagliato di implementazione, vedere [Role based access control in cloud applications using Azure AD][Duyshant-Role-Blog] (Controllo degli accessi in base al ruolo nelle applicazioni cloud con Azure AD).

## <a name="scopes"></a>ambiti
Ad esempio [ruoli](#roles), gli ambiti di forniscono un modo per un [server delle risorse](#resource-server) toogovern accesso tooits risorse protette. Gli ambiti sono utilizzati tooimplement [basata sull'ambito] [ OAuth2-Access-Token-Scopes] , controllo di accesso per un [applicazione client](#client-application) che è stato assegnato l'accesso delegato toohello risorsa dal relativo proprietario.

Gli ambiti sono risorsa definita stringhe (ad esempio "Mail.Read", "Directory.ReadWrite.All"), gestite in hello [portale di Azure] [ AZURE-portal] tramite della risorsa hello [manifesto dell'applicazione](#application-manifest)e archiviati nella risorsa di hello [oauth2Permissions proprietà][AAD-Graph-Sp-Entity]. Hello portale di Azure è inoltre usato tooconfigure applicazione client [autorizzazioni delegate](#permissions) tooaccess un ambito.

Una convenzione di denominazione prassi migliori, è un formato "assumono" toouse. Per una descrizione dettagliata degli ambiti hello esposti dall'API Graph di Azure AD, vedere [ambiti di autorizzazione dell'API Graph][AAD-Graph-Perm-Scopes]. Per informazioni sugli ambiti esposti dai servizi di Office 365, vedere [Office 365 API permissions reference][O365-Perm-Ref] (Informazioni di riferimento sulle autorizzazioni delle API di Office 365).

## <a name="security-token"></a>token di sicurezza
Documento firmato contenente attestazioni, come un token OAuth2 o un'asserzione SAML 2.0. Per una [concessione di autorizzazione](#authorization-grant) OAuth2, un [token di accesso](#access-token) (OAuth2) e un [token ID](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) costituiscono un tipo di token di sicurezza e vengono entrambi implementati come [token JSON Web (token JWT)][JWT].

## <a name="service-principal-object"></a>oggetto entità servizio
Quando si registra o aggiornare un'applicazione hello [portale di Azure][AZURE-portal], portale hello creazioni, aggiornamenti sia un [oggetto applicazione](#application-object) e un'entità servizio corrispondente oggetto per il tenant. oggetto applicazione Hello *definisce* hello configurazione dell'identità dell'applicazione globale (tra tutti i tenant in cui un'applicazione hello associato è stato concesso l'accesso), e hello modello da cui il servizio corrispondente gli oggetti principali sono *derivato* per l'utilizzo in locale in fase di esecuzione (in un tenant specifico).

Per altre informazioni, vedere [Oggetti applicazione e oggetti entità servizio in Azure Active Directory][AAD-App-SP-Objects].

## <a name="sign-in"></a>accesso
Hello processo di un [applicazione client](#client-application) avvia autenticazione degli utenti finali e l'acquisizione correlati stato, a scopo di hello di acquisire un [token di sicurezza](#security-token) e ambito hello applicazione sessione toothat stato. Lo stato può includere elementi come informazioni del profilo utente e informazioni derivate dalle attestazioni del token.

funzione sign Hello di un'applicazione è in genere utilizzate tooimplement single sign-on (SSO). Si può anche essere preceduto da una funzione di "registrazione", come punto di ingresso hello per un'applicazione di tooan accesso toogain utente finale (al primo accesso di). Hello funzione iscrizione è toogather utilizzato e mantenere utente toohello specifico stato aggiuntivi e possono richiedere [il consenso dell'utente](#consent).

## <a name="sign-out"></a>disconnessione
Hello processo di autenticazione non di un utente finale, lo scollegamento di stato utente hello associato hello [applicazione client](#client-application) sessione durante [Accedi](#sign-in)

## <a name="tenant"></a>tenant
Un'istanza di una directory di Azure AD è tooas di cui si fa riferimento un tenant di Azure AD. Offre una serie di funzionalità, tra cui:

* un servizio di registro per applicazioni integrate
* autenticazione di account utente e applicazioni registrate
* Gli endpoint REST necessari toosupport vari protocolli, tra cui SAML, tra cui hello e OAuth2 [endpoint di autorizzazione](#authorization-endpoint), [endpoint token](#token-endpoint) e hello "common" endpoint usato dal [ applicazioni multi-tenant](#multi-tenant-application).

Un tenant è anche associato a un annuncio di Azure o sottoscrizione Office 365 durante il provisioning della sottoscrizione di hello, fornendo funzionalità di gestione accesso e identità per la sottoscrizione di hello. Vedere [come tenant di Azure Active Directory tooget] [ AAD-How-To-Tenant] per informazioni dettagliate su hello vari modi per ottenere accesso tooa tenant. Vedere [delle sottoscrizioni Azure sono associate con Azure Active Directory] [ AAD-How-Subscriptions-Assoc] per informazioni dettagliate sulla relazione hello tra sottoscrizioni e un tenant di Azure AD.

## <a name="token-endpoint"></a>endpoint di token
Uno degli endpoint hello implementato da hello [server autorizzazione](#authorization-server) toosupport OAuth2 [concede l'autorizzazione](#authorization-grant). A seconda della concessione di hello, può essere utilizzato tooacquire un [token di accesso](#access-token) (e correlate token "Aggiorna") tooa [client](#client-application), o [token ID](#ID-token) se usato con hello [ OpenID Connect] [ OpenIDConnect] protocollo.

## <a name="user-agent-based-client"></a>client basato su agente utente
Tipo di [applicazione client](#client-application) che scarica il codice da un server Web e viene eseguita all'interno di un agente utente (come un Web browser), ad esempio un'applicazione a singola pagina. Poiché tutto il codice viene eseguito su un dispositivo, viene considerato un client "public" a causa di tooits impossibilità toostore credenziali privatamente/riservatezza. Per altri dettagli, vedere [i profili e i tipi di client di OAuth2][OAuth2-Client-Types].

## <a name="user-principal"></a>entità utente
Allo stesso modo toohello che un oggetto entità servizio viene utilizzato toorepresent un'istanza dell'applicazione, un oggetto dell'entità utente è un altro tipo di entità di sicurezza, che rappresenta un utente. Hello Azure AD Graph [entità utente] [ AAD-Graph-User-Entity] definisce hello schema per un oggetto utente, incluse le proprietà relative agli utenti, ad esempio nome e cognome, nome dell'entità utente, appartenenza al ruolo di directory, e così via. Questo fornisce la configurazione di identità utente hello per Azure AD tooestablish un utente dell'entità in fase di esecuzione. entità utente Hello è toorepresent usato un utente autenticato per Single Sign-On, la registrazione [consenso](#consent) delega, effettua le decisioni di controllo di accesso e così via.

## <a name="web-client"></a>client Web
Un tipo di [applicazione client](#client-application) che viene eseguito tutto il codice in un server web e in grado di toofunction come "riservati" client da archiviare in modo sicuro le credenziali nel server di hello. Per altri dettagli, vedere [i profili e i tipi di client di OAuth2][OAuth2-Client-Types].

## <a name="next-steps"></a>Passaggi successivi
Hello [Guida per gli sviluppatori di Azure AD] [ AAD-Dev-Guide] è hello toouse portale per lo sviluppo di Azure AD argomenti, inclusa una panoramica delle correlati [integrazione dell'applicazione] [ AAD-How-To-Integrate] e concetti di base hello [autenticazione di Azure AD e gli scenari di autenticazione supportati][AAD-Auth-Scenarios].

Utilizzare hello seguendo i commenti e suggerimenti tooprovide di sezione commenti e consentono di ridefinire e definire il contenuto, incluse le richieste di nuove definizioni o aggiornare quelli esistenti.

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
