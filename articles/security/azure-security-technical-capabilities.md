---
title: "funzionalità tecniche di sicurezza aaaAzure | Documenti Microsoft"
description: "Informazioni sui servizi di calcolo basate su cloud che includono un'ampia selezione di istanze di calcolo e i servizi che possono estendersi su e giù automaticamente toomeet hello esigenze dell'applicazione o dell'organizzazione."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Funzionalità tecniche per la sicurezza di Azure

tooassist e potenziali clienti Azure comprendere e utilizzare hello varie funzionalità correlate alla sicurezza disponibili in e circostante hello piattaforma Azure, Microsoft ha sviluppato una serie di White paper, sicurezza panoramiche, procedure consigliate, e Elenchi di controllo. intervallo di argomenti in termini di dimensioni e della complessità Hello e vengono aggiornate periodicamente. Questo documento fa parte della serie, come riepilogato nella sezione astratta hello riportata di seguito. Per altre informazioni su questa serie sulla sicurezza di Azure, vedere la pagina all'indirizzo (URL).

## <a name="azure-platform"></a>Piattaforma Azure

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) è una piattaforma cloud costituita da servizi di infrastruttura e applicazioni, con servizi dati integrati, analisi avanzata e strumenti e servizi per sviluppatori, ospitata nei data center del cloud pubblico Microsoft. I clienti utilizzare Azure per molti capacità diversi scenari e, dalla base calcolo, rete e archiviazione, toomobile e app servizi web, gli scenari di cloud di toofull ad esempio Internet of Things e possono essere utilizzati con tecnologie open source e distribuiti come ibrida il cloud o ospitato nel Data Center di un cliente. Azure offre tecnologie cloud come blocchi predefiniti toohelp società ridurre i costi, innovazione rapidamente e gestire in modo proattivo i sistemi. Quando si compila, o eseguire la migrazione di provider di cloud tooa asset IT, ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli di hello assicurano toomanage hello delle risorse basati su cloud e servizi hello.

Microsoft Azure è hello solo calcolo provider cloud che offre una piattaforma sicura, coerenti e infrastructure-as-a-service per toowork team all'interno di competenze di cloud diversi livelli di complessità del progetto, con dati integrati servizi e analitica che apre intelligence dai dati ogni volta che esiste tra piattaforme Microsoft e non Microsoft, apre strumenti, fornendo scelta per l'integrazione cloud e locali nonché la distribuzione di servizi cloud di Azure all'interno e Framework Data Center locale. Come parte di Microsoft Cloud attendibili hello, i clienti si basano su Azure leader del settore sicurezza, affidabilità, conformità, privacy e vasta rete di hello di persone, i partner e processi toosupport organizzazioni nel cloud hello.

Microsoft Azure consente di:

- Consente di accelerare innovazione con cloud hello.

- Basare le app e le decisioni aziendali su informazioni dettagliate.

- Creare con facilità e distribuire ovunque.

- Proteggere l'azienda.

## <a name="scope"></a>Scope

il punto focale Hello di questo white paper riguarda le funzionalità di sicurezza e funzionalità per il supporto componenti principali di Microsoft Azure, vale a dire [archiviazione di Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-introduction), [database SQL di Microsoft Azure](https://docs.microsoft.com/azure/sql-database/), [Il modello di macchina virtuale di Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/  ), gli strumenti per hello e infrastruttura di gestire tutto. In questo white paper concentrarsi su tooyou disponibili funzionalità tecniche di Microsoft Azure come i clienti toofulfil proprio ruolo nella protezione hello sicurezza e privacy dei propri dati.

importanza Hello di questo modello responsabilità condivisa è essenziale per i clienti che stanno spostando toohello cloud. Provider di cloud offrono notevoli vantaggi per le attività di sicurezza e conformità, ma questi vantaggi non absolve cliente hello di proteggere i relativi utenti, applicazioni e le offerte di servizio.

Per le soluzioni IaaS, cliente hello responsabile o è una responsabilità condivisa per la sicurezza e la gestione del sistema operativo hello, configurazione di rete, applicazioni, identità, i client e dati.  Compilazione di soluzioni PaaS nelle distribuzioni IaaS, cliente hello continua a essere o è una responsabilità condivisa per la protezione e gestione di applicazioni, identità, i client e dati. Per le soluzioni SaaS, Nonetheless, cliente hello continua toobe responsabile. Garantiscono che dati sia classificati correttamente e che condividono un toomanage responsabilità i relativi utenti e dispositivi endpoint.

Questo documento non fornisce dettagliati di uno qualsiasi dei hello relativi componenti della piattaforma Microsoft Azure, ad esempio siti Web di Azure, Azure Active Directory, HDInsight, servizi multimediali e altri servizi che sono disposti sopra i componenti di base hello. Nonostante venga offerto un livello minimo di informazioni generali, si presuppone che i lettori abbiano familiarità con i concetti di base di Azure descritti in altri documenti di riferimento forniti da Microsoft e inclusi nei collegamenti disponibili in questo white paper.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Responsabilità di utente (Customer) di sicurezza disponibili funzionalità tecniche toofulfil - quadro generale

Microsoft Azure offre servizi che consentono ai clienti di soddisfano esigenze di conformità, privacy e sicurezza hello. Hello seguenti immagine consente di spiegano i vari servizi di Azure disponibili per gli utenti toobuild un'infrastruttura di applicazioni protetti e conformi in base a standard di settore.

![Funzionalità tecniche per la sicurezza disponibili: quadro generale](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Gestire e controllare le identità e l'accesso degli utenti (protezione)

Azure consente di proteggere informazioni personali e aziendali, consentendo di identità utente toomanage e le credenziali e controllare l'accesso.

### <a name="azure-active-directory"></a>Azure Active Directory

Identità e accessi Gestione soluzioni Guida di Microsoft IT proteggere tooapplications di accesso e le risorse tra data center aziendale hello e nel cloud hello, abilitando livelli aggiuntivi di convalida, ad esempio multi-factor authentication e condizionale criteri di accesso. Il monitoraggio delle attività sospette tramite funzioni avanzate di report di sicurezza, controllo e avvisi consente di attenuare i potenziali problemi di sicurezza. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) fornisce single sign-on toothousands le app cloud (SaaS) e l'accesso tooweb App eseguite in locale.

Vantaggi di sicurezza di Azure Active Directory (AD) includono il possibilità hello di:

- Creare e gestire una singola identità per ogni utente in un'azienda ibrida, mantenendo sincronizzati utenti, gruppi e dispositivi.

- Fornire l'accesso single sign-on tooyour applicazioni tra migliaia di applicazioni SaaS preintegrate.

- Abilitare la sicurezza dell'accesso alle applicazioni grazie all'autenticazione a più fattori basata su regole per applicazioni locali e cloud.

- Accesso remoto sicuro di provisioning tooon locale delle applicazioni mediante il Proxy di applicazione AD Azure web.

Il [portale di Azure Active Directory](http://aad.portal.azure.com/) è disponibile nell'ambito del portale di Azure. Da questo dashboard, è possibile ottenere una panoramica dello stato di hello dell'organizzazione e approfondire facilmente la gestione delle directory hello, utenti o accesso dell'applicazione.

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Di seguito sono illustrate le funzionalità principali di gestione delle identità di Azure:

- Single sign-on

- Autenticazione a più fattori

- Monitoraggio della sicurezza, avvisi e report basati su Machine Learning

- Gestione delle identità e dell'accesso degli utenti

- Registrazione del dispositivo

- Privileged Identity Management

- Identity Protection

#### <a name="single-sign-on"></a>Single sign-on

[Accesso Single sign-on (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) si intende tooaccess in grado di tutte le applicazioni di hello e risorse che toodo business, è necessario l'accesso una sola volta utilizzando un unico account utente. Una volta effettuato l'accesso, è possibile accedere a tutte le applicazioni hello è necessario senza essere tooauthenticate necessari (ad esempio, digitare una password) un secondo momento.

Molte organizzazioni si basano su applicazioni software come un servizio (SaaS), come Office 365, Box e Salesforce, per la produttività degli utenti finali. In passato, tooindividually necessario personale IT di creare e aggiornare gli account utente in ciascuna applicazione SaaS e gli utenti dovevano tooremember una password per ogni applicazione SaaS.

[Azure AD estende Active Directory locale al cloud hello](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), l'abilitazione della loro primario organizzativa toouse utenti account toonot solo accesso tootheir dominio dispositivi e risorse aziendali, ma anche tutti hello web e applicazioni SaaS per il proprio lavoro.

Non solo gli utenti, non toomanage più set di nomi utente e password, accesso all'applicazione può essere automaticamente sottoposto a provisioning o deprovisioning in base ai gruppi organizzativi e lo stato di un dipendente. [Azure AD vengono presentati i controlli di governance di accesso e protezione](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) che consentono di toocentrally gestire l'accesso degli utenti tra le applicazioni SaaS.

#### <a name="multi-factor-authentication"></a>Autenticazione a più fattori

[Azure multi-factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) è un metodo di autenticazione che richiede l'uso di hello di più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni. [MFA contribuisce a salvaguardare](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) accedere toodata e alle applicazioni rispettando richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite diverse opzioni di verifica, ad esempio una telefonata, un SMS, una notifica o un codice di verifica dell'app per dispositivi mobili e token OAuth di terze parti.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Monitoraggio della sicurezza, avvisi e report basati su Machine Learning

Monitoraggio della sicurezza, avvisi e report basati su Machine Learning che identificano i modelli di accesso non coerenti per contribuire alla protezione dell'azienda. È possibile utilizzare l'accesso di Azure Active Directory e utilizzo report toogain visibilità hello integrità e sicurezza della directory dell'organizzazione. Con queste informazioni, un amministratore di directory possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.

Nel portale di Azure classico hello o tramite [portale di Azure Active directory](http://aad.portal.azure.com/), [report](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) sono classificati in hello seguenti modi:

- Report anomalie: includono eventi che è stato rilevato toobe anomali di accesso. L'obiettivo è toomake si è consapevoli di tale attività e consentono di toobe toodecide in grado di indicano se un evento è sospetto.

- Report applicazioni integrate: offrono informazioni dettagliate sull'uso delle applicazioni cloud nell'organizzazione. Azure Active Directory offre l'integrazione con migliaia di applicazioni cloud.

- Report errori: indicano errori che possono verificarsi durante il provisioning di applicazioni tooexternal account.

- Report specifici dell'utente: visualizzano i dati del dispositivo/dell'attività di accesso per un utente specifico.

- Log attività: include un record di tutti gli eventi controllati entro hello ultime 24 ore, ultimi 7 giorni, o ultimi 30 giorni e modifiche dell'attività di gruppo e attività di registrazione e di reimpostazione della password.

#### <a name="consumer-identity-and-access-management"></a>Gestione delle identità e dell'accesso degli utenti

[Azure B2C Directory attiva](https://azure.microsoft.com/services/active-directory-b2c/) è un servizio di gestione di identità globale, a disponibilità elevata per le applicazioni per consumatori che viene ridimensionata toohundreds di milioni di valori Identity. Il servizio può essere integrato tra piattaforme mobili e Web. Il consumer può accedere tooall le applicazioni attraverso esperienze di personalizzabile tramite gli account di social networking esistenti o creando nuove credenziali.

In hello precedenti, gli sviluppatori di applicazioni che volevano troppo[iscriversi e accesso degli utenti](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) nelle relative applicazioni sarebbe stato necessario scrivere il proprio codice. E si sarebbe usato locale database o i sistemi toostore nomi utente e password. Azure B2C Directory attiva offre organizzazione una migliore gestione identità consumer di toointegrate modo nelle applicazioni con supporto hello di una piattaforma sicura, basato su standard e un ampio set di criteri estendibili.

Con Azure Active Directory B2C, gli utenti possono registrarsi alle applicazioni usando gli account di social networking esistenti (Facebook, Google, Amazon, LinkedIn) o creando nuove credenziali (indirizzo di posta elettronica e password o nome utente e password).

Registrazione del dispositivo

[Registrazione dispositivo di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) è hello base basata su dispositivi [accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) scenari. Quando un dispositivo viene registrato, registrazione dispositivo Azure Active Directory fornisce dispositivo hello con un'identità che è usato tooauthenticate hello quando hello utente accede. dispositivo Hello autenticato e gli attributi di hello del dispositivo hello, possono quindi essere tooenforce utilizzato Criteri di accesso condizionale per le applicazioni ospitate nel cloud hello e locale.

In combinazione con un [gestione dei dispositivi mobili (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) soluzione, ad esempio Intune, sugli attributi del dispositivo hello in Azure Active Directory sono stati aggiornati con informazioni aggiuntive sul dispositivo di hello. Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità.

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) consente di gestire, controllare e monitorare le identità privilegiate e accedere tooresources in Azure AD, così come altri servizi online Microsoft come Office 365 o Microsoft Intune.

In alcuni casi gli utenti devono toocarry operazioni privilegiate in risorse di Azure o Office 365 o altre applicazioni SaaS. Questo spesso significa che le organizzazioni possono toogive di accesso con privilegi permanenti usarle in Azure AD. Questo rappresenta un rischio di sicurezza crescente per le risorse ospitate nel cloud poiché le organizzazioni non sono in grado di monitorare completamente le operazioni eseguite dagli utenti con i privilegi amministrativi. Inoltre, se un account utente con accesso privilegiato è compromesso, tale singola violazione può compromettere la sicurezza dell'intero cloud. Azure AD Privileged Identity Management consente tooresolve questo rischio.

Azure AD Privileged Identity Management consente di effettuare le operazioni seguenti:

- Individuare gli utenti amministratori di Azure AD

- Abilitare le connessioni, "just in time" accesso amministrativo tooMicrosoft Online Services quali Office 365 e Intune

- Ottenere report sulla cronologia degli accessi degli amministratori e sulle modifiche alle assegnazioni degli amministratori

- Ottenere avvisi relativi al ruolo con privilegi di accesso tooa

#### <a name="identity-protection"></a>Identity Protection

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) è un servizio di sicurezza che offre una visualizzazione consolidata degli eventi di rischio e delle potenziali vulnerabilità che interessano le identità dell'organizzazione. Identity Protection usa le funzionalità esistenti di rilevamento anomalie di Azure Active Directory, disponibili tramite i report Anomalie dell'attività di Azure AD, e introduce nuovi tipi di eventi di rischio che consentono di rilevare le anomalie in tempo reale.

## <a name="secured-resource-access-in-azure"></a>Accesso protetto alle risorse in Azure

La fatturazione costituisce il punto di partenza per il controllo di accesso in Azure. proprietario Hello di un account Azure, accedere visitando hello [centro account Azure](https://account.windowsazure.com/subscriptions), è hello amministratore dell'account. Le sottoscrizioni sono un contenitore per la fatturazione, ma vengono utilizzate anche come limite di sicurezza: ogni sottoscrizione dispone di un servizio amministratore (SA) che è possibile aggiungere, rimuovere e modificare le risorse di Azure nella sottoscrizione specificata mediante hello [portale di Azure classico](https://manage.windowsazure.com/). hello è Hello predefinito SA di una nuova sottoscrizione, ma hello AA modificabili SA hello in hello centro account Azure.

![Accesso protetto alle risorse in Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Le sottoscrizioni dispongono anche di un'associazione a una directory. directory Hello definisce un set di utenti. Può trattarsi di utenti da hello aziendale o dell'istituto di istruzione che ha creato la directory hello o possono essere utenti esterni (vale a dire Accounts Microsoft). Le sottoscrizioni sono accessibili da un subset di tali utenti di directory che sono stati assegnati come servizio amministratore (SA) o coamministratore (CA); Hello solo eccezione è che, per motivi di compatibilità, Accounts Microsoft (precedentemente Windows Live ID) possono essere assegnati come SA o CA senza essere presenti nella directory hello.

Le aziende sicurezza è consigliabile concentrarsi sul dando dipendenti hello conoscere esattamente le autorizzazioni che necessarie. Numero eccessivo di autorizzazioni possono esporre un tooattackers account. Un numero di autorizzazioni insufficiente impedisce ai dipendenti di svolgere il proprio lavoro in modo efficiente. Il [controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) consente di risolvere questo problema offrendo una gestione specifica degli accessi per Azure.

![Accesso protetto alle risorse ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

Usa tale controllo, è possibile separare i compiti all'interno del team e concedere solo quantità di hello di accesso toousers necessarie tooperform i processi. Invece di concedere a tutti autorizzazioni senza restrizioni per la sottoscrizione o le risorse di Azure, è possibile consentire solo determinate azioni. Ad esempio, un dipendente di usare RBAC toolet gestire macchine virtuali in una sottoscrizione, mentre un altro può gestire SQL database all'interno di hello stessa sottoscrizione.

![Accesso protetto alle risorse in Azure (controllo degli accessi in base al ruolo)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Sicurezza e crittografia dei dati in Azure (protezione)

Uno dei hello chiavi toodata di protezione nel cloud hello è tenendo conto dei possibili stati di hello in cui i dati possono verificarsi e i controlli sono disponibili per tale stato. Per la crittografia e protezione dei dati di Azure consigliate hello essere intorno hello seguenti stati dei dati.

- Inattivi: sono inclusi tutti gli oggetti, i contenitori e i tipi di archiviazione di informazioni esistenti in forma statica nei supporti fisici, siano essi dischi magnetici o dischi ottici.

- In transito: Quando vengono trasferiti dati tra i componenti, posizioni o i programmi, ad esempio tramite rete hello, su un bus di servizio (da on-premise toocloud e viceversa, incluse le connessioni ibride, ad esempio ExpressRoute) o durante un input/output processo, viene considerata come in movimento.

### <a name="encryption--rest"></a>Crittografia dei dati inattivi

tooachieve crittografia inattivi seguenti hello:

Supportare almeno uno di hello consigliato modelli crittografia descritti in dettaglio in hello tooencrypt dati della tabella seguente.

| Modelli di crittografia |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Crittografia server | Crittografia server | Crittografia server | Crittografia client
| Crittografia lato server con chiavi gestite dal servizio | Crittografia lato server con chiavi gestite dal cliente in Azure Key Vault | Crittografia lato server con chiavi gestite dal cliente in locale |
| • Azure i provider di risorse eseguire operazioni di crittografia e decrittografia hello <br> • Microsoft gestisce le chiavi di hello <br>• La funzionalità di cloud completa | • Azure i provider di risorse eseguire operazioni di crittografia e decrittografia hello<br>•    Il cliente controlla le chiavi tramite Azure Key Vault<br>• Funzionalità cloud complete | • Azure i provider di risorse eseguire operazioni di crittografia e decrittografia hello <br>• Il cliente controlla chiavi locale <br> •   Funzionalità cloud complete| • I servizi di Azure non possono visualizzare i dati decrittografati <br>•  I clienti mantengono le chiavi in locale o in altri archivi sicuri. Le chiavi non sono servizi disponibili tooAzure <br>• Funzionalità cloud ridotte|

### <a name="enabling-encryption-at-rest"></a>Abilitazione della crittografia dei dati inattivi

**Identificare tutte le posizioni in cui sono archiviati i dati**

obiettivo di Hello di crittografia è tooencrypt tutti i dati. Questa operazione Elimina il possibilità di hello di dati importanti o tutti i percorsi persistenti mancanti. Consente di enumerare tutti i dati archiviati dall'applicazione. 

> [!Note] 
> Non solo "dati applicazioni" o "PII', ma tutti i dati correlati inclusi tooapplication account metadati (sottoscrizione mapping, le informazioni di contratto di informazioni personali).

Si consideri il contenuto memorizzato si utilizzano dati toostore. ad esempio:

- Risorsa di archiviazione esterna (ad esempio, SQL Azure, DocumentDB, HDInsight, Data Lake e così via)

- Risorsa di archiviazione temporanea (qualsiasi cache locale contenente i dati dei tenant)

- Cache in memoria (può essere inserita in file di paging hello.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Utilizzare la crittografia esistente hello al supporto tecnico di rest in Azure

Per ogni archivio usata, hello sfruttano esistente di crittografia al supporto tecnico di Rest.

- Archiviazione di Azure: vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](https://docs.microsoft.com/azure/storage/storage-service-encryption)

- SQL Azure: vedere [Transparent Data Encryption (TDE) e SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)

- Archiviazione in disco locale o VM: vedere [Crittografia dischi di Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

In caso di archiviazione in disco locale o VM usare Crittografia dischi di Azure, se supportato:

IaaS

Utilizzano i servizi con le macchine virtuali IaaS (Windows o Linux) [crittografia del disco di Azure](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt volumi contenenti i dati dei clienti.

PaaS v2

Servizi in esecuzione su PaaS v2 Service Fabric possibile utilizzare la crittografia del disco di Azure per Set di scalabilità della macchina virtuale [VMSS] tooencrypt le proprie macchine virtuali v2 PaaS.

PaaS v1

Crittografia dischi di Azure non è attualmente supportato in PaaS v1. Pertanto, è necessario utilizzare il livello di applicazione tooencrypt crittografia persistenti i dati inattivi.  che includono, tra gli altri, dati applicazione, file temporanei, log e dump di arresto anomalo del sistema.

La maggior parte dei servizi devono tentare di crittografia hello tooleverage di un provider di risorse di archiviazione. Alcuni servizi sono toodo esplicita crittografia, ad esempio, rendere persistente un materiale della chiave (certificati, radice / master chiavi) devono essere archiviate nell'insieme di credenziali chiave.

Se si supporta la crittografia lato servizio con le chiavi di gestione del cliente è necessario toobe un modo per la chiave di hello hello cliente tooget toous. Hello supportato e consigliato toodo di modo che, grazie all'integrazione con insieme di credenziali chiave di Azure (insieme). In questo caso, i clienti possono aggiungere e gestire le proprie chiavi in Azure Key Vault. Un cliente utili come toouse AKV tramite [Guida introduttiva a insieme di credenziali chiave](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate insieme di credenziali chiave di Azure, è possibile aggiungere codice toorequest una chiave dall'insieme quando sono necessari per la decrittografia.

- Vedere [insieme credenziali chiavi Azure – Step by Step](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) per informazioni su come toointegrate con l'insieme.

Se si supportano le chiavi di gestito dal cliente, è necessario tooprovide un'esperienza utente per hello cliente toospecify toouse quale insieme di credenziali chiave (o l'URI dell'insieme di credenziali chiave).

Come crittografia comporta la crittografia hello dei dati di host, l'infrastruttura e tenant, la perdita di hello delle chiavi di hello a causa di attività dannose o di errore toosystem potrebbe essere in tutti i dati crittografato hello viene perso. È pertanto fondamentale che la crittografia soluzione Rest disponga di un ripristino di emergenza completa storia toosystem resilienti errori e attività dannose.

I servizi che implementano crittografia inattivi sono in genere le chiavi di crittografia toohello comunque soggetti o lasciati dati non crittografati nell'unità host hello (ad esempio, in hello file di paging del sistema operativo host hello.) Pertanto, servizi devono verificare hello host volume per i servizi viene crittografato. toofacilitate team questo calcolo è abilitata la distribuzione di hello di crittografia Host, che usa [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP ed estensioni toohello DCM servizio e l'agente tooencrypt hello volume host.

La maggior parte dei servizi viene implementata in VM di Azure standard. Tali servizi dovrebbero ottenere automaticamente la [crittografia host](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) quando viene abilitata dal team di calcolo. Per i servizi eseguiti in cluster gestiti dal team di calcolo, la crittografia host viene abilitata automaticamente con l'implementazione di Windows Server 2016.

### <a name="encryption-in-transit"></a>Crittografia dei dati in transito

La protezione dei dati in transito deve essere una parte essenziale della strategia di protezione dati. Poiché i dati si spostano avanti e indietro da molte posizioni, hello generale si consiglia di utilizzare sempre dati tooexchange di protocolli SSL/TLS in posizioni diverse. In alcuni casi, è opportuno canale di comunicazione intera hello tooisolate tra le sedi locali e cloud dell'infrastruttura tramite una rete privata virtuale (VPN).

Per lo spostamento dei dati tra l'infrastruttura locale e Azure, è opportuno considerare le misure di protezione appropriate, ad esempio HTTPS o VPN.

Per le organizzazioni che richiedono l'accesso toosecure da più workstation in locale tooAzure, [Azure VPN site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Per le organizzazioni che richiedono l'accesso toosecure da una workstation trova tooAzure locale, utilizzare [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Set di dati più grandi possono essere spostati su un collegamento WAN ad alta velocità dedicato, ad esempio [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se si sceglie toouse ExpressRoute, è anche possibile crittografare i dati hello hello a livello di applicazione utilizzando [SSL/TLS](https://support.microsoft.com/kb/257591) o altri protocolli per una maggiore protezione.

Se si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS. [API REST di archiviazione](https://msdn.microsoft.com/library/azure/dd179355.aspx) tramite HTTPS può anche essere utilizzati toointeract con [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/).

Le organizzazioni che non soddisfano tooprotect dati in transito sono più sensibili per [attacchi man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [intercettazione](https://technet.microsoft.com/library/gg195641.aspx)e Hijack della sessione. Questi attacchi possono essere hello innanzitutto ottenere l'accesso ai dati tooconfidential.

Maggiori informazioni sull'opzione VPN di Azure leggendo l'articolo hello [pianificazione e progettazione per il Gateway VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Applicare la crittografia dei dati a livello di file

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp di criteri di crittografia, identità e autorizzazione utilizza proteggere file e posta elettronica. Azure RMS opera su più dispositivi, tra cui telefoni, tablet e PC, applicando una protezione all'interno e all'esterno dell'organizzazione. Questa funzionalità è possibile poiché Azure RMS aggiunge un livello di protezione che rimane con dati hello, anche quando fuoriescono dai confini fisici dell'organizzazione.

Quando si usano Azure RMS tooprotect i file, si utilizza la crittografia standard del settore con il supporto completo di [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Quando si utilizzano Azure RMS per la protezione dati, occorre garanzia hello che hello rimane associata file hello, anche se è copiato toostorage che non è incluso nel controllo hello del reparto IT, ad esempio un servizio di archiviazione cloud. Hello stesso comportamento si verifica per i file condivisi tramite posta elettronica, file hello viene protetto come un messaggio di posta elettronica tooan allegato, con istruzioni come tooopen hello protetto allegato.
Durante la pianificazione per l'adozione di Azure RMS è consigliabile hello segue:

- Installare hello [app RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Questa app si integra con le applicazioni Office installando un componente aggiuntivo di Office che offre agli utenti un modo semplice per proteggere direttamente i file.

- Configurare le applicazioni e servizi toosupport Azure RMS

- Creare [modelli personalizzati](https://technet.microsoft.com/library/dn642472.aspx) che rispecchiano i requisiti aziendali, ad esempio un modello per i dati riservati da applicare in tutti i messaggi di posta elettronica correlati a informazioni riservate.

Le organizzazioni che sono vulnerabili in [classificazione dei dati](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) e la protezione dei file potrebbe essere più vulnerabile toodata perdita. Senza protezione file appropriate, le organizzazioni non tooobtain in grado di ottenere informazioni aziendali accurate, monitoraggio per evitare eventuali abusi e impedire accessi non autorizzati toofiles.

> [!Note]
> Maggiori informazioni su Azure RMS, leggere l'articolo hello [Introduzione a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Proteggere l'applicazione (protezione)
Sebbene Azure è responsabile per la protezione dell'infrastruttura di hello e una piattaforma che l'applicazione viene eseguita in, è toosecure la responsabilità dell'applicazione stessa. In altre parole, è necessario toodevelop, distribuire e gestire il codice dell'applicazione e i contenuti in modo sicuro. In caso contrario, il codice dell'applicazione o il contenuto può essere ancora toothreats vulnerabile.

### <a name="web-application-firewall-waf"></a>Web application firewall (WAF)
[Web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) è una funzionalità del [gateway applicazione](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) che offre una protezione centralizzata delle applicazioni Web da exploit e vulnerabilità comuni.

Firewall applicazione Web è in base alle regole da hello [set di regole di base OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 o 2.2.9. Le applicazioni Web sono sempre più vittime di attacchi che sfruttano le più comuni vulnerabilità note. Comuni tra questi attacchi sono gli attacchi SQL injection, cross-site scripting attacchi tooname alcuni. Impedire gli attacchi nel codice dell'applicazione può risultare complessa e potrebbe richiedere manutenzione rigorosa, l'applicazione di patch e il monitoraggio a più livelli della topologia applicazione hello. Firewall applicazione web centralizzata rende molto più semplice gestione della sicurezza e offre migliorato garanzia agli amministratori di tooapplication contro minacce o intrusioni. Una soluzione WAF può inoltre riflettere minaccia alla sicurezza tooa più veloce per l'applicazione di patch una vulnerabilità nota in una posizione centrale e la protezione di ognuna delle singole applicazioni web. Gateway applicazione esistente può essere facilmente convertito tooa web applicazione firewall abilitato applicazioni gateway.

Alcune delle vulnerabilità web comuni hello firewall applicazione web consente di proteggere include:

- Protezione dagli attacchi SQL injection

- Protezione dagli attacchi di scripting intersito

- Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion

- Protezione dalle violazioni del protocollo HTTP

- Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header

- Prevenzione contro robot, crawler e scanner

- Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)

> [!Note]
> Per un elenco dettagliato delle regole e le protezioni vedere seguente hello [set di regole di base](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure offre inoltre più facile utilizzare funzionalità toohelp proteggere il traffico in ingresso e in uscita per l'app. Azure consente ai clienti proteggere il codice di applicazione fornendo esternamente fornite funzionalità tooscan l'applicazione web per le vulnerabilità.

- [Proteggere l'app Web mediante vari meccanismi di autenticazione e autorizzazione](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Configurare l'autenticazione di Azure Active Directory per l'app](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Proteggere il traffico tooyour app abilitando Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Forzare tutto il traffico in ingresso tramite connessione HTTPS](http://microsoftazurewebsitescheatsheet.info/)

  - [Abilitare Strict Transport Security (HSTS)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Limitare l'accesso tooyour app dall'indirizzo IP del client](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Limitare l'accesso tooyour app tramite il comportamento del client - frequenza di richiesta e la concorrenza](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Analizzare il codice dell'app Web per le vulnerabilità tramite Tinfoil Security Scanning](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [Configurare l'autenticazione reciproca TLS toorequire client certificati tooconnect tooyour web app](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Configurare un certificato client per l'utilizzo da parte del toosecurely app connettere le risorse di tooexternal](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Rimuovere strumenti di server standard intestazioni tooavoid da fingerprinting app](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Connettere in modo sicuro l'app alle risorse in una rete privata usando una VPN da punto a sito](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Connettere in modo sicuro l'app alle risorse in una rete privata usando connessioni ibride](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure App Service utilizza hello stessa soluzione Antimalware utilizzata da servizi Cloud di Azure e macchine virtuali. toolearn informazioni fare riferimento tooour [documentazione Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Proteggere la rete (protezione)
Microsoft Azure include un toosupport di infrastruttura di rete affidabile l'applicazione e i requisiti di connettività del servizio. Connettività di rete è possibile tra le risorse disponibili in Azure, tra la versione locale e Azure ospitati, risorse e tooand da hello Internet e Azure.

Hello [dell'infrastruttura di rete di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) Abilita tooeach con altre risorse di Azure di connettersi è toosecurely [reti virtuali (Vnet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello Azure cloud rete dedicata tooyour sottoscrizione. È possibile connettere reti virtuali tooyour sulle reti locali.

![Proteggere la rete (protezione)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Se è necessario un controllo di accesso a livello di rete di base (basato su IP indirizzo e hello protocolli TCP o UDP), quindi è possibile utilizzare [gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Un gruppo di sicurezza di rete (gruppo) è un pacchetto con stato base filtro firewall e consente toocontrol accesso in base a un [5 tuple](https://www.techopedia.com/definition/28190/5-tuple).

Rete di Azure supporta hello possibilità toocustomize hello il funzionamento del routing del traffico di rete di una rete virtuale di Azure. A tale scopo è possibile configurare [route definite dall'utente](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) in Azure.

[Il tunneling forzato](https://www.petri.com/azure-forced-tunneling) è un meccanismo che è possibile utilizzare tooensure che i servizi non sono consentiti tooinitiate toodevices una connessione su hello Internet.

Azure supporta dedicato collegamento WAN connettività tooyour locale rete e una rete virtuale di Azure con [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). collegamento Hello tra Azure e il sito utilizza una connessione dedicata che non viene trasmesso hello rete Internet pubblica. Se l'applicazione Azure è in esecuzione in più Data Center, è possibile utilizzare [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute richieste degli utenti in modo intelligente tra istanze di un'applicazione hello. È inoltre possibile inviare traffico tooservices non è in esecuzione in Azure se sono accessibili da Internet hello.

## <a name="virtual-machine-security-protect"></a>Sicurezza delle macchine virtuali (protezione)

[Macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/) consente di distribuire in modo flessibile un'ampia gamma di soluzioni di calcolo. Grazie al supporto per Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP e Servizi BizTalk di Azure, è possibile distribuire qualsiasi carico di lavoro, in qualunque linguaggio, praticamente su tutti i sistemi operativi.

Con Azure, è possibile utilizzare [software antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) da fornitori di sicurezza, ad esempio Microsoft, Symantec, Trend Micro e Kaspersky tooprotect delle macchine virtuali dal file dannosi, adware e altre minacce.

Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure è una funzionalità di protezione in tempo reale che aiuta a identificare e rimuovere virus, spyware e altro software dannoso. Microsoft Antimalware fornisce avvisi configurabili quando noto tooinstall di tentativi di software dannoso o indesiderato stesso o eseguito nei sistemi di Azure.

[Backup di Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) è una soluzione scalabile che protegge i dati delle applicazioni senza investimenti di capitale e con costi operativi minimi. Gli errori delle applicazioni possono danneggiare i dati e gli errori umani possono comportare l'introduzione di bug nelle applicazioni. Con Backup di Azure, le macchine virtuali che eseguono Windows e Linux sono protette.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) consente di orchestrare la replica, il failover e il ripristino di carichi di lavoro e app in modo che siano disponibili da una località secondaria in caso di inattività di quella primaria.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Garantire la conformità: elenco di controllo della due diligence per i servizi cloud (protezione)

Microsoft sviluppato [hello Checklist molta attenzione a causa di Cloud Services](https://aka.ms/cloudchecklist.download) toohelp organizzazioni esercitare scadenza molta attenzione che ritengono di un cloud toohello di spostamento. Fornisce una struttura di un'organizzazione di qualsiasi dimensione e tipo, ovvero aziende private e le organizzazioni del settore pubblico, inclusi per enti pubblici in tutti i livelli e organizzazioni no profit: tooidentify le proprie prestazioni, servizio, la gestione dei dati e gli obiettivi di governance e requisiti. Ciò consente loro offerte hello toocompare dei provider di servizi cloud diversi, in definitiva che costituiscono la base hello per un contratto di servizio cloud.

elenco di controllo Hello fornisce un framework che consente di allineare by clausola con un nuovo standard internazionale per i contratti di servizio cloud, ISO/IEC 19086. Questo standard offre un insieme unificato di considerazioni per le organizzazioni toohelp prendere decisioni relative all'adozione di cloud e creare una base comune per il confronto di offerte di servizio cloud.

elenco di controllo Hello Alza di livello un cloud toohello spostamento accuratamente esaminati, fornendo informazioni strutturate e un approccio coerenza e ripetibile per la scelta di un provider di servizi cloud.

L'adozione del cloud non è più semplicemente una decisione relativa alla tecnologia. Poiché l'elenco di controllo requisiti toccano su ogni aspetto di un'organizzazione, hanno tooconvene tutti chiave interne-decisori: hello CIO e CISO nonché legali, dei rischi professionisti di gestione, approvvigionamento e la conformità. In questo modo si aumenta l'efficienza di hello del processo decisionale hello e le decisioni di terra audio ragionamento, riducendo la probabilità di hello di tooadoption problemi imprevisti.

Hello, inoltre, l'elenco di controllo:

- Espone gli argomenti di discussione chiave dei decisori all'inizio di hello del processo di adozione hello cloud.

- Supporta le discussioni business approfondita sulle normative e gli obiettivi dell'organizzazione di hello per la protezione dei dati sulla privacy e informazioni personali (PII).

- Consente di identificare i potenziali problemi che potrebbero influire su un progetto cloud.

- Offre una gamma di domande, con hello stessi termini, definizioni, metriche e i risultati finali per ogni provider, il processo di hello toosimplify del confronto tra le offerte dal provider di servizi cloud diversi.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Convalida della sicurezza delle applicazioni e dell'infrastruttura di Azure (rilevamento)

[Sicurezza operativa Azure](https://docs.microsoft.com/azure/security/azure-operational-security) fa riferimento a servizi toohello, controlli e toousers disponibili funzionalità per la protezione dei dati, applicazioni e altre risorse in Microsoft Azure.

![Convalida della sicurezza (rilevamento)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Sicurezza operative di Azure si basa su un framework che incorpora informazioni hello ottenute tramite una varie funzionalità che sono univoci tooMicrosoft, tra cui Microsoft Security Development Lifecycle (SDL), Microsoft Security risposta Centre hello hello programma e conoscenza approfondita dei panorama delle minacce alla sicurezza informatica hello.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) è la soluzione di gestione IT per cloud ibrido hello hello. Utilizzato da solo o tooextend consente la distribuzione esistente di System Center, OMS hello la massima flessibilità e controllo per la gestione basata su cloud dell'infrastruttura.

![Microsoft Operations Management Suite (OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Con OMS, è possibile gestire qualsiasi istanza di qualsiasi cloud, inclusi i cloud locali, Azure, AWS, Windows Server, Linux, VMware e OpenStack, a un costo inferiore rispetto alle soluzioni della concorrenza. Compilato per HelloWorld prima di cloud, OMS offre la un nuovo toomanaging approccio dell'azienda che consente a hello più veloce e più conveniente toomeet nuove attività le problematiche e supportare nuovi carichi di lavoro, le applicazioni e ambienti cloud.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornisce servizi di monitoraggio per OMS raccogliendo i dati delle risorse gestite in un repository centrale. Questi dati possono includere gli eventi, dati sulle prestazioni o dati personalizzati forniti tramite hello API. Una volta raccolti, hello sono disponibili dati per gli avvisi, l'analisi e l'esportazione.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Questo metodo consente tooconsolidate dati da una varietà di origini, pertanto è possibile combinare dati da servizi di Azure esistenti ambiente locale. Inoltre chiaramente separa raccolta hello di dati hello dall'azione di hello eseguita su tali dati in modo che tutte le azioni sono tooall disponibili tipi di dati.

### <a name="azure-security-center"></a>Centro sicurezza di Azure

[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sui hello protezione delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Centro sicurezza PC analizza lo stato di sicurezza hello le risorse di Azure tooidentify potenziali vulnerabilità della protezione. Un elenco di suggerimenti in modo semplificato il processo di hello di configurazione di controlli necessari.

Tra gli esempi sono inclusi:

- Provisioning antimalware toohelp identificare e rimuovere il software dannoso

- Configurazione di rete sicurezza e gruppi di regole toocontrol traffico tooVMs

- Il provisioning dei firewall applicazione web toohelp difendersi da attacchi che le applicazioni web di destinazione

- Distribuzione degli aggiornamenti di sistema mancanti

- Indirizzamento delle configurazioni del sistema operativo che non corrispondono a hello consiglia le linee di base

Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner come programmi antimalware e firewall. Quando vengono rilevate minacce, viene creato un avviso di sicurezza. Ad esempio, è compreso il rilevamento di:

- VM compromesse in comunicazione con indirizzi IP dannosi noti

- Malware avanzato rilevato tramite Segnalazione errori Windows

- Attacchi di forza bruta alle VM

- Avvisi di sicurezza da programmi antimalware e firewall integrati

### <a name="azure-monitor"></a>Monitoraggio di Azure

[Monitoraggio Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) fornisce puntatori tooinformation su tipi specifici di risorse. Offre una visualizzazione, query, routing, avvisi, scalabilità automatica e l'automazione in entrambi i dati hello dell'infrastruttura di Azure (Log di attività) e ogni singola risorsa di Azure (log di diagnostica).

Le applicazioni cloud sono complesse e hanno molte parti mobili. Il monitoraggio fornisce tooensure dati che l'applicazione resta alto e in esecuzione in uno stato integro. Consente inoltre toostave è impostata su off problemi potenziali o risolvere i problemi oltre quelle.

![Monitoraggio Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) , inoltre, è possibile utilizzare Monitoraggio dati toogain approfondite sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale.

Il controllo della sicurezza della rete è fondamentale per rilevare le vulnerabilità e garantire la conformità con il modello di governance normativo e della sicurezza IT. Con visualizzazione del gruppo di sicurezza, è possibile recuperare le regole di hello configurato il gruppo di sicurezza di rete e sicurezza, nonché hello regole di sicurezza efficace. Con l'elenco di hello delle regole applicate, è possibile determinare ss e porte hello aperte vulnerabilità di rete.

### <a name="network-watcher"></a>Network Watcher

[Controllo di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) è un servizio consente toomonitor internazionale e diagnosticare le condizioni a un livello di rete in, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure. Il servizio include l'acquisizione pacchetti, l'hop successivo, la verifica del flusso IP, la visualizzazione dei gruppi di sicurezza e i registri dei flussi dei gruppi di sicurezza di rete. Monitoraggio a livello di scenario è inclusa una visualizzazione di tooend finale delle risorse di rete in Monitoraggio risorse di rete di contrasto tooindividual.

### <a name="storage-analytics"></a>Analisi archiviazione

[Archiviazione Analitica](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) può archiviare le metriche che includono transazioni aggregate le statistiche e dati sulla capacità del servizio di archiviazione tooa richieste. Vengono dichiarate le transazioni a livello di operazione entrambi hello API, nonché a livello di servizio di archiviazione hello e capacità viene segnalata a livello di servizio di archiviazione hello. Dati di metrica possono essere utilizzati tooanalyze utilizzo di servizi di archiviazione, diagnosticare i problemi con le richieste effettuate al servizio di archiviazione hello e tooimprove hello prestazioni delle applicazioni che utilizzano un servizio.

### <a name="application-insights"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) è un servizio estendibile di gestione delle prestazioni delle applicazioni per sviluppatori Web su più piattaforme, Utilizzarlo toomonitor l'applicazione web in tempo reale. Il servizio rileva automaticamente le anomalie nelle prestazioni Include toohelp di analitica potenti strumenti per la diagnosi di problemi e toounderstand degli utenti a cui eseguire l'app. È progettato toohelp è migliorare continuamente le prestazioni e usabilità. Funziona per le app su una vasta gamma di piattaforme, tra cui .NET, Node.js e J2EE, ospitato in locale o nel cloud hello. Si integra con il processo di devOps e dispone di diversi strumenti di sviluppo tooa punti di connessione.

Esegue il monitoraggio di:

- **Frequenza delle richieste, tempi di risposta e percentuali di errore**: trovare le pagine più visitate, gli orari di visita e la posizione degli utenti.  Vedere quali pagine abbiano prestazioni migliori. Se i tempi di risposta e le percentuali di errore aumentano di pari passo con le richieste, è probabile che ci sia un problema di assegnazione delle risorse.

- **Tassi di dipendenza, tempi di risposta e percentuali di errore**: trovare quali servizi esterni causino un rallentamento.

- **Eccezioni** : analizzare le statistiche aggregata hello, o selezionare istanze specifiche e approfondire l'analisi dello stack hello e le richieste correlate. Vengono segnalate eccezioni di server e browser.

- **Visualizzazioni pagina e prestazioni di carico**, segnalate dai browser degli utenti.

- **Chiamate AJAX da pagine Web**: frequenza, tempi di risposta e percentuali di errore.

- **Conteggi degli utenti e delle sessioni**.

- **Contatori delle prestazioni** dai computer server Windows o Linux, ad esempio l'uso di CPU, memoria e rete.

- **Diagnostica dell'host** da Docker o Azure.

- **Log di traccia di diagnostica** dall'app, in modo da poter correlare gli eventi di traccia con le richieste.

- **Eventi personalizzati e le metriche** scrivere manualmente nel codice client o server di hello, tootrack gli eventi di business, ad esempio articoli venduti o partite vinte.
infrastruttura di Hello per l'applicazione è in genere costituito da numerosi componenti, forse una macchina virtuale, account di archiviazione e rete virtuale, o un'app web, database, server di database e i servizi di terze parti 3rd. Questi componenti non appaiono come entità separate, ma come parti correlate e interdipendenti di una singola entità Si desidera toodeploy, gestire e monitorarli come gruppo. [Gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) consente toowork con risorse hello nella soluzione come gruppo.

È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per la soluzione in un'operazione singola, coordinata. Per la distribuzione viene usato un modello; questo modello può essere usato per diversi ambienti, ad esempio di testing, staging e produzione. Gestione risorse offre sicurezza, il controllo e assegnazione di tag toohelp funzionalità Gestione delle risorse dopo la distribuzione.

**vantaggi di Hello dell'utilizzo di gestione risorse**

Gestione risorse offre numerosi vantaggi:

- È possibile distribuire, gestire e monitorare tutte le risorse di hello per la soluzione come un gruppo, anziché gestire singolarmente queste risorse.

- Più volte, è possibile distribuire la soluzione in tutto il ciclo di sviluppo hello e che le risorse vengono distribuite in uno stato coerente di fiducia.

- È possibile gestire l'infrastruttura con modelli dichiarativi, piuttosto che con script.

- È possibile definire le dipendenze di hello tra risorse, in modo che vengono distribuiti nell'ordine corretto hello.

- È possibile applicare tooall servizi di controllo di accesso nel gruppo di risorse perché il controllo di accesso basato sui ruoli (RBAC) in modo nativo viene integrato nella piattaforma di gestione di hello.

- È possibile applicare tag tooresources toologically organizzare tutte le risorse di hello nella sottoscrizione.

- Si può aiutare a chiarire la fatturazione dell'organizzazione visualizzando i costi per un gruppo di risorse di condivisione hello stesso tag.

> [!Note]
> Gestione risorse fornisce un nuovo toodeploy modo e gestire le soluzioni. Se è stato utilizzato un modello di distribuzione precedente hello e si desidera toolearn sulle modifiche di hello, vedere [distribuzione classica e gestione di informazioni sulle risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla sicurezza, vedere alcuni degli approfondimenti sull'argomento:

- [Controllo e registrazione](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Crimine informatico](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Progettazione e sicurezza operativa](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Crittografia](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Gestione delle identità e dell'accesso](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Sicurezza di rete](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Gestione delle minacce](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
