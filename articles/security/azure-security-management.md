---
title: sicurezza di gestione remota aaaEnhance in Azure | Documenti Microsoft
description: Questo articolo illustra i passaggi per il miglioramento della sicurezza della gestione remota nell'amministrazione degli ambienti di Microsoft Azure, inclusi Servizi cloud, Macchine virtuali e applicazioni personalizzate.
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Gestione della sicurezza in Azure
I sottoscrittori di Azure possono gestire i propri ambienti cloud da più dispositivi, tra cui workstation di gestione, PC per sviluppatori e dispositivi di utenti finali con privilegi elevati con autorizzazioni specifiche per le attività. In alcuni casi, le funzioni amministrative vengono eseguite tramite le console basata sul web, ad esempio hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). In altri casi, potrebbe essere tooAzure connessioni dirette da sistemi locali su reti Private virtuali (VPN), servizi Terminal, protocolli di applicazioni client o (a livello di codice) hello Azure Service Management API (SMAPI). Gli endpoint client possono essere inoltre aggiunti a un dominio o isolati e non gestiti, ad esempio tablet o smartphone.

Anche se più funzioni di accesso e la gestione forniscono un'ampia gamma di opzioni, questo variabilità può aggiungere distribuzione cloud tooa di rischio. Può essere difficile toomanage, tenere traccia e controllare le azioni amministrative. Questo variabilità anche può comportare rischi di protezione tramite gli endpoint di accesso non regolamentate tooclient che vengono utilizzati per la gestione dei servizi cloud. L'uso di workstation generiche o personali per lo sviluppo e la gestione dell'infrastruttura genera vettori di minaccia imprevedibili, come l'esplorazione del Web (ad esempio attacchi di tipo watering hole) o la posta elettronica (ad esempio "ingegneria sociale" e phishing).

![][1]

rischio di attacchi Hello aumenta in questo tipo di ambiente perché si tratta di criteri di sicurezza tooconstruct complessa e meccanismi tooappropriately gestire interfacce tooAzure di accesso (ad esempio SMAPI) dall'endpoint ampiamente diversi.

### <a name="remote-management-threats"></a>Minacce relative alla gestione remota
Gli utenti malintenzionati spesso tentano di toogain con privilegiata da compromettere le credenziali dell'account (ad esempio, tramite password bruta imporre, phishing e raccolta delle credenziali) o da indurre gli utenti a eseguire codice dannoso (ad esempio, da siti Web dannosi con unità di download o da allegati di posta elettronica dannoso). In un ambiente cloud gestiti in remoto, account violazioni della sicurezza può causare tooan rischio maggiore tooanywhere scadenza, l'accesso in qualsiasi momento.

Anche con controlli rigidi sugli account amministratore principale, gli account utente di livello inferiore possono essere utilizzato tooexploit punti deboli di una strategia di sicurezza. Mancanza di formazione di sicurezza appropriate può inoltre causare toobreaches tramite la diffusione accidentale o l'esposizione delle informazioni sull'account.

Quando la workstation utente viene usata anche per attività amministrative, è possibile che venga compromessa in molti punti diversi, Se un utente è esplorazione web hello, utilizzando gli strumenti di terze parti 3rd e open source o apertura di un file di documento dannoso che contiene un trojan.

In generale, più attacchi mirati che comporterà violazioni della sicurezza dei dati possono essere tracciati toobrowser exploit e plug-in (ad esempio Flash, PDF, Java), spear phishing (posta elettronica) su computer desktop. Queste macchine potrebbero disporre di livello amministrativo o le autorizzazioni a livello di servizio tooaccess live server o dispositivi di rete per le operazioni quando viene utilizzato per lo sviluppo o di altre risorse di gestione.

### <a name="operational-security-fundamentals"></a>Concetti fondamentali sulla sicurezza operativa
Per la gestione più sicuro e operazioni, è possibile ridurre la superficie di attacco del client, riducendo il numero di hello di punti di ingresso possibili. Per ottenere questo risultato, è possibile usare le entità di sicurezza di tipo "separazione di compiti" e "separazione di ambienti".

Isolare le funzioni riservate dal loro toodecrease hello probabilità che un errore a livello di una porta tooa violazione in un altro. Esempi:

* Attività amministrative non devono essere combinate con le attività che potrebbero causare la compromissione tooa (ad esempio, malware nel messaggio di posta elettronica dell'amministratore che infetta quindi un server di infrastruttura).
* Una workstation utilizzata per operazioni alti livelli di sensibilità non deve essere hello stesso sistema utilizzato per scopi ad alto rischio, ad esempio hello esplorazione Internet.

Ridurre la superficie di attacco del sistema hello rimuovendo il software non necessario. Esempio:

* Se la funzione principale del dispositivo hello servizi cloud toomanage standard di amministrazione, supporto o workstation di sviluppo non dovrebbe richiedere alcuna installazione di un client di posta elettronica o altre applicazioni per la produttività.

Sistemi client che hanno tooinfrastructure accesso amministratore i componenti devono essere sottoposti a toohello più rigoroso possibili criteri tooreduce rischi per la sicurezza. Esempi:

* Criteri di sicurezza possono includere impostazioni di criteri di gruppo che nega l'accesso a Internet aprire dispositivo hello e l'utilizzo di una configurazione di firewall restrittive.
* Usare VPN IPsec (Internet Protocol Security) se l'accesso diretto è necessario.
* Configurare domini di Active Directory separati per la gestione e lo sviluppo.
* Isolare e filtrare il traffico di rete della workstation di gestione.
* Usare software antimalware.
* Implementare l'autenticazione a più fattori tooreduce hello rischio credenziali rubate.

Il consolidamento delle risorse di accesso e l'eliminazione degli endpoint non gestiti consentono anche di semplificare le attività di gestione.

### <a name="providing-security-for-azure-remote-management"></a>Sicurezza per la gestione remota di Azure
Azure offre protezione amministratori di tooaid meccanismi che gestiscono servizi cloud di Azure e macchine virtuali. ad esempio:

* Autenticazione e [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-configure.md).
* Monitoraggio, registrazione e controllo.
* Certificati e comunicazioni crittografate.
* Portale di gestione Web.
* Filtri dei pacchetti di rete.

Con configurazione di protezione sul lato client e la distribuzione di Data Center di un gateway di gestione, è possibili toorestrict e monitoraggio amministratore toocloud applicazioni di accesso e di dati.

> [!NOTE]
> Alcune indicazioni incluse in questo articolo potrebbero comportare un maggiore utilizzo delle risorse di dati, rete o calcolo e un aumento dei costi di licenza o di sottoscrizione.
>
>

## <a name="hardened-workstation-for-management"></a>Workstation con protezione avanzata per la gestione
obiettivo Hello di protezione avanzata di una workstation è tooeliminate tutti, ma le funzioni principali di hello obbligatorio per tale toooperate, rendendo possibili superficie di attacco hello quanto più breve possibile. Protezione avanzata di sistema include riducendo al minimo il numero di hello dei servizi installati e delle applicazioni, limitando l'esecuzione dell'applicazione, limitando tooonly accesso rete cosa è necessario, e mantenere sempre il sistema di hello backup toodate. L'uso di una workstation con protezione avanzata per la gestione consente anche di separare gli strumenti amministrativi da altre attività dell'utente finale.

All'interno di un ambiente aziendale locale, è possibile limitare la superficie di attacco hello dell'infrastruttura fisica tramite reti di gestione dedicata, stanze dei server che dispongono dell'accesso smart card e le workstation che eseguono in aree protette del rete hello. In un cloud o modello IT ibrido, essere attenti a servizi di gestione protetta può essere più complessa a causa di mancanza di hello di risorse tooIT accesso fisico. L'implementazione delle soluzioni di protezione richiede una configurazione attenta del software, processi incentrati sulla sicurezza e criteri completi.

Utilizzando un footprint di con privilegi minimi ridotta a icona software in una workstation bloccata per la gestione di cloud e per lo sviluppo di applicazioni, può ridurre il rischio di hello di eventi di sicurezza per la standardizzazione di ambienti di gestione e sviluppo remoti hello. Una configurazione di protezione avanzata workstation consente di evitare di compromettere hello account che sono utilizzati toomanage cloud cruciali risorse chiudendo molti percorsi comuni utilizzati da malware e gli attacchi. In particolare, è possibile utilizzare [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) e toocontrol tecnologia Hyper-V e isolare il comportamento di sistema client e ridurre i rischi, tra cui posta elettronica o esplorazione di Internet.

In una workstation con protezione avanzata, messaggio per l'amministratore esegue un account utente standard (che blocca l'esecuzione di livello amministrativo) e le applicazioni associate sono controllate da un elenco Consenti. elementi di base di una workstation finalizzato Hello sono i seguenti:

* Analisi attiva e applicazione di patch. Distribuire il software antimalware, eseguire analisi di vulnerabilità regolari e aggiornare tutte le workstation utilizzando l'ultimo aggiornamento della sicurezza hello in modo tempestivo.
* Funzionalità limitata. È possibile disinstallare le applicazioni non necessarie e disabilitare i servizi non necessari (avvio).
* Protezione avanzata della rete. Utilizzare Windows Firewall regole tooallow solo gli indirizzi IP, porte e gli URL correlati tooAzure gestione. Verificare che tale workstation toohello le connessioni remote in ingresso vengono anche bloccate.
* Restrizione dell'esecuzione. Consentire solo un set di file eseguibili predefiniti che sono necessari per la gestione toorun (denominato tooas "rifiuto predefinito"). Per impostazione predefinita, gli utenti devono essere negati l'autorizzazione per qualsiasi programma a meno che non è definito in modo esplicito in hello toorun elenco Consenti.
* Privilegi minimi. Gli utenti di workstation di gestione senza privilegi amministrativi sul computer locale di hello stesso. In questo modo, non possono modificare la configurazione di sistema hello o file di sistema hello, intenzionalmente o accidentalmente.

È possibile applicare tutte queste tramite [oggetti Criteri di gruppo](https://www.microsoft.com/download/details.aspx?id=2612) (GPO) in servizi di dominio Active Directory (AD DS) e applicarli tramite gli account di gestione tooall dominio gestione (locale).

### <a name="managing-services-applications-and-data"></a>Gestione di servizi, applicazioni e dati
Configurazione di servizi cloud di Azure viene eseguita tramite il portale di Azure hello o SMAPI, tramite l'interfaccia della riga di comando di Windows PowerShell hello o un'applicazione personalizzata che consente di sfruttare queste interfacce RESTful. I servizi che usano questi meccanismi includono Azure Active Directory (Azure AD), Archiviazione di Azure, Siti Web di Azure, Rete virtuale di Azure e altri ancora.

Distribuire la macchina virtuale: applicazioni forniscono i propri strumenti client e le interfacce in base alle esigenze, ad esempio hello Microsoft Management Console (MMC), una console di gestione dell'organizzazione (ad esempio Microsoft System Center o Windows Intune) o un altro management applicazione-Microsoft SQL Server Management Studio, ad esempio. Questi strumenti si trovano in genere in un ambiente aziendale o in una rete client. Possono dipendere da protocolli di rete specifici, ad esempio Remote Desktop Protocol (RDP), che richiedono connessioni dirette e con stato. Alcuni possono disporre di interfacce basate su web che non devono essere accessibile tramite Internet hello o apertamente pubblicata.

È possibile limitare l'accesso tooinfrastructure e piattaforma di gestione dei servizi in Azure utilizzando [multi-factor authentication](../multi-factor-authentication/multi-factor-authentication.md), [i certificati di gestione di certificati x. 509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)e le regole del firewall. portale di Azure Hello e SMAPI richiedono Transport Layer Security (TLS). Tuttavia, servizi e applicazioni che si distribuiscono in Azure richiedono le misure di protezione tootake più appropriate in base all'applicazione. Questi meccanismi possono essere spesso abilitati con maggiore facilità tramite una configurazione di workstation con protezione avanzata standardizzata.

### <a name="management-gateway"></a>Gateway di gestione
toocentralize tutti amministrativi di accesso e semplificare il monitoraggio e la registrazione, è possibile distribuire una dedicata [Gateway Desktop remoto](https://technet.microsoft.com/library/dd560672) server (Gateway Desktop remoto) in locale di rete, connesso tooyour ambiente Azure.

Un Gateway Desktop remoto è un servizio proxy RDP basato su criteri che applica i requisiti relativi alla sicurezza. L'implementazione di un Gateway Desktop remoto insieme a Protezione accesso alla rete di Windows Server consentono di assicurare che solo i client che soddisfano criteri di integrità specifici definiti dagli oggetti Criteri di gruppo di Servizi di dominio Active Directory riescano a connettersi. Eseguire anche queste operazioni:

* Eseguire il provisioning un [certificato di gestione di Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) su hello Gateway Desktop remoto in modo che sia consentito di host a soli hello tooaccess hello portale di Azure.
* Join hello Gateway Desktop remoto toohello stesso [dominio di gestione](http://technet.microsoft.com/library/bb727085.aspx) come hello workstation di amministratore. Ciò è necessario quando si utilizza una VPN IPsec site-to-site o ExpressRoute all'interno di un dominio con tooAzure un trust unidirezionale AD o se credenziali federazione tra locale istanza di Active Directory e Azure AD.
* Configurare un [criteri di autorizzazione connessioni client](http://technet.microsoft.com/library/cc753324.aspx) toolet hello Gateway Desktop remoto verificare che nome del computer client hello è valido (dominio) e tooaccess consentiti hello portale di Azure.
* Utilizzare IPsec per [VPN di Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther proteggere il traffico di gestione di intercettazione e token di furto o provare a un collegamento Internet isolato tramite [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* Abilitare l'autenticazione a più fattori tramite [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) oppure l'autenticazione tramite smart card per gli amministratori che accedono tramite il Gateway Desktop remoto.
* Configurare l'origine [restrizioni degli indirizzi IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) o [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) in numero di hello Azure toominimize di endpoint di gestione consentite.

## <a name="security-guidelines"></a>Linee guida sulla sicurezza
In generale, contribuendo toosecure workstation di amministratore per l'utilizzo con cloud hello pratiche toohello simile per qualsiasi workstation locale, ad esempio, ridotta a icona di compilazione e autorizzazioni restrittive. Alcuni aspetti della gestione del cloud sono più analogia tooremote o gestione fuori banda enterprise. Ad esempio utilizzare hello e controllo delle credenziali, sicurezza avanzata accesso remoto e di rilevamento minacce e risposta.

### <a name="authentication"></a>Autenticazione
È possibile utilizzare indirizzi IP di origine tooconstrain restrizioni di accesso di Azure per l'accesso a strumenti di amministrazione e controllare le richieste di accesso. toohelp Azure di identificare i client di gestione (workstation e/o applicazioni), è possibile configurare sia SMAPI (tramite gli strumenti, ad esempio i cmdlet di Windows PowerShell dal cliente) e hello toorequire portale Azure sul lato client Gestione certificati toobe inoltre tooSSL i certificati installati. È anche consigliabile che l'accesso amministratore richieda l'autenticazione a più fattori.

Alcune applicazioni o alcuni servizi distribuiti in Azure possono avere meccanismi di autenticazione specifici per l'accesso degli utenti finali e degli amministratori, mentre altri sfruttano tutte le funzionalità di Azure AD. A seconda se federazione le credenziali tramite Active Directory Federation Services (ADFS), utilizzando la sincronizzazione delle directory o la gestione di account utente esclusivamente in hello cloud, utilizzando [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (in parte Azure AD Premium) consente di gestire i cicli di vita di identità tra le risorse di hello.

### <a name="connectivity"></a>Connettività
Diversi meccanismi sono disponibili toohelp client protetta connessioni tooyour reti virtuali di Azure. Due di questi meccanismi, [VPN site-to-site](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) e [VPN point-to-site](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), abilitare l'utilizzo di hello del settore (S2S) di IPsec standard o hello [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) per la crittografia e tunneling. Quando Azure si connette gestione toopublic orientati ai servizi di Azure, ad esempio hello portale di Azure, Azure richiede Hypertext Transfer Protocol Secure (HTTPS).

Una workstation finalizzata autonoma che non si connettono tooAzure tramite un Gateway Desktop remoto hello basato su SSTP point-to-site VPN toocreate hello connessione iniziale toohello rete virtuale di Azure, utilizzare e quindi stabilire tooindividual connessione RDP virtuale macchine da con tunnel VPN hello.

### <a name="management-auditing-vs-policy-enforcement"></a>Confronto tra il controllo della gestione e l'applicazione dei criteri
In genere, sono disponibili due approcci per aiutare i processi di gestione toosecure: il controllo e criteri di imposizione. L'uso di entrambi gli approcci offre controlli completi, ma potrebbe non essere consentito in tutte le situazioni. Inoltre, ogni approccio presenta diversi livelli di rischio, il costo e sforzo associato con la gestione della sicurezza, in particolare per quanto riguarda toohello livello di affidabilità singoli e architetture di sistema.

Il monitoraggio, registrazione e controllo fornire una base per il rilevamento e la comprensione delle attività amministrative, ma potrebbe non essere sempre possibile tooaudit tutte le azioni di completamento dettaglio scadenza toohello quantità di dati generati. Controllo efficacia hello dei criteri di gestione di hello è tuttavia consigliabile.

L'applicazione di criteri che include controlli di accesso rigorosi implementa meccanismi a livello di codice che consentono di regolamentare le azioni amministrative e di assicurare che vengano usate tutte le misure di protezione possibili. Registrazione fornisce la prova dell'applicazione, nel record di chi ha fatto cosa, da dove e quando tooa del componente aggiuntivo. Registrazione anche consente tooaudit e crosscheck informazioni su come gli amministratori seguono i criteri e fornisce una prova di attività

## <a name="client-configuration"></a>Configurazione del client
Sono consigliabili tre configurazioni primarie per una workstation con protezione avanzata. differenze principali di Hello tra loro sono costo, usabilità e accessibilità, il mantenimento di un profilo di protezione simili in tutte le opzioni. Hello nella tabella seguente fornisce un'analisi breve di hello vantaggi e ai rischi tooeach. Si noti che "PC aziendali" si riferisce tooa desktop PC configurazione standard di distribuzione per tutti gli utenti di dominio, indipendentemente dai ruoli.

| Configurazione | Vantaggi | Svantaggi |
| --- | --- | --- |
| Workstation autonoma con protezione avanzata |Workstation con controllo rigoroso |Costo più elevato per i desktop dedicati |
| - | Rischio ridotto di exploit dell'applicazione |Maggiore impegno di gestione |
| - | Separazione netta dei compiti | - |
| Computer aziendale come macchina virtuale |Costi hardware ridotti | - |
| - | Separazione di ruolo e applicazioni | - |
| Windows toogo con crittografia unità BitLocker |Compatibilità con la maggior parte dei computer |Verifica delle risorse |
| - | Convenienza economica e portabilità | - |
| - | Ambiente di gestione isolato |- |

È importante che hello finalizzato workstation è host hello e hello guest, senza alcun elemento tra hello ospita l'hardware di sistema e hello operativa. Hello "origine pulita principio" di seguito (noto anche come "sicuro origine) significa che ospitano hello debba essere hello più avanzata. In caso contrario, hello finalizzato workstation (guest) è soggetto tooattacks nel sistema hello in cui è ospitato.

È possibile isolare ulteriormente il funzioni amministrative mediante le immagini del sistema dedicato per ogni workstation di protezione avanzata che hanno solo gli strumenti di hello e le autorizzazioni necessarie per la gestione di Azure selezionare applicazioni cloud e, con specifici oggetti Criteri di dominio Active Directory AD locale in gruppo per hello attività necessarie.

Per gli ambienti IT che non hanno un'infrastruttura locale (ad esempio, nessun accesso tooa per oggetti Criteri di gruppo dell'istanza locale di dominio Active Directory perché tutti i server sono nel cloud hello), un servizio, ad esempio [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) può semplificare la distribuzione e la gestione configurazioni di workstation.

### <a name="stand-alone-hardened-workstation-for-management"></a>Workstation autonoma con protezione avanzata per la gestione
Con una workstation autonoma con protezione avanzata gli amministratori hanno un computer o un computer portatile che può essere usato per attività amministrative e un altro computer o computer portatile separato per le attività non amministrative. Toomanaging una workstation dedicata i servizi di Azure non necessita di altre applicazioni installate. L'uso di workstation che supportano un [Trusted Platform Module](https://technet.microsoft.com/library/cc766159) (TPM) o una tecnologia analoga per la crittografia a livello hardware semplifica l'autenticazione dei dispositivi e contribuisce a evitare determinati attacchi. TPM supporta anche la protezione dell'intero volume dell'unità di sistema hello utilizzando [crittografia unità BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

In uno scenario autonomo workstation finalizzato hello (mostrato sotto), l'istanza locale di hello di Windows Firewall (o un firewall non Microsoft client) è tooblock configurato connessioni, ad esempio RDP in ingresso. messaggio per l'amministratore può accedere toohello finalizzato workstation e avviare una sessione RDP che si connette tooAzure dopo aver stabilito una connessione VPN connettersi con una rete virtuale di Azure, ma non è possibile accedere tooa aziendale PC e usare RDP tooconnect toohello finalizzato workstation se stesso.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Computer aziendale come macchina virtuale
Nei casi in cui una workstation separata di finalizzazione autonoma dei costi di hello proibitivo o poco workstation finalizzato può ospitare un'attività non amministrative tooperform di macchina virtuale.

![][3]

tooavoid diversi rischi di sicurezza derivanti dall'utilizzo di una workstation per la gestione dei sistemi e altre attività quotidiane di lavoro, è possibile distribuire un toohello di macchina virtuale Hyper-V di Windows finalizzato workstation. Questa macchina virtuale può essere utilizzata come hello PC aziendali. ambiente PC aziendali Hello può rimanere isolata da hello Host, che riduce la superficie di attacco e rimuove le attività quotidiane dell'utente hello (ad esempio posta elettronica) da coesistenza con sensibili attività amministrative.

macchina virtuale di PC aziendale Hello eseguito in uno spazio protetto e fornisce le applicazioni utente. host Hello rimane "origine pulita" e impone i criteri di rete strict hello del sistema operativo radice (ad esempio, bloccando l'accesso RDP da una macchina virtuale hello).

### <a name="windows-toogo"></a>Windows tooGo
Un altro toorequiring alternativo una workstation finalizzata autonoma è toouse un [tooGo Windows](https://technet.microsoft.com/library/hh831833.aspx) unità, una funzionalità che supporti una funzionalità di avvio USB sul lato client. Windows tooGo consente immagine sistema isolato tooan tooboot un PC compatibile di utenti in esecuzione da un'unità flash USB crittografata. Fornisce controlli aggiuntivi per gli endpoint di amministrazione remota poiché immagine hello può essere completamente gestito da un gruppo IT aziendale, con i criteri di sicurezza rigidi di una build del sistema operativo minimo, e supporta TPM.

Nella figura seguente hello immagine PE hello è un sistema dominio tooAzure solo tooconnect preconfigurato, richiede l'autenticazione a più fattori e blocca tutto il traffico non-management. Se un utente di avvii hello stessa immagine aziendale di PC toohello standard e viene tentato l'accesso a Gateway Desktop remoto per gli strumenti di gestione di Azure, la sessione hello è bloccata. Windows tooGo diventa sistema operativo di livello radice hello e nessun livelli aggiuntivi sono necessari (host il sistema operativo, hypervisor, macchina virtuale) che potrebbero risultare più vulnerabili agli attacchi di toooutside.

![][4]

È importante toonote siano più facilmente la perdita di un PC desktop medio unità flash USB. Utilizzo di BitLocker tooencrypt hello intero volume, insieme a una password complessa, rende meno probabile che un utente malintenzionato può utilizzare immagine dell'unità di hello per scopi dannosi. Inoltre, se un'unità flash USB hello viene perso, revoca e [emissione di un nuovo certificato di gestione](https://technet.microsoft.com/library/hh831574.aspx) insieme a una rapida password reset può ridurre l'esposizione. I log di controllo amministrativo si trovano all'interno di Azure, non nel client di hello, un'ulteriore riduzione potenziale perdita di dati.

## <a name="best-practices"></a>Procedure consigliate
Prendere in considerazione hello indicazioni per la gestione di applicazioni e dati in Azure.

### <a name="dos-and-donts"></a>Procedure rischiose e procedure consigliate
Non presupporre che verso il basso che è stato bloccato in una workstation altri requisiti di sicurezza comuni non è necessitino toobe soddisfatti. potenziale rischio per Hello è superiore a causa di livelli di accesso con privilegi elevati che in genere dispongono di account di amministratore. Nella tabella hello riportata di seguito sono illustrati esempi di rischi e le alternative consigliate.

| Procedura rischiosa | Procedura consigliata |
| --- | --- |
| Non inviare tramite posta elettronica le credenziali per l'accesso amministratore o altri segreti, ad esempio SSL o certificati di gestione. |Mantenere la riservatezza comunicando a voce i nomi e le password degli account, ma non memorizzandoli nella posta vocale, eseguire un'installazione remota di certificati client/server (tramite una sessione crittografata), eseguire il download da una condivisione di rete crittografata oppure eseguire la distribuzione manuale tramite un supporto rimovibile. |
| - | Gestire in modo proattivo i cicli di vita del certificati di gestione. |
| Non memorizzare le password dell'account senza crittografarle o senza hash nella risorsa di archiviazione dell'applicazione, ad esempio in fogli di calcolo, siti di SharePoint o condivisioni di rete. |Stabilire i principi di gestione della sicurezza e protezione avanzata dei criteri di sistema e applicarle tooyour ambiente di sviluppo. |
| - | Utilizzare [avanzata attenuazione esperienza Toolkit 5.5](https://technet.microsoft.com/security/jj653751) certificato blocco regole siti SSL/TLS tooAzure di tooensure accesso appropriato. |
| Non condividere account e password tra gli amministratori o riutilizzare le password tra più account utente o servizi, in particolare quelli destinati a social media o ad altre attività non amministrative. |Creare un dedicato toomanage account Microsoft alla sottoscrizione di Azure, ovvero un account che non viene utilizzato per la posta elettronica personale. |
| Non inviare file di configurazione tramite posta elettronica. |I file e i profili di configurazione devono essere installati da un'origine attendibile, ad esempio un'unità flash USB crittografata, non da un meccanismo che può essere compromesso facilmente, ad esempio la posta elettronica. |
| Non usare password di accesso vulnerabili o semplici. |Applicare criteri per password complesse, cicli di scadenza (changeon-first-use), timeout della console e blocchi automatici degli account. Usare un sistema di gestione delle password client con autenticazione a più fattori per l'accesso all'insieme di credenziali delle password. |
| Non esporre Gestione porte toohello Internet. |Bloccare le porte di Azure e accesso di gestione toorestrict gli indirizzi IP. Per ulteriori informazioni, vedere hello [sicurezza di rete di Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) white paper relativo alle. |
| - | Usare firewall, VPN e Protezione accesso alla rete per tutte le connessioni di gestione. |

## <a name="azure-operations"></a>Operazioni di Azure
Nell'ambito della gestione Microsoft di Azure, i responsabili del funzionamento e il personale di supporto che accedono ai sistemi di produzione di Azure usano [computer workstation con protezione avanzata con VM](#stand-alone-hardened-workstation-for-management) sottoposti a provisioning per l'accesso di rete aziendale interno e per le applicazioni, ad esempio posta elettronica, Intranet e così via. Tutti i computer workstation di gestione dispongono di moduli TPM, unità di avvio host hello è crittografato con BitLocker e sono unite in join tooa speciali unità organizzativa (OU) nel dominio aziendale principale di Microsoft.

La protezione avanzata del sistema viene applicata tramite Criteri di gruppo, con aggiornamento software centralizzato. Per il controllo e analisi, i registri eventi (ad esempio sicurezza e di AppLocker) vengono raccolti da workstation di gestione e salvati tooa centrale.

Inoltre, dedicate jump caselle nella rete di Microsoft che richiedono l'autenticazione a due fattori sono rete di produzione del tooAzure tooconnect utilizzato.

## <a name="azure-security-checklist"></a>Elenco di controllo di sicurezza di Azure
Ridurre al minimo il numero di hello di attività che gli amministratori possono eseguire in una workstation con protezione avanzata consente di ridurre al minimo la superficie di attacco hello nell'ambiente di sviluppo e gestione. Hello utilizzare seguenti tecnologie toohelp proteggere finalizzata workstation:

* Protezione avanzata di Internet Explorer. il browser Internet Explorer Hello (o qualsiasi web browser, d'altra parte) è un punto di ingresso chiave per il codice dannoso scadenza tooits interazioni completa con i server esterni. Verificare i criteri client e applicare l'esecuzione in modalità protetta, disabilitando i componenti aggiuntivi, disabilitando i download di file e usando i filtri [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Verificare che gli avvisi di sicurezza vengano visualizzati. Sfruttare i vantaggi delle aree Internet e creare un elenco di siti attendibili per cui è stata configurata una protezione avanzata ragionevole. Bloccare tutti i siti e il codice nel browser, ad esempio ActiveX e Java.
* Utente standard. In esecuzione come utente standard offre numerosi vantaggi, hello principale dei quali è che diventa più difficile furto di credenziali di amministratore da software dannoso. Inoltre, un account utente standard non dispone di privilegi elevati nel sistema operativo radice di hello e numerose API e le opzioni di configurazione sono bloccate per impostazione predefinita.
* AppLocker. È possibile utilizzare [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello programmi e script che gli utenti possono eseguire. È possibile eseguire AppLocker in modalità di controllo o di imposizione. Per impostazione predefinita, AppLocker è una regola di autorizzazione che consente agli utenti che dispongono di un toorun token admin tutto il codice client hello. Questa regola esiste amministratori tooprevent da bloccare direttamente out e si applica solo i token tooelevated. Vedere anche l'integrità del codice come parte della [sicurezza di base](http://technet.microsoft.com/library/dd348705.aspx) di Windows Server.
* Firma del codice. La firma del codice per tutti gli strumenti e gli script usati dagli amministratori offre un meccanismo gestibile per la distribuzione di criteri di blocco dell'applicazione. Gli hash non eseguire la scalabilità con codice toohello modifiche rapide e i percorsi di file non forniscono un elevato livello di sicurezza. Le regole di AppLocker deve essere combinato con un PowerShell [criteri di esecuzione](http://technet.microsoft.com/library/ee176961.aspx) che solo codice firmato specifico e script toobe [eseguito](http://technet.microsoft.com/library/hh849812.aspx).
* Criteri di gruppo. Creare un criterio di amministrazione globale che è applicato tooany workstation di dominio utilizzato per la gestione (e blocca l'accesso da tutti gli altri) e gli account toouser autenticati delle workstation.
* Provisioning con miglioramento della sicurezza. Proteggere l'immagine di workstation protezione avanzata della linea di base toohelp protezione contro eventuali manomissioni. Utilizzare le misure di sicurezza quali crittografia e immagini toostore isolamento, le macchine virtuali e gli script e limitare l'accesso (ad esempio utilizzare una controllabile check-in/estrazione processo).
* Applicazione di patch. Mantenere una compilazione coerenza o immagini separato per lo sviluppo, operazioni e altre attività amministrative, cercare le modifiche e malware regolarmente, mantenere compilazione hello backup toodate e attivare solo i computer quando sono necessari.
* Crittografia. Verificare che le workstation di gestione abbiano un toomore TPM abilitare in modo sicuro [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) e BitLocker. Se si utilizza Windows tooGo, utilizzare solo chiavi USB crittografate con BitLocker.
* Governance. Utilizzare oggetti Criteri di gruppo di dominio Active Directory AD toocontrol Windows degli amministratori di hello tutte le interfacce, ad esempio la condivisione file. Includere le workstation di gestione nei processi di controllo, monitoraggio e registrazione. Tenere traccia di tutti gli accessi e gli utilizzi di amministratori e sviluppatori.

## <a name="summary"></a>Riepilogo
L'uso di una configurazione di workstation con protezione avanzata per l'amministrazione dei servizi cloud di Azure, delle macchine virtuali e delle applicazione può contribuire a evitare numerosi rischi e minacce derivanti dalla gestione remota dell'infrastruttura IT essenziale. Azure sia di Windows fornire meccanismi che è possibile utilizzare toohelp proteggere e controllano il comportamento di comunicazioni e l'autenticazione client.

## <a name="next-steps"></a>Passaggi successivi
Hello sono le seguenti risorse tooprovide disponibili informazioni più generali su Azure e i servizi Microsoft, in aggiunta toospecific elementi a cui fa riferimento in questo white paper correlati:

* [Protezione dell'accesso con privilegi](https://technet.microsoft.com/library/mt631194.aspx) – informazioni hello tecniche per la progettazione e creazione di una workstation di amministrazione sicura per la gestione di Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) - informazioni sulle funzionalità della piattaforma Azure che proteggono hello infrastruttura di Azure e hello carichi di lavoro da eseguire in Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) , in cui le vulnerabilità di sicurezza di Microsoft, inclusi i problemi con Azure, è possono creare report o tramite posta elettronica troppo[secure@microsoft.com](mailto:secure@microsoft.com)
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) – tenersi toodate su hello più recente nella sicurezza di Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
