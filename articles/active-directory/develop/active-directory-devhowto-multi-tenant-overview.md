---
title: "aaaHow toobuild un'applicazione che può accedere qualsiasi utente di Azure AD | Documenti Microsoft"
description: Istruzioni dettagliate per la creazione di un'applicazione che consenta a un utente di accedere da qualsiasi tenant Azure Active Directory, nota anche come applicazione multi-tenant.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Come toosign in qualsiasi utente di Azure Active Directory (AD) usando hello modello di applicazione multi-tenant
Se si offrono un Software come un toomany di applicazione di servizio organizzazioni, è possibile configurare l'applicazione tooaccept accessi da un tenant di Azure AD.  In Azure AD questa operazione viene definita impostazione dell'applicazione multi-tenant.  Gli utenti in un tenant di Azure AD saranno in grado di toosign tooyour applicazione dopo il consenso toouse il proprio account con l'applicazione.  

Se si dispone di un'applicazione esistente che ha un proprio sistema di account, o supporta altri tipi di accesso da altri provider di cloud, l'aggiunta dell'accesso di Azure AD da un qualsiasi tenant è semplice. Registrare l'app, aggiungere il codice di accesso tramite OAuth2, OpenID Connect o SAML e inserire un pulsante "Accedi con Microsoft" all'applicazione. Fare clic su hello seguente pulsante toolearn ulteriori informazioni sulla personalizzazione dell'applicazione.

[![Pulsante di accesso][AAD-Sign-In]][AAD-App-Branding]

Questo articolo presuppone che l'utente abbia già familiarità con la creazione di un'applicazione single-tenant per Azure AD.  Se non si testa il backup toohello [home page di Guida per sviluppatori] [ AAD-Dev-Guide] e provare a uno dei nostri introduttive!

Esistono quattro semplici passaggi tooconvert l'applicazione in un'app multi-tenant di Azure AD:

1. Aggiornare applicazione registrazione toobe multi-tenant
2. Aggiornare il toohello /common di codice toosend richieste endpoint 
3. Aggiornare il codice toohandle più valori dell'autorità di certificazione
4. Informarsi sul consenso dell'utente e dell'amministratore e apportare le modifiche appropriate al codice

Esaminiamo in dettaglio ogni passaggio. È inoltre possibile passare direttamente troppo[questo elenco di esempi di multi-tenant][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Aggiornare il registrazione toobe multi-tenant
Per impostazione predefinita, le registrazioni di API o app Web in Azure AD sono single-tenant.  È possibile apportare la registrazione multi-tenant individuando passare hello "multi-tenant" nella pagina delle proprietà hello della registrazione dell'applicazione in hello [portale di Azure] [ AZURE-portal] e l'impostazione troppo "Yes".

Si noti inoltre, prima di effettuare un'applicazione multi-tenant, Azure AD richiede hello URI ID App toobe applicazione hello globalmente univoco. URI ID App Hello è uno dei modi hello che un'applicazione viene identificata nei messaggi di protocollo.  Per un'applicazione single-tenant, è sufficiente per hello URI ID App toobe univoco all'interno di tale tenant.  Per un'applicazione multi-tenant, deve essere globalmente univoco in modo da Azure AD è possibile trovare un'applicazione hello tra tutti i tenant.  Richiedendo hello URI ID App toohave un nome host che corrisponde a un dominio verificato del tenant di Azure AD hello, viene applicata l'univocità globale.  Ad esempio, se il nome di hello del tenant stato contoso.onmicrosoft.com valido URI ID App sarà `https://contoso.onmicrosoft.com/myapp`.  Se il tenant ha un dominio verificato `contoso.com`, l'URI ID app valido sarà `https://contoso.com/myapp`.  L'impostazione di un'applicazione come multi-tenant avrà esito negativo se hello URI ID App non segue questo modello.

Per impostazione predefinita, le registrazioni client native sono multi-tenant.  Non è necessario tootake qualsiasi toomake azione native client applicazione registrazione multi-tenant.

## <a name="update-your-code-toosend-requests-toocommon"></a>Aggiornare il codice toosend richieste troppo comuni
In un'applicazione single-tenant, le richieste di accesso vengono inviate a endpoint di accesso toohello del tenant. Ad esempio, contoso.onmicrosoft.com potrebbe essere endpoint hello:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Le richieste inviate endpoint tooa del tenant possono accedere gli utenti (o Guest) in tale tooapplications tenant nel tenant.  Con un'applicazione multi-tenant, un'applicazione hello non conosce in anticipo quale utente hello tenant è, pertanto non è possibile inviare richieste endpoint tooa del tenant.  Al contrario, le richieste vengono inviate tooan endpoint che il demultiplexing tra tenant tutti Azure Active Directory:

    https://login.microsoftonline.com/common

Quando Azure AD riceve una richiesta in hello/endpoint comune, effettua l'accesso utente hello e come una conseguenza consente di individuare quale utente hello tenant si trova.  Hello/endpoint comune funziona con tutti i protocolli di autenticazione hello è supportati da Azure AD: OpenID Connect, OAuth 2.0, SAML 2.0 e WS-Federation.

risposta di accesso toohello un'applicazione Hello quindi contiene un token che rappresenta utente hello.  valore dell'autorità emittente Hello nel token hello indica un'applicazione quale utente hello tenant da.  Quando restituisce una risposta da hello/endpoint comuni, il valore dell'autorità emittente hello nel token hello corrisponderà tenant toohello dell'utente.  È importante toonote hello/endpoint comune non è un tenant e non è un'autorità di certificazione, è semplicemente un multiplexer.  Quando si usa /common, logica hello in token toovalidate applicazione deve tootake toobe aggiornare questo conto. 

Come indicato in precedenza applicazioni multi-tenant devono anche fornire un'esperienza di accesso coerente per gli utenti, seguente hello linee guida del marchio dell'applicazione di Azure AD. Fare clic su hello seguente pulsante toolearn ulteriori informazioni sulla personalizzazione dell'applicazione.

[![Pulsante di accesso][AAD-Sign-In]][AAD-App-Branding]

Esaminiamo ora utilizzare hello di hello /common endpoint e l'implementazione del codice in modo più dettagliato.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Aggiornare il codice toohandle più valori dell'autorità di certificazione
Le applicazioni Web e le API Web ricevono e convalidano i token da Azure AD.  

> [!NOTE]
> Mentre le applicazioni client native richiedere e ricevano token da Azure AD, vengono in tal caso toosend li tooAPIs, in cui vengono convalidate.  Le applicazioni native non convalidano i token e devono gestirli come opachi.
> 
> 

Passiamo ora al modo in cui un'applicazione convalida i token ricevuti da Azure AD.  Un'applicazione single-tenant prende in genere un valore dell'endpoint come:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

e utilizzarla tooconstruct come un URL di metadati (in questo caso, OpenID Connect):

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload due importanti parti di informazioni e i token utilizzati toovalidate: firma del tenant hello chiavi e il valore dell'autorità di certificazione.  Ogni tenant di Azure AD ha un valore univoco dell'autorità di certificazione del modulo hello:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

valore GUID hello dove è hello rename-versione dell'ID tenant hello del tenant hello.  Se si fa clic sul precedente collegamento di metadati per hello `contoso.onmicrosoft.com`, è possibile visualizzare il valore dell'autorità di certificazione nel documento hello.

Quando un'applicazione single-tenant convalida un token, controlla firma hello del token di hello contro hello chiavi dal documento di metadati hello di firma. In questo modo si toomake del valore di autorità emittente che hello hello corrispondenze token hello uno che è stato trovato nel documento di metadati hello.

Poiché hello/comuni endpoint non corrisponde a tooa tenant e non è un'autorità di certificazione, quando si esamina il valore dell'autorità emittente hello nei metadati hello comune è un URL basato su modelli anziché un valore effettivo:

    https://sts.windows.net/{tenantid}/

Pertanto, un'applicazione multi-tenant non è possibile convalidare i token solo confrontando il valore dell'autorità emittente hello nei metadati hello con hello `issuer` valore nel token hello.  Un'applicazione multi-tenant deve logica toodecide i valori dell'autorità di certificazione non sono validi e che non, basata su tenant hello parte ID del valore dell'autorità emittente hello.  

Ad esempio, se un'applicazione multi-tenant consente solo accesso da un tenant specifico che hanno effettuato l'iscrizione ai servizi, quindi deve verificare il valore di autorità emittente hello o hello `tid` valore in hello token toomake tenant sia nel proprio elenco di attestazione sottoscrittori.  Se un'applicazione multi-tenant solo occupa utenti singoli e non decisioni qualsiasi accesso in base ai tenant, è possibile ignorare il valore di autorità emittente hello completamente.

Negli esempi di multi-tenant hello in hello [contenuto correlato](#related-content) sezione alla fine di hello di questo articolo, la convalida dell'autorità di certificazione è disabilitato tooenable qualsiasi toosign tenant di Azure AD in.

Ora esaminiamo esperienza utente hello per gli utenti che accedono applicazioni toomulti tenant.

## <a name="understanding-user-and-admin-consent"></a>Informazioni sul consenso dell'utente e dell'amministratore
Per un utente toosign tooan applicazione in Azure AD, l'applicazione hello deve essere rappresentata nel tenant dell'utente hello.  Ciò consente l'organizzazione hello toodo operazioni quali applicare i criteri univoci quando gli utenti dal tenant l'accesso toohello applicazione.  Per un'applicazione single-tenant, la registrazione è semplice. è hello che si verifica quando si registra un'applicazione hello in hello [portale di Azure][AZURE-portal].

Per un'applicazione multi-tenant, la registrazione iniziale per un'applicazione hello hello risiede nel tenant di Azure AD hello usato dallo sviluppatore hello.  Quando un utente da un tenant diverso accede toohello applicazione hello per la prima volta, Azure AD richiede le autorizzazioni toohello tooconsent richieste dall'applicazione hello.  Se si acconsente, quindi una rappresentazione di un'applicazione hello chiamato un *dell'entità servizio* viene creato in hello tenant dell'utente e di accesso può continuare. Viene inoltre creata una delega nella directory hello che registra l'applicazione toohello di consenso dell'utente hello. Vedere [oggetti applicazione e oggetti entità servizio] [ AAD-App-SP-Objects] per informazioni dettagliate su oggetti applicazione ed entità servizio dell'applicazione hello e come interagiscono tooeach altri.

![Applicazione toosingle a livello di consenso][Consent-Single-Tier] 

Questa esperienza di consenso è indipendente dalle autorizzazioni hello richieste dall'applicazione hello.  Azure AD supporta due tipi di autorizzazioni, delegate e solo app:

* Un'autorizzazione delegata concede un tooact possibilità di applicazione hello come utente connesso per un sottoinsieme di utenti di hello hello operazioni eseguibili.  Ad esempio, è possibile concedere un hello tooread di applicazione hello autorizzazione delegata firmato nel calendario dell'utente.
* Un'autorizzazione solo app viene concessa direttamente toohello identità dell'applicazione hello.  Ad esempio, è possibile concedere un applicazione hello autorizzazione solo app tooread hello elenco di utenti in un tenant, indipendentemente dal fatto che ha effettuato l'accesso dell'applicazione toohello.

Alcune autorizzazioni possono essere stato fornito il consenso tooby un utente normale, mentre altri richiedono il consenso dell'amministratore tenant. 

### <a name="admin-consent"></a>Consenso dell'amministratore
Le autorizzazioni solo app richiedono il consenso dell'amministratore tenant.  Se l'applicazione richiede un'autorizzazione solo app e un utente tenta di toosign toohello applicazione, verrà visualizzato un messaggio di errore indicante che l'utente di hello non è in grado di tooconsent.

Alcune autorizzazioni delegate richiedono anche il consenso dell'amministratore tenant.  Hello possibilità toowrite indietro tooAzure Active Directory come hello effettuato l'accesso utente, ad esempio, è necessario il consenso dell'amministratore tenant.  Ad esempio le autorizzazioni solo app, se un utente ordinario tenta toosign tooan applicazione che richiede un'autorizzazione delegata che richiede il consenso dell'amministratore, l'applicazione riceverà un errore.  Richiede un'autorizzazione o meno consenso dell'amministratore è determinata dallo sviluppatore hello pubblicati risorse hello e può essere disponibili nella documentazione di hello per risorsa hello.  I collegamenti che descrive le autorizzazioni disponibili hello hello API Azure AD Graph e Microsoft Graph API da cui hello tootopics [contenuto correlato](#related-content) sezione di questo articolo.

Se l'applicazione utilizza le autorizzazioni che richiedono di consenso dell'amministratore, è necessario un movimento, ad esempio un pulsante o collegamento cui salve possibile avviare l'azione di hello toohave.  richiesta di Hello inviato dall'applicazione per questa azione è una richiesta di autorizzazione OAuth2/OpenID Connect normale, ma che include anche hello `prompt=admin_consent` parametro della stringa di query.  Una volta salve ha accettato le condizioni e dell'entità servizio hello viene creato nel tenant del cliente hello, le successive richieste di accesso non è necessario hello `prompt=admin_consent` parametro. Poiché il messaggio per l'amministratore ha deciso di hello richieste le autorizzazioni sono accettabili, nessun altro utente nel tenant di hello verranno richiesto il consenso da tale punto in avanti.

Hello `prompt=admin_consent` parametro può essere utilizzato anche dalle applicazioni che richiedono le autorizzazioni che non necessitano di consenso dell'amministratore. Questa operazione viene eseguita quando l'applicazione hello richiede un'esperienza in tenant salve "effettua l'iscrizione" una volta e nessun agli utenti verrà chiesto il consenso da tale punto in.

Se un'applicazione richiede autorizzazioni di amministratore e un amministratore accede nel ma hello `prompt=admin_consent` parametro non viene inviato, salve verrà correttamente consenso all'applicazione toohello **solo per l'account utente**.  Gli utenti standard non sarà ancora in grado di toosign in e applicazione toohello consenso.  Ciò è utile se si desidera toogive hello tenant amministratore hello possibilità tooexplore l'applicazione prima di consentire l'accesso ad altri utenti.

Un amministratore tenant è possibile disabilitare il possibilità hello per tooapplications tooconsent degli utenti normali.  Se questa funzionalità è disabilitata, è sempre necessaria per toobe applicazione hello impostare nel tenant di hello consenso dell'amministratore.  Se si desidera tootest l'applicazione con il consenso utente normale disabilitato, è possibile trovare hello opzione di configurazione nel tenant di Azure AD hello sezione di configurazione di hello [portale di Azure][AZURE-portal].

> [!NOTE]
> Alcune applicazioni desidera un'esperienza in cui gli utenti normali sono in grado di tooconsent inizialmente e può implicare la successiva applicazione hello amministratore hello e richiedere le autorizzazioni che richiedono di consenso dell'amministratore.  Non è toodo alcun modo ciò con la registrazione di una singola applicazione in Azure AD oggi.  endpoint v2 Hello future Azure AD consente applicazioni toorequest autorizzazioni in fase di esecuzione, invece che al momento della registrazione, in modo da consentire questo scenario.  Per ulteriori informazioni, vedere hello [Guida per sviluppatori di Azure AD App modello v2][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Consenso e applicazioni multilivello
L'applicazione può avere più livelli, ognuno rappresentato dalla propria registrazione in Azure AD.  Un esempio è un'applicazione nativa che esegue una chiamata a un'API Web o un'applicazione Web che esegue una chiamata a un'API Web.  In entrambi i casi, hello client (app native o web) richiede autorizzazioni toocall hello risorsa (API web).  Per hello client toobe autorizzato correttamente nel tenant del cliente, tutte le risorse toowhich, richiede autorizzazioni deve esistere già nel tenant del cliente hello.  Se questa condizione non viene soddisfatta, Azure AD verrà restituito un errore che hello risorsa deve essere aggiunto per primo.

**Più livelli in un tenant singolo**

Può trattarsi di un problema se l'applicazione logica è costituita da due o più registrazioni di applicazioni, ad esempio un client e una risorsa separati.  Come ottenere risorse hello nel tenant del cliente hello prima?  Azure AD sono inclusi in questo caso abilitando client e acconsentito toobe risorse in un unico passaggio. utente Hello vede hello somma totale della autorizzazioni hello richiesto dal client hello e risorsa nella pagina di consenso hello.  tooenable questo comportamento, registrazione dell'applicazione della risorsa hello deve includere l'ID App del client hello come un `knownClientApplications` nel manifesto dell'applicazione.  ad esempio:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Questa proprietà può essere aggiornata tramite risorsa hello [manifesto dell'applicazione][AAD-App-Manifest]. Come illustrato in un client nativo multilivello chiamata di esempio di API web in hello [contenuto correlato](#related-content) sezione alla fine di hello di questo articolo. Hello diagramma seguente viene fornita una panoramica dell'autorizzazione per un'applicazione multilivello registrata in un singolo tenant:

![App client note toomulti a livello di consenso][Consent-Multi-Tier-Known-Client] 

**Più livelli in tenant multipli**

Un caso simile si verifica se livelli diversi di hello di un'applicazione vengono registrati nel tenant diversi.  Ad esempio, si consideri il caso hello di compilazione di un'applicazione client nativa che chiama hello API di Office 365 Exchange Online.  toodevelop hello nativi dell'applicazione e versioni successive per hello applicazione nativa toorun nel tenant del cliente, l'entità servizio Exchange Online hello deve essere presente.  In questo caso, hello developer e cliente deve acquistare Exchange Online per toobe dell'entità servizio hello creato nei relativi tenant.  

Nel caso di hello di un'API compilata da un'organizzazione diversa da Microsoft, hello di hello API sviluppatore tooprovide un modo per la propria applicazione hello tooconsent di clienti in tenant dei clienti. Hello consiglia di progettazione per hello 3rd party developer toobuild hello API in modo che può inoltre fungere da un client web per tooimplement iscrizione:

1. Seguire hello hello di tooensure nelle sezioni precedenti API implementa i requisiti di registrazione o codice hello applicazione multi-tenant
2. Garantisce inoltre tooexposing hello API ambiti/ruoli, registrazione di hello include hello "Accedi e Leggi il profilo utente" autorizzazione di Azure AD (fornito per impostazione predefinita)
3. Implementare una pagina di accesso-in/iscrizione nel client web hello seguente hello [consenso dell'amministratore](#admin-consent) linee guida descritte in precedenza 
4. Una volta toohello applicazione di consenso dell'utente di hello, hello servizio principale e il consenso delega vengono creati collegamenti al proprio tenant e un'applicazione nativa hello è possibile ottenere i token per hello API

Hello seguente diagramma viene fornita una panoramica dell'autorizzazione per un'applicazione multilivello registrata nel tenant diversi:

![Applicazione di più parti toomulti a livello di consenso][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Revoca del consenso
Utenti e amministratori possono revocare consenso tooyour applicazione in qualsiasi momento:

* Gli utenti revoke accesso tooindividual applicazioni rimuovendole dal loro [applicazioni del Pannello di accesso] [ AAD-Access-Panel] elenco.
* Gli amministratori revocare l'accesso tooapplications rimuovendole da Azure AD usando la sezione relativa alla gestione hello Azure AD di hello [portale di Azure][AZURE-portal].

Se un amministratore acconsente tooan applicazione per tutti gli utenti in un tenant, gli utenti non è possibile revocare singolarmente l'accesso.  Solo amministratore hello possibile revocare l'accesso e solo per l'intera applicazione hello.

### <a name="consent-and-protocol-support"></a>Supporto del consenso e dei protocolli
Consenso è supportato in Azure AD tramite hello OAuth, OpenID Connect, WS-Federation e protocolli SAML.  Hello protocolli SAML e WS-Federation non supportano hello `prompt=admin_consent` parametro, pertanto il consenso dell'amministratore è possibile solo tramite OAuth e OpenID Connect.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Applicazioni multi-tenant e memorizzazione nella cache dei token di accesso
Applicazioni multi-tenant è anche possono ottenere i token di accesso toocall API che sono protetti da Azure AD.  Un errore comune quando si utilizza hello Active Directory Authentication Library (ADAL) con un'applicazione multi-tenant, è richiesta tooinitially un token per un utente tramite /common, ricevere una risposta, quindi richiedere un token per l'utente stesso anch'esso tramite /common successive.  Poiché viene hello risposta da Azure AD da un tenant, non/comune, ADAL memorizza nella cache il token hello come proveniente da tenant hello. Hello successive chiamare tooget troppo comune o un token di accesso per la voce della cache di hello utente mancati riscontri hello e utente hello è richiesta toosign in nuovamente.  cache di hello tooavoid mancante, verificare che le successive chiamate per un utente già connesso vengono effettuate endpoint toohello del tenant.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toobuild un'applicazione che può accedere un utente di qualsiasi tenant di Azure Active Directory. Dopo l'abilitazione di Single Sign-On tra l'applicazione e Azure Active Directory, è inoltre possibile aggiornare il tooaccess applicazione API esposte dalle risorse di Microsoft, come Office 365. Pertanto è possibile offrire un'esperienza personalizzata nell'applicazione, ad esempio che mostra le informazioni contestuali toohello utenti, ad esempio le immagine del profilo o loro successivo appuntamento del calendario. toolearn più su come rendere API chiama tooAzure Active Directory e servizi Office 365 come Exchange, SharePoint, OneDrive, OneNote, Planner, Excel e altre informazioni, visitare: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Contenuti correlati
* [Esempi di applicazioni multi-tenant][AAD-Samples-MT]
* [Linee guida sulla personalizzazione per le applicazioni][AAD-App-Branding]
* [Guida per sviluppatori di Azure AD][AAD-Dev-Guide]
* [Oggetti applicazione e oggetti entità servizio][AAD-App-SP-Objects]
* [Integrazione di applicazioni con Azure Active Directory][AAD-Integrating-Apps]
* [Panoramica di hello il Framework di consenso][AAD-Consent-Overview]
* [Ambiti di autorizzazione di Microsoft API Graph][MSFT-Graph-permision-scopes]
* [Ambiti di autorizzazione di Azure AD API Graph][AAD-Graph-Perm-Scopes]

Utilizzare hello seguendo i commenti e suggerimenti tooprovide di sezione commenti e consentono di ridefinire e definire il contenuto.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














