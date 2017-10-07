---
title: 'CENC con DRM multiplo e controllo di accesso: progettazione di riferimento e implementazione in Azure e in Servizi multimediali di Azure | Microsoft Docs'
description: "Informazioni su come toolicensing hello Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC con DRM multiplo e controllo di accesso: progettazione di riferimento e implementazione in Azure e in Servizi multimediali di Azure
 
## <a name="introduction"></a>Introduzione
È noto che è un toodesign attività complesse e compilare un sottosistema DRM per un OTT o streaming soluzione online. Ed è una pratica comune per toooutsource provider video online/operatori questo provider di servizi di parte toospecialized DRM. obiettivo di Hello di questo documento è toopresent un progetto di riferimento e l'implementazione del sottosistema DRM end-to-end OTT o una soluzione di flusso in linea.

i lettori di Hello di destinazione di questo documento sono ingegneri nel sottosistema DRM di OTT streaming/multi-screen soluzioni online o qualsiasi lettore interessati nel sottosistema DRM. il presupposto di Hello è che familiarità con almeno una delle tecnologie DRM hello sul mercato hello, ad esempio PlayReady, Widevine, FairPlay o accesso Adobe Reader.

DRM include anche CENC (Common Encryption) con DRM multiplo. Una tendenza principale nel flusso in linea e del settore OTT è toouse CENC con multi-native-DRM su varie piattaforme client, ovvero un turno dalla tendenza precedente di hello dell'utilizzo di un singolo DRM e il relativo client SDK per diverse piattaforme client. Quando si utilizza CENC con DRM multi-native, PlayReady sia Widevine vengono crittografati in base hello [Common Encryption (CENC ISO/IEC 23001-7)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) specifica.

vantaggi di Hello di CENC con multi-DRM sono i seguenti:

1. Riduce il costo della crittografia perché viene usata una sola elaborazione crittografica per piattaforme diverse con i DRM nativi.
2. Consente di ridurre il costo di hello di gestire gli asset crittografati poiché è necessaria una sola copia di un asset crittografato.
3. Elimina client DRM costi della licenza poiché hello native DRM client è in genere disponibile nella piattaforma nativa.

Microsoft, insieme ad alcuni dei principali leader di settore, ha promosso attivamente DASH e CENC. Servizi multimediali di Microsoft Azure ha fornito il supporto di DASH e CENC. Per gli annunci recenti, vedere i blog di Mingfei relativi all'[annuncio dell'anteprima pubblica dei servizi di distribuzione delle licenze Google Widevine in Servizi multimediali di Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/) e all'[aggiunta in Servizi multimediali di Azure del pacchetto Google Widevine per la distribuzione del flusso DRM multiplo](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Panoramica dell'articolo
obiettivo di Hello di questo articolo include seguente hello:

1. Fornire una progettazione di riferimento del sottosistema DRM usando CENC con DRM multiplo.
2. Fornire un'implementazione di riferimento nella piattaforma Microsoft Azure/Servizi multimediali di Azure.
3. Illustrare alcuni argomenti relativi alla progettazione e all'implementazione.

Nell'articolo hello, "multi-DRM" vengono trattati i seguenti hello:

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

Hello nella tabella seguente vengono riepilogate app di piattaforma nativa/nativo hello e browser supportati da ogni DRM.

| **Piattaforma client** | **Supporto DRM nativo** | **Browser/App** | **Formati di streaming** |
| --- | --- | --- | --- |
| **Smart TV, STB operatore, STB OTT** |Principalmente PlayReady e/o Widevine e/o altro |Linux, Opera, WebKit, altri |Vari formati |
| **Dispositivi Windows 10 (PC Windows, tablet Windows, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH (per HLS, PlayReady non è supportato)<br/><br/>DASH, Smooth Streaming (per HLS, PlayReady non è supportato) |
| **Dispositivi Android (telefoni, tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), client OS X e Apple TV** |FairPlay |Safari 8+/EME |HLS |


Considerando lo stato corrente di hello di distribuzione per ogni DRM, un servizio in genere consigliabile toomake DRMs tooimplement 2 o 3 che si risolve tutti i tipi di endpoint in hello migliore hello modo.

Non c'è un compromesso tra complessità hello della logica di hello del servizio e complessità hello in hello client side tooreach un certo livello di utente esperienza hello di vari client.

toomake la selezione, tenere presente questi fact:

* PlayReady viene implementato in modo nativo in tutti i dispositivi Windows e in alcuni dispositivi Android ed è disponibile tramite SDK software su praticamente qualsiasi piattaforma.
* Widevine viene implementato in modo nativo in tutti i dispositivi Android, in Chrome e in alcuni altri dispositivi.
* FairPlay è disponibile solo in iOS e nei client Mac OS o tramite iTunes.

Quindi, un DRM multiplo tipico corrisponde ai seguenti:

* Opzione 1: PlayReady e Widevine
* Opzione 2: PlayReady, Widevine e FairPlay

## <a name="a-reference-design"></a>Progettazione di riferimento
In questa sezione verrà presentata una progettazione di riferimento che è tooimplement tootechnologies agnostico utilizzato è.

Un sottosistema DRM può contenere hello seguenti componenti:

1. Gestione della chiave
2. Creazione pacchetto DRM
3. Distribuzione di licenze DRM
4. Controllo dei diritti
5. Autenticazione/autorizzazione
6. Lettore
7. Origine/rete CDN

Hello diagramma seguente viene illustrata hello elevata livello interazione tra i componenti di hello in un sottosistema DRM.

![Sottosistema DRM con CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

In Progettazione hello sono disponibili tre base "a livelli":

1. Livello back office (in nero) non esposto esternamente.
2. Livello "DMZ" (blu) che contiene tutti gli endpoint di hello affiancate pubblici.
3. Livello Internet pubblico (azzurro) contenente la rete CDN e i lettori con traffico su Internet pubblico.

Deve essere presente uno strumento di gestione del contenuto per controllare la protezione DRM, indipendentemente dal fatto che si tratti di crittografia statica o dinamica. input Hello per la crittografia DRM deve includere:

1. Contenuto video con velocità in bit multipla.
2. Chiave simmetrica.
3. URL di acquisizione delle licenze.

Durante la fase di riproduzione, flusso di livello elevato di hello è:

1. L'utente viene autenticato.
2. Token di autorizzazione viene creato per utente hello.
3. Il contenuto protetto con DRM (manifesto) viene scaricato tooplayer;
4. Giocatore invia server con ID chiave e l'autorizzazione toolicense licenze acquisizione richiesta di token.

Prima di spostare argomento successivo toohello, alcune parole su hello progettare della gestione delle chiavi.

| **Chiave simmetrica-ad-asset** | **Scenario** |
| --- | --- |
| 1-a-1 |caso più semplice Hello. Fornisce un controllo finest hello. Tuttavia, ciò comporta in genere il costo più elevato licenza recapito hello. È necessaria almeno una richiesta di licenza per ogni asset protetto. |
| 1-a-molti |È possibile utilizzare hello stesso contenuto della chiave di più risorse. Ad esempio, per tutti gli asset hello in un gruppo logico, ad esempio un genere o un sottoinsieme di genere (o film Gene), è possibile utilizzare una singola chiave simmetrica. |
| Molti-a-1 |Per ogni asset sono necessarie più chiavi simmetriche. <br/><br/>Ad esempio, se è necessario protezione CENC dinamica tooapply con multi-DRM per MPEG-DASH e la crittografia dinamica AES-128 per HLS, è necessario due chiavi di contenuto separate, ognuna con il proprio ContentKeyType. (Per chiave simmetrica hello utilizzati per la protezione CENC dinamica, ContentKeyType.CommonEncryption deve essere utilizzata, mentre per hello contenuto chiave utilizzata per la crittografia dinamica AES-128, ContentKeyType.EnvelopeEncryption deve essere utilizzata.)<br/><br/>Contenuto di un altro esempio, la protezione di trattino CENC, in teoria, una chiave simmetrica può essere utilizzato tooprotect video flusso e un altro tooprotect chiave contenuto audio. |
| Molti – troppo-molti |Combinazione di hello sopra due scenari: un set di chiavi vengono usate per ogni contenuto hello più asset in hello stesso asset "gruppo di". |

Un altro fattore importante tooconsider è utilizzare hello di licenze permanenti e non persistente.

Perché queste considerazioni sono importanti?

Hanno recapito toolicense impatto diretto costo se si utilizza cloud pubblico per il recapito di licenza. Si consideri hello seguenti due tooillustrate di casi di progettazione diverse:

1. Sottoscrizione mensile: usare una licenza persistente e il mapping chiave simmetrica-ad-asset 1-a-molti. Ad esempio, per tutti i filmati bambini hello, utilizziamo una singola chiave simmetrica per la crittografia. In questo caso:

    N. totale di licenze richieste per tutti i film per bambini/dispositivo = 1
2. Sottoscrizione mensile: usare una licenza non persistente e il mapping 1-a-1 tra la chiave simmetrica e l'asset. In questo caso:

    N. totale di licenze richieste per tutti i film per bambini/dispositivo = [n. di film guardati] x [n. di sessioni]

Come è possibile visualizzare facilmente, hello due diverse progettazioni comportare licenza molto diverso richiedere modelli pertanto il recapito di licenza dei costi se il servizio di recapito licenza viene fornito da un cloud pubblico, ad esempio servizi multimediali di Azure.

## <a name="mapping-design-tootechnology-for-implementation"></a>Mapping tootechnology di progettazione per l'implementazione
Successivamente, vengono mappate tootechnologies la struttura generica sulla piattaforma Microsoft Azure/Azure Media Services, specificando quali toouse di tecnologia per ogni blocco di compilazione.

Hello nella tabella seguente viene illustrato il mapping di hello:

| **Blocco predefinito** | **Technology** |
| --- | --- |
| **Lettore** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **Provider di identità (IdP)** |Azure Active Directory |
| **Servizio token di sicurezza** |Azure Active Directory |
| **Flusso di lavoro protezione DRM** |Protezione dinamica di Servizi multimediali di Azure |
| **Distribuzione di licenze DRM** |1. Distribuzione delle licenze di Servizi multimediali di Azure (PlayReady, Widevine, FairPlay) o <br/>2. Server licenze Axinom, <br/>3. Server licenze PlayReady personalizzato |
| **Origine** |Endpoint di streaming di Servizi multimediali di Azure |
| **Gestione della chiave** |Non necessaria per l'implementazione di riferimento |
| **Gestione del contenuto** |Applicazione console in C# |

In altre parole, sia il provider di identità (IdP) che il servizio token di sicurezza saranno Azure AD. Come lettore si userà l' [API di Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). Sia Servizi multimediali di Azure che Azure Media Player supportano DASH e CENC con DRM multiplo.

Hello seguente diagramma illustra hello struttura e il flusso generale con hello sopra il mapping di tecnologia.

![CENC in AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

In tooset di ordine di crittografia CENC dinamica, lo strumento di gestione dei contenuti hello utilizzerà hello seguenti input:

1. Contenuto aperto.
2. Chiave simmetrica dalla generazione/gestione delle chiavi.
3. URL di acquisizione delle licenze.
4. Un elenco di informazioni da Azure AD.

output di Hello dello strumento di gestione dei contenuti hello sarà:

1. ContentKeyAuthorizationPolicy contenente hello specifica in modo recapito licenza verifica specifiche di licenza DRM; e un token JWT
2. AssetDeliveryPolicy contenente le specifiche sul formato di streaming, sulla protezione DRM e sugli URL di acquisizione delle licenze.

Durante la fase di esecuzione, il flusso di hello è come di seguito:

1. Durante l'autenticazione utente, viene generato un token JWT.
2. Una delle attestazioni hello contenute nel token JWT hello è attestazione "groups" contenente l'ID di oggetto gruppo hello di "EntitledUserGroup". Questa attestazione verrà usata per superare il controllo "entitlement check".
3. Manifesto di client Windows Media Player download di un CENC contenuto protetto e "Visualizza" seguente hello:

   1. ID chiave.
   2. il contenuto di Hello è CENC protetto,
   3. URL di acquisizione delle licenze.
4. Windows Media Player effettua una richiesta di acquisizione della licenza basata su browser/DRM di hello è supportato. ID e hello JWT di richiesta di acquisizione licenza hello, chiave token è inoltre possibile avviare. Il servizio di distribuzione di licenze verificherà token JWT hello e attestazioni hello contenute prima di rilasciare hello necessaria licenza.

## <a name="implementation"></a>Implementazione
### <a name="implementation-procedures"></a>Procedure di implementazione
implementazione di Hello includerà hello alla procedura seguente:

1. Preparare l'asset di test: codificare/creazione pacchetto di un test toomulti-velocità in bit video frammentato MP4 in servizi multimediali di Azure. Questo asset NON è protetto da DRM. La protezione DRM verrà applicata più avanti con la protezione dinamica.
2. Creare l'ID chiave e la chiave simmetrica (facoltativamente dal seme chiave). In questo caso, non è necessario un sistema di gestione delle chiavi perché viene usato un solo set di ID chiave e chiave simmetrica per un paio di asset di test.
3. Utilizzare API AMS tooconfigure multi-DRM licenza servizi per la distribuzione per asset test hello. Se si utilizza il server licenze personalizzati dall'azienda o fornitori della società anziché servizi di licenza in servizi multimediali di Azure, è possibile ignorare questo passaggio e specificare gli URL di acquisizione licenza nel passaggio hello per la configurazione di recapito di licenza. API di sistema AMS è necessario toospecify dettagliate alcune configurazioni, ad esempio restrizione dei criteri di autorizzazione, licenza modelli di risposta per diversi servizi di licenza DRM e così via. In questo momento, hello portale di Azure non ancora fornire hello necessari dell'interfaccia utente per questa configurazione. Le info relative all'API e il codice di esempio sono disponibili nel documento di Julia Kornich: [Uso della crittografia comune dinamica PlayReady e/o Widevine](media-services-protect-with-drm.md).
4. Utilizzare criteri di distribuzione di API AMS tooconfigure asset per asset test hello. Le info relative all'API e il codice di esempio sono disponibili nel documento di Julia Kornich: [Uso della crittografia comune dinamica PlayReady e/o Widevine](media-services-protect-with-drm.md).
5. Creare e configurare un tenant di Azure Active Directory in Azure.
6. Creare alcuni gruppi e account utente nel tenant di Azure Active Directory: è necessario creare almeno "EntitledUser" e aggiungere un gruppo di utenti toothis. Gli utenti di questo gruppo verranno passato il controllo sui diritti acquisizione della licenza e gli utenti non di questo gruppo non supererà il controllo di autenticazione toopass e non sarà in grado di tooacquire alcuna licenza. Un membro del gruppo "EntitledUser" è un'attestazione "groups" necessario nel token JWT hello emesso da Azure AD. Questo requisito di attestazione deve essere specificato nel passaggio relativo alla configurazione dei servizi di distribuzione di licenze con DRM multiplo.
7. Creare un'app MVC ASP.NET che ospiterà il lettore video. Questa applicazione ASP.NET sarà protetti con l'autenticazione utente nel tenant di Azure Active Directory hello. Attestazioni appropriate verranno inclusi nei token di accesso hello ottenuto dopo l'autenticazione utente. Per questo passaggio, è consigliata l'API OpenID Connect. È necessario hello tooinstall pacchetti NuGet seguenti:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. Creare un lettore usando l' [API di Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). [API di Azure Media Player ProtectionInfo](http://amp.azure.net/libs/amp/latest/docs/) consente toospecify quali toouse tecnologia DRM su piattaforma DRM diversa.
9. Testare la matrice:

| **DRM** | **Browser** | **Risultato per un utente idoneo** | **Risultato per un utente non idoneo** |
| --- | --- | --- | --- |
| **PlayReady** |MS Edge o IE11 in Windows 10 |Succeed |Fail |
| **Widevine** |Chrome in Windows 10 |Succeed |Fail |
| **FairPlay** |Da definire | | |

George Trifonov del team di Servizi multimediali di Azure ha scritto un blog con i passaggi dettagliati per configurare Azure Active Directory per un'app lettore ASP.NET MVC: [Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George ha scritto anche un blog relativo all' [autenticazione di token JWT in Servizi multimediali di Azure e alla crittografia dinamica](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). Qui invece è disponibile il suo [esempio di integrazione di Azure AD con la distribuzione delle chiavi di Servizi multimediali di Azure](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Per informazioni su Azure Active Directory:

* Le informazioni per gli sviluppatori sono disponibili nella [Guida per gli sviluppatori di Azure Active Directory](../active-directory/active-directory-developers-guide.md).
* Le informazioni per gli amministratori sono disponibili in [Amministrare la directory di Azure AD](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Problematiche di implementazione
Esistono alcuni problemi"" nell'implementazione di hello. Probabilmente seguente elenco di "trucchi" hello consentono la risoluzione dei problemi nel caso in cui si verifichino problemi.

1. L'URL dell'**autorità di certificazione** deve terminare con **"/"**.  

    **Gruppo di destinatari** deve essere hello ID client dell'applicazione di Windows Media player e aggiungere anche **"/"** alla fine di hello dell'URL dell'autorità di certificazione hello.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    In [JWT decodificatore](http://jwt.calebb.net/), dovrebbe essere **aud** e **iss** come indicato di seguito nel token JWT hello:

    ![Primo trabocchetto](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Aggiungere l'applicazione toohello autorizzazioni in AAD (nella scheda Configura dell'applicazione hello). Questa operazione è obbligatoria per ogni applicazione (versioni locali e distribuite).

    ![Secondo trabocchetto](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Utilizzare hello destra dell'autorità di certificazione nella configurazione della protezione CENC dinamica:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    Hello segue non funzionerà:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Hello GUID è l'ID del tenant hello AAD. Hello GUID è reperibile nella finestra popup di endpoint nel portale di Azure.
4. Concedere i privilegi delle attestazioni di appartenenza al gruppo. Assicurarsi che nel file manifesto dell'applicazione AAD, abbiamo seguente hello

    "groupMembershipClaims": "All", (valore predefinito di hello è null)
5. Impostare l'oggetto TokenType appropriato quando si creano i requisiti relativi alle restrizioni.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Poiché l'aggiunta del supporto di JWT (AAD) inoltre tooSWT (ACS), predefinito hello TokenType è TokenType.JWT. Se si usa SWT/ACS, è necessario impostare tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Argomenti aggiuntivi per l'implementazione
Verranno ora illustrati alcuni argomenti aggiuntivi sulla progettazione e l'implementazione.

### <a name="http-or-https"></a>HTTP o HTTPS?
applicazione di Windows Media player ASP.NET MVC è compilate Hello deve supportare seguente hello:

1. Autenticazione degli utenti tramite Azure AD che deve toobe in HTTPS.
2. Scambio di token JWT tra client e Azure AD che deve toobe in HTTPS.
3. Acquisizione della licenza DRM dal client hello che è necessario toobe in HTTPS se il recapito di licenza viene fornito da servizi multimediali di Azure. Naturalmente, la famiglia di prodotti PlayReady non obbliga a usare HTTPS per la distribuzione delle licenze. Se il server delle licenze PlayReady non rientra nei Servizi multimediali di Azure, usare HTTP o HTTPS.

Pertanto, hello applicazione player ASP.NET verrà utilizzato HTTPS come procedura consigliata. Ciò significa hello che Azure Media Player verranno eseguite su una pagina in HTTPS. Tuttavia, per lo streaming preferiamo HTTP, è necessario pertanto tooconsider problema contenuto misto.

1. Il browser non consente il contenuto misto, ma lo consentono i plug-in come Silverlight e il plug-in OSMF per Smooth e DASH. Contenuto misto è un problema di sicurezza, in scadenza toohello minaccia di hello possibilità tooinject JS dannosi che possono causare hello toobe dati cliente a rischio.  Browser blocca questa operazione per impostazione predefinita e finora hello solo modo toowork intorno a esso è sul lato server (origine) hello tooallow tutti i domini (indipendentemente dal fatto che https o http). ma probabilmente nemmeno questa è una buona idea.
2. È consigliabile evitare il contenuto misto: entrambi devono usare HTTP o HTTPS. Quando gestisce il contenuto misto, la tecnologia silverlightSS richiede la cancellazione di un avviso di contenuto misto. La tecnologia flashSS gestisce il contenuto misto senza avvisi di contenuto misto.
3. Se l'endpoint di streaming è stato creato prima di agosto 2014, non supporterà HTTPS. In questo caso, creare e usare un nuovo endpoint di streaming per HTTPS.

Nell'implementazione di riferimento hello, per il contenuto protetto con DRM, applicazione e il flusso saranno in HTTTPS. Per aprire contenuto, Windows Media player hello non è necessario l'autenticazione o licenza, in modo che sia hello liberty toouse HTTP o HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Rollover della chiave per la firma di Azure Active Directory
Si tratta di un tootake punto importante in considerazione dell'implementazione. Se non si considerano nell'implementazione, il sistema hello completato infine smetteranno di funzionare completamente all'interno di al massimo 6 settimane.

Azure AD Usa trust tooestablish standard di settore tra l'elemento e le applicazioni con Azure AD. In particolare, Azure AD usa una chiave per la firma costituita da una coppia di chiavi pubblica e privata. Quando Azure AD crea un token di sicurezza che contiene informazioni sull'utente hello, questo token viene firmato da Azure AD usando la relativa chiave privata prima di inviarlo applicazione toohello indietro. tooverify che hello token sia valido e provenga effettivamente da Azure AD, un'applicazione hello deve convalidare hello firma tramite la chiave pubblica hello esposta da Azure AD che è contenuto nel documento di metadati di federazione del tenant hello. Questa chiave pubblica e hello chiave da cui deriva la firma, è hello identico a quello utilizzato per tutti i tenant di Azure AD.

Informazioni dettagliate sul rollover della chiave di Azure AD possono essere trovato nel documento hello: [informazioni importanti sul Rollover della chiave di firma in Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Tra hello [coppia di chiavi pubblica / privata](https://login.microsoftonline.com/common/discovery/keys/),

* la chiave privata di Hello viene utilizzata da Azure Active Directory toogenerate un token JWT.
* la chiave pubblica di Hello viene utilizzata da un'applicazione, ad esempio servizi di recapito licenza DRM in token JWT di AMS tooverify hello;

Per motivi di sicurezza, Azure Active Directory fa girare questo certificato periodicamente (ogni 6 settimane). In caso di violazioni della sicurezza, rollover della chiave hello può verificarsi a qualsiasi momento. Pertanto, servizi di recapito hello licenza nel sistema AMS necessario tooupdate hello della chiave pubblica utilizzata come Azure AD ruota coppia di chiavi hello, in caso contrario l'autenticazione token nel sistema AMS non riuscirà e non verrà generata alcuna licenza.

Questo risultato viene ottenuto impostando TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument quando si configurano i servizi di distribuzione delle licenze DRM.

flusso di token JWT Hello è come di seguito:

1. Azure AD emetta token JWT hello con chiave privata hello corrente per un utente autenticato.
2. Quando un lettore rileva un CENC con contenuto protetto con DRM a multipla, individuerà innanzitutto token JWT hello emesso da Azure AD.
3. Windows Media player Hello invia una richiesta di acquisizione di licenza con i servizi di recapito toolicense token JWT hello in AMS;
4. servizi di recapito Hello licenza nel sistema AMS utilizzerà hello corrente o una chiave pubblica valida dal token JWT hello tooverify Azure AD prima di rilasciare le licenze.

Servizi multimediali di licenza DRM verranno sempre eseguita la verifica per hello corrente o una chiave pubblica valida da Azure AD. chiave pubblica di Hello presentata da Azure AD verrà chiave hello utilizzata per la verifica per determinare se un token JWT rilasciato da Azure AD.

Cosa accade se rollover della chiave hello avviene dopo AAD genera un token JWT ma prima di hello JWT token viene inviato da lettori tooDRM licenza servizi per la distribuzione nel sistema AMS per la verifica?

Poiché una chiave può essere eseguito il rollback in qualsiasi momento, è sempre più di una chiave pubblica valida nel documento di metadati di federazione hello disponibili. Distribuzione di licenze di servizi multimediali Azure è possibile utilizzare uno qualsiasi dei hello chiavi specificato nel documento hello, poiché una chiave può essere implementata a breve, un altro può essere relativa sostituzione e così via.

### <a name="where-is-hello-access-token"></a>In cui è hello Token di accesso?
Se si osserva come un'app web chiama un'API app in [identità applicazione con concessione di credenziali Client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), flusso di autenticazione hello è come di seguito:

1. Un utente ha effettuato l'accesso tooAzure AD nell'applicazione web hello (vedere hello [tooWeb Web Browser applicazione](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. endpoint di autorizzazione Hello Azure AD reindirizza l'applicazione client toohello indietro hello utente agente con un codice di autorizzazione. agente utente Hello restituisce l'URI di reindirizzamento dell'applicazione di autorizzazione codice toohello client.
3. un'applicazione web Hello deve tooacquire un token di accesso in modo che possa autenticare toohello web API e recuperare la risorsa hello desiderato. In questo modo l'endpoint token tooAzure una richiesta di AD, fornendo credenziali hello, ID client e URI ID applicazione dell'API web. Presenta tooprove codice di autorizzazione hello che hello utente ha acconsentito.
4. Azure AD autentica l'applicazione hello e restituisce un token di accesso JWT usato toocall hello web API.
5. Su HTTPS, un'applicazione web hello Usa hello restituito hello tooadd token di accesso JWT stringa JWT con una designazione "Bearer" nell'intestazione di autorizzazione hello API Web di toohello richiesta hello. API web Hello quindi convalida token JWT hello e se la convalida ha esito positivo, restituisce hello desiderato di risorse.

In questo flusso di "application identity", API web hello trust utente autenticato hello hello applicazione web. Per questo motivo il modello è definito sottosistema attendibile. Hello [diagramma in questa pagina](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) viene descritto come codice di autorizzazione è consentire il funzionamento del flusso.

Acquisizione licenza con restrizione token, ci stiamo seguente hello stesso modello di sottosistema attendibile. E servizio di recapito hello licenze in servizi multimediali di Azure è risorsa API web hello, hello "back-end resource" un'applicazione web deve tooaccess. Pertanto, dove è il token di accesso di hello?

In realtà il token di accesso viene ottenuto da Azure AD. Al termine dell'autenticazione utente, viene restituito il codice di autorizzazione. codice di autorizzazione Hello viene quindi utilizzato, insieme alle app e l'ID chiave client, tooexchange di token di accesso. E token di accesso hello è per l'accesso a un'applicazione di "puntatore" che punta oppure rappresentano servizio di distribuzione di licenze di servizi multimediali di Azure.

È necessario tooregister e configurare app "puntatore" hello in Azure AD eseguendo hello procedura seguente:

1. Nel tenant di hello Azure AD

   * aggiungere un'applicazione (risorsa) con l'URL di accesso:

   https://[nome_risorsa].azurewebsites.net/ e

   * l'URL dell'ID app:

   https://[nome_tenant_aad].onmicrosoft.com/[nome_risorsa];
2. Aggiungere una nuova chiave per l'app risorse hello;
3. Aggiornare i file manifesto dell'applicazione hello in modo che disponga di proprietà groupMembershipClaims hello hello il valore seguente: "groupMembershipClaims": "All",  
4. Nell'app di Azure AD hello verso toohello lettore web app, nella sezione hello "autorizzazioni tooother applicazioni", aggiungere hello risorsa app che è stato aggiunto nel passaggio 1 sopra. In "Autorizzazioni delegate" selezionare la casella di controllo "Accedi a [nome_risorsa]". In questo modo dell'autorizzazione dell'app web hello toocreate i token di accesso per l'accesso alle app risorse hello. Eseguire questa operazione sia locali che distribuite versione di hello web app se si sviluppa con app web di Visual Studio e Azure.

Pertanto, token JWT hello emesso da Azure AD è effettivamente i token di accesso hello per accedere alla risorsa di tipo "puntatore".

### <a name="what-about-live-streaming"></a>Come funziona lo streaming live?
In hello precedente, la discussione si occupa della asset su richiesta. Come funziona lo streaming live?

Hello buone notizie sono che è possibile utilizzare esattamente hello stessa progettazione e implementazione per la protezione di streaming in tempo reale in servizi multimediali di Azure, considerando asset hello associata a un programma come "asset VOD".

In particolare, è noto che toodo live streaming con servizi multimediali di Azure, è necessario toocreate un canale, quindi un programma in canale hello. programma hello toocreate, è necessario un asset che conterrà l'archivio in tempo reale di hello per programma hello toocreate. In ordine tooprovide CENC con protezione multi-DRM contenuto hello in tempo reale, è sufficiente, toodo è tooapply hello stesso programma di installazione o l'elaborazione dei toohello asset come se fosse un asset"VOD" prima di avviare il programma hello.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Come funzionano i server licenze al di fuori di Servizi multimediali di Azure?
I clienti spesso investono in una farm di server licenze nel proprio data center o ospitata da provider di servizi DRM. Fortunatamente, la protezione del contenuto di Azure Media Services consente toooperate in modalità ibrida: contenuto ospitato e protetti in modo dinamico in servizi multimediali di Azure, mentre le licenze DRM vengono recapitate dal server all'esterno di servizi multimediali di Azure. In questo caso, esistono hello seguenti considerazioni di modifiche:

1. Hello servizio Token di sicurezza esigenze tooissue i token che sono accettabili e possono essere verificati dalla farm di server licenze hello. Ad esempio, i server delle licenze Widevine hello fornito da Axinom richiede un token JWT specifico che contiene "messaggio il diritto". Pertanto, è necessario toohave tooissue un servizio token di sicurezza tali token JWT. gli autori di Hello hanno completato un'implementazione di questo tipo e sono disponibili dettagli hello hello seguente documento in [Centro documentazione di Azure](https://azure.microsoft.com/documentation/): [toodeliver Axinom utilizzando Widevine licenze di servizi multimediali tooAzure](media-services-axinom-integration.md).
2. Non è più necessario tooconfigure servizio di recapito licenza (ContentKeyAuthorizationPolicy) in servizi multimediali di Azure. È necessario toodo è l'URL di acquisizione licenza hello tooprovide (per PlayReady, Widevine e FairPlay) quando si configura AssetDeliveryPolicy nell'impostazione CENC con multi-DRM.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>Cosa accade se si desidera toouse un servizio token di sicurezza personalizzato?
Potrebbe esserci una serie di motivi che un cliente può scegliere toouse un STS personalizzato (servizio Token di sicurezza) per fornire i token JWT. Eccone alcuni:

1. Provider di identità (IDP) utilizzato dal cliente hello Hello non supporta servizio token di sicurezza. In questo caso un servizio token di sicurezza personalizzato può essere una soluzione.
2. cliente Hello potrebbe essere necessario controllo più flessibile o una stretta integrazione servizio token di sicurezza con server di sottoscrizione del cliente sistema di fatturazione. Ad esempio, un operatore MVPD può offrire più pacchetti di sottoscrittore OTT come premium, basic, sport, operatore hello e così via. potrebbe essere toomatch hello attestazioni in un token con il pacchetto di un sottoscrittore in modo che solo contenuto nel pacchetto corretto hello viene reso disponibile. In questo caso, un servizio token di sicurezza personalizzata fornisce hello necessari flessibilità e controllo.

Due modifiche necessario toobe apportate quando si utilizza un servizio token di sicurezza personalizzato:

1. Quando si configura il servizio di recapito licenze per un asset, è necessario chiave di sicurezza hello toospecify utilizzata per la verifica dal servizio token personalizzata hello (ulteriori dettagli di seguito) anziché la chiave corrente di hello da Azure Active Directory.
2. Quando viene generato un token JTW, anziché la chiave privata di hello del certificato X509 corrente hello in Azure Active Directory viene specificata una chiave di sicurezza.

Esistono due tipi di chiavi di sicurezza:

1. Chiave simmetrica: hello stessa chiave verrà usata per la generazione e la verifica di un token JWT.
2. Chiave asimmetrica: una coppia di chiavi pubblica / privata in un certificato viene usato con la chiave privata per la crittografia o la generazione di un JWT hello e token di chiave pubblica per verifica token hello di X509.

#### <a name="tech-note"></a>Nota tecnica
Se si utilizza .NET Framework / c# come piattaforma di sviluppo, hello X509 certificato utilizzato per la chiave di sicurezza asimmetrica deve avere una lunghezza della chiave almeno 2048. Questo è un requisito della classe hello System.IdentityModel.Tokens.X509AsymmetricSecurityKey in .NET Framework. In caso contrario, verrà generata l'eccezione seguente hello:

IDX10630: hello 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' per la firma non può essere minore di '2048' bit.

## <a name="hello-completed-system-and-test"></a>test e sistema di hello completata
Esamineremo alcuni scenari nel sistema end-to-end hello completata in modo che i lettori possono avere un' "immagine" del comportamento di hello basic prima di ottenere un account di accesso.

Hello applicazione web di Windows Media player e del relativo account di accesso sono disponibili [qui](https://openidconnectweb.azurewebsites.net/).

Se è necessario è "non integrata" scenario: risorse video ospitati in servizi multimediali di Azure che sono uno non protetto o protetto DRM ma senza l'autenticazione con token (un toowhoever di licenza con la richiesta di rilascio), è possibile eseguirne il test senza account di accesso (passando tooHTTP se il flusso di dati video su HTTP).

Se è necessario scenari end-to-end di installazione integrata: risorse video è dinamica DRM la protezione dati in servizi multimediali di Azure, con l'autenticazione del token e il token JWT viene generato da Azure AD, è necessario toologin.

### <a name="user-login"></a>Accesso utente
In ordine tootest hello end-to-end integrato sistema DRM, è necessario toohave un "account" creati o aggiunti.

Quale account?

Anche se in origine l'accesso ad Azure era consentito solo agli utenti con account Microsoft, ora è invece consentito l'accesso agli utenti di entrambi i sistemi. Questa operazione viene eseguita con tutti i trust di Azure di proprietà hello Azure AD per l'autenticazione con Azure AD autenticare gli utenti dell'organizzazione e la creazione di una relazione di federazione in cui Azure AD considera attendibile il sistema identità utente di hello Microsoft account tooauthenticate degli utenti. Di conseguenza, Azure AD è tooauthenticate in grado di account di Microsoft "guest", nonché account di Azure AD "nativo".

Poiché Azure AD considera attendibile il dominio Account Microsoft (MSA), è possibile aggiungere qualsiasi account da uno qualsiasi dei seguenti domini toohello personalizzato AD Azure hello tenant e utilizzare toologin account hello:

| **Nome di dominio** | **Dominio** |
| --- | --- |
| **Dominio del tenant di Azure AD personalizzato** |nome.onmicrosoft.com |
| **Dominio aziendale** |microsoft.com |
| **Dominio account Microsoft (MSA)** |outlook.com, live.com, hotmail.com |

È possibile contattare uno qualsiasi dei hello autori toohave un account creati o aggiunti automaticamente.

Di seguito sono riportati screenshot hello di pagine di diversi account di accesso utilizzate da diversi account di dominio.

**Account di dominio del tenant AD Azure personalizzato**: In questo caso, si vedere pagina di accesso personalizzata hello del dominio tenant hello personalizzato AD Azure.

![Account dominio del tenant di Azure AD personalizzato](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Account di dominio di Microsoft con smart card**: In questo caso si vedere pagina di accesso hello personalizzata da aziendale di Microsoft IT con l'autenticazione a due fattori.

![Account dominio del tenant di Azure AD personalizzato](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Account Microsoft (MSA)**: In questo caso, si vedere la pagina di accesso hello dell'Account Microsoft per i consumer.

![Account dominio del tenant di Azure AD personalizzato](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Uso di Encrypted Media Extensions per PlayReady
In un browser moderno con crittografati supporti le estensioni (EME) per il supporto, ad esempio i browser Internet Explorer 11 su Windows 8.1 e successive e Microsoft Edge in Windows 10, PlayReady sarà PlayReady hello DRM sottostante per EME.

![Uso di EME per PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

a causa delle tabelle dei fatti toohello tale protezione PlayReady impedisce l'uno dall'acquisizione schermo di video protetto effettua l'area di Windows Media player scuro Hello è.

Hello schermata seguente mostra i plug-in Windows Media player hello e supporto MSE/EME.

![Uso di EME per PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME in Microsoft Edge e IE 11 in Windows 10 consente di chiamare [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) sui dispositivi Windows 10 che lo supportano. PlayReady SL3000 Sblocca flusso hello del contenuto premium migliorate (4 KB, HDR, e così via) e i nuovi modelli di distribuzione di contenuti (finestra iniziale per il contenuto avanzata).

Concentrarsi sui dispositivi Windows hello: PlayReady è hello solo DRM in HW hello disponibili nei dispositivi Windows (PlayReady SL3000). Un servizio di streaming può usare PlayReady tramite EME o un'applicazione UWP e offrire una migliore qualità video usando PlayReady SL3000 anziché un altro DRM. In genere, tramite Chrome o Firefox del flusso del contenuto di 2 KB e 4 K contenuto tramite Microsoft Edge/IE11 o un'applicazione UWP in hello stesso dispositivo (a seconda delle impostazioni di servizio e nell'implementazione).

#### <a name="using-eme-for-widevine"></a>Uso di EME per Widevine
In un browser moderno grazie al supporto EME/Widevine, ad esempio Chrome 41 + in Windows 10, Windows 8.1, Mac OSX Yosemite e Chrome in Android 4.4.4, Google Widevine è hello DRM dietro EME.

![Uso di EME per Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Si noti che Widevine non impedisce di acquisire schermate da un video protetto.

![Uso di EME per Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Utenti non idonei
Se un utente non è un membro del gruppo "Utenti intitolata", hello non sarà in grado di toopass "Controlla il diritto" e il servizio licenze multi-DRM hello rifiuterà tooissue hello richiesta licenza come illustrato di seguito. Hello dettagliate descrizione è "acquisire licenze non riuscita", che è quello previsto.

![Utenti non idonei](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Esecuzione del servizio token di sicurezza personalizzato
Scenario di hello di esecuzione personalizzato Secure Token Service (STS), hello JWT verrà emesso alcun token dal servizio token di sicurezza personalizzata hello tramite chiave simmetrica o asimmetrica.

caso Hello di utilizzando la chiave simmetrica (con Chrome):

![Esecuzione del servizio token di sicurezza personalizzato](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

caso di utilizzo chiave asimmetrica tramite un X509 Hello (tramite browser moderno Microsoft) del certificato.

![Esecuzione del servizio token di sicurezza personalizzato](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

In entrambi hello sopra i casi, l'autenticazione utente mantiene invariato: hello tramite Azure AD. Hello unica differenza è che i token JWT vengono emessi da hello STS personalizzato invece di Azure AD. Naturalmente, quando si configura la protezione CENC dinamica, restrizione hello del servizio di recapito licenza specifica il tipo di hello del token JWT, la chiave simmetrica o asimmetrica.

## <a name="summary"></a>Riepilogo
In questo documento è stata illustrata la crittografia CENC con DRM nativo multiplo e il controllo di accesso tramite l'autenticazione token: la progettazione e l'implementazione con Azure, Servizi multimediali di Azure e Azure Media Player.

* Viene presentato un progetto di riferimento che contiene tutti i componenti necessari di hello in un sottosistema DRM/CENC;
* Implementazione di riferimento in Azure, Servizi multimediali di Azure e Azure Media Player.
* Vengono descritte anche alcuni argomenti partecipano hello progettazione e implementazione.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
