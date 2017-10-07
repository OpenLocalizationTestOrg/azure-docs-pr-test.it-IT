---
title: aaaNetwork concetti sulla sicurezza e i requisiti di Azure | Documenti Microsoft
description: " In questo articolo facilita toounderstand è ciò che Microsoft Azure ha toooffer nell'area di hello di sicurezza di rete. Informazioni su quali Azure sono toooffer in ognuna di queste aree è fornire una spiegazione di base per i requisiti e i concetti sulla sicurezza di rete di base. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Panoramica della sicurezza di rete di Azure
Microsoft Azure include un toosupport di infrastruttura di rete affidabile l'applicazione e i requisiti di connettività del servizio. Connettività di rete è possibile tra le risorse disponibili in Azure, tra la versione locale e Azure ospitati, risorse e tooand da hello Internet e Azure.

obiettivo di Hello di questo articolo è toomake più semplice per è toounderstand quali Microsoft Azure ha toooffer nell'area di hello della sicurezza di rete. Vengono fornite spiegazioni di base per i principali concetti e requisiti della sicurezza di rete, È inoltre fornire informazioni su quali Azure ha toooffer in ognuna di queste aree, nonché collegamenti toohelp acquisire una comprensione più approfondita delle aree di interesse.

Cenni preliminari sulla sicurezza di rete di Azure viene descritta la hello seguenti aree:

* Rete di Azure
* Controllo di accesso alla rete
* Accesso remoto sicuro e connettività cross-premise
* Disponibilità
* Risoluzione dei nomi
* Architettura della rete perimetrale
* Monitoraggio e rilevamento delle minacce


## <a name="azure-networking"></a>Rete di Azure
La connettività di rete è indispensabile per le macchine virtuali. toosupport tale requisito, Azure richiede toobe macchine virtuali connesse tooan rete virtuale di Azure. Una rete virtuale di Azure è un costrutto logico basato sull'infrastruttura di rete di Azure fisica hello. Ogni rete virtuale di Azure logica è isolata da tutte le altre reti virtuali di Azure. Ciò consente di assicurare che il traffico di rete nelle distribuzioni non è accessibile tooother i clienti di Microsoft Azure.

Altre informazioni:

* [Panoramica di Rete virtuale.](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Controllo di accesso alla rete
Controllo accesso alla rete consiste hello limitazione tooand connettività da subnet all'interno di una rete virtuale di Azure o dispositivi specifici. obiettivo di Hello del controllo di accesso di rete è toolimit accesso tooyour le macchine virtuali e gli utenti tooapproved di servizi e dispositivi. I controlli di accesso sono basati su consentire o negare decisioni per le connessioni tooand dalla macchina virtuale o un servizio.

Azure supporta numerosi tipi di controllo di accesso alla rete:

* Controllo a livello rete
* Controllo di route e tunneling forzato
* Appliance di sicurezza di rete virtuale

### <a name="network-layer-control"></a>Controllo a livello rete
Qualsiasi distribuzione sicura richiede alcune misure di controllo di accesso alla rete. obiettivo di Hello del controllo di accesso di rete è toorestrict macchina virtuale toohello necessarie ai sistemi di comunicazione e che altri tentativi di comunicazione sono bloccate.

Se è necessario un controllo di accesso a livello di rete di base (basato su protocolli UDP e TCP hello o indirizzo IP), è possibile utilizzare gruppi di sicurezza di rete. Un gruppo di sicurezza di rete (gruppo) è un pacchetto con stato base filtro firewall e consente toocontrol accesso in base a un [5 tuple](https://www.techopedia.com/definition/28190/5-tuple). Gli NSG non forniscono ispezione a livello dell'applicazione o controlli di accesso autenticato.

Altre informazioni:

* [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Controllo di route e tunneling forzato
Hello possibilità toocontrol routing comportamento le reti virtuali di Azure è una funzionalità di controllo di sicurezza critici di rete. Se il routing è configurato in modo non corretto, applicazioni e servizi ospitati nella macchina virtuale possono connettersi a dispositivi toounauthorized inclusi i sistemi di proprietà e gestito da potenziali utenti malintenzionati.

Rete di Azure supporta hello possibilità toocustomize hello il funzionamento del routing del traffico di rete di una rete virtuale di Azure. In questo modo tooalter hello predefinito voci tabella di routing nella rete virtuale di Azure. Il controllo del comportamento di routing consente di assicurarsi che tutto il traffico in ingresso o in uscita da un determinato dispositivo o gruppo di dispositivi nella rete virtuale di Azure avvenga attraverso un percorso specifico.

Ad esempio, nella rete virtuale di Azure potrebbe essere presente un'appliance di sicurezza di rete virtuale. Si desidera assicurarsi che tutti tooand di traffico di rete virtuale di Azure passa attraverso il dispositivo di protezione virtuale toomake. A questo scopo è possibile configurare le [route definite dall'utente](../virtual-network/virtual-networks-udr-overview.md) in Azure.

[Il tunneling forzato](https://www.petri.com/azure-forced-tunneling) è un meccanismo che è possibile utilizzare tooensure che i servizi non sono consentiti tooinitiate toodevices una connessione su hello Internet. Si noti che questo sia diverso da accettare connessioni in ingresso e rispondere toothem. Server web front-end necessario toorequests toorespond dagli host Internet e pertanto è consentito il traffico originato Internet sono consentiti i server web in ingresso toothese e server web hello toorespond.

Ciò che si desidera tooallow è un tooinitiate di server web front-end una richiesta in uscita. Tali richieste potrebbero rappresentare un rischio per la sicurezza, poiché queste connessioni può essere utilizzato toodownload malware. Anche se si desidera che questi front-end server tooinitiate in uscita richiede toohello Internet, potrebbe essere necessario tooforce li toogo tramite locale proxy web in modo che è possibile sfruttare il filtraggio e la registrazione di URL.

In alternativa, è opportuno tooprevent tunneling forzato questo toouse. Quando si abilita il tunneling forzato, tutte le connessioni toohello Internet forzata tramite il gateway locale. È possibile configurare il tunneling forzato sfruttando le route definite dall'utente.

Altre informazioni:

* [Informazioni sulle route definite dall'utente e sull'inoltro IP](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Appliance di sicurezza di rete virtuale
Mentre i gruppi di sicurezza di rete, le route definite dall'utente e il tunneling forzato offrono un livello di protezione a livelli di rete e di trasporto hello di hello [modello OSI](https://en.wikipedia.org/wiki/OSI_model), è possibile che si desideri sicurezza tooenable a livelli superiori di rete hello.

Ad esempio, i requisiti di sicurezza possono includere:

* Autenticazione e autorizzazione prima di consentire l'accesso tooyour applicazione
* Rilevamento delle intrusioni e relativa risposta
* Ispezione a livello dell'applicazione per i protocolli di alto livello
* Filtro degli URL
* Antimalware e antivirus a livello di rete
* Protezione anti-robot
* Controllo di accesso all'applicazione
* Protezione DDoS aggiuntiva (sopra hello protezione fornita hello DDoS l'infrastruttura di Azure stesso)

È possibile accedere a queste funzionalità di sicurezza di rete avanzate usando una soluzione dei partner di Azure. È possibile trovare soluzioni di sicurezza della rete partner Azure più recenti hello visitando hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) e cercare "sicurezza" e "sicurezza di rete".

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Accesso remoto sicuro e connettività cross-premise
Il programma di installazione, configurazione e gestione delle risorse di Azure deve toobe eseguita in remoto. Inoltre, è opportuno toodeploy [ambiente IT ibrido](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) soluzioni che hanno componenti locali e nel cloud pubblico di Azure hello. Questi scenari richiedono l'accesso remoto sicuro.

Rete di Azure supporta i seguenti scenari di accesso remoto sicuro hello:

* Connettere le singole workstation tooan rete virtuale di Azure
* Connettere il tooan di rete locale rete virtuale di Azure con una connessione VPN
* Connettere il tooan di rete locale rete virtuale di Azure con un collegamento WAN dedicato
* Connettersi tooeach altre reti virtuali di Azure

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Connettere le singole workstation tooan rete virtuale di Azure
È possibile che si desideri tooenable singoli sviluppatori o operazioni personale toomanage macchine virtuali e servizi in Azure. Ad esempio, è necessario accedere tooa di macchina virtuale in una rete virtuale di Azure e i criteri di sicurezza non consentono l'accesso remoto RDP o SSH tooindividual le macchine virtuali. In questo caso, è possibile usare una connessione VPN da punto a sito.

connessione VPN Usa hello point-to-site Hello [VPN SSTP](https://technet.microsoft.com/library/cc731352.aspx) protocollo tooenable tooset connessione privata e protetta tra utente hello e hello rete virtuale di Azure. Una volta stabilita connessione VPN hello, hello sarà in grado di tooRDP o SSH su hello VPN collegamento in una macchina virtuale nel hello di rete virtuale di Azure (presupponendo che hello utente può eseguire l'autenticazione e autorizzazione).

Altre informazioni:

* [Configurare una connessione Point-to-Site di tooa di rete virtuale con PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>La connessione di rete locale tooan rete virtuale di Azure con una connessione VPN
È consigliabile tooconnect l'intera rete aziendale, o parti di esso, tooan rete virtuale di Azure. Questo approccio è comune negli scenari di IT ibrido in cui le aziende [estendono il data center locale ad Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). In molti casi le aziende ospitano parti di un servizio in Azure e parti in locale, ad esempio quando una soluzione include server Web front-end in Azure e database back-end in locale. Questo tipo di connessioni "cross-premise" rende anche più sicura la gestione delle risorse residenti in Azure e abilita scenari come l'estensione di controller di dominio Active Directory in Azure.

Un modo tooaccomplish tratta toouse un [VPN site-to-site](https://www.techopedia.com/definition/30747/site-to-site-vpn). Hello differenza tra una VPN da sito a sito e una VPN point-to-site consiste nel fatto che una VPN point-to-site si connette tooan un singolo dispositivo della rete virtuale di Azure, mentre una VPN da sito a sito si connette a una rete virtuale di Azure di tooan tutta la rete (ad esempio la rete locale) . Site-to-site VPN tooan rete virtuale di Azure usare protocollo con modalità hello estremamente sicuro IPsec del tunnel VPN.

Altre informazioni:

* [Creare un gestore delle risorse di VNet con una connessione VPN da sito a sito usando hello portale di Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Pianificazione e progettazione per il gateway VPN](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Connettere la rete virtuale di Azure di tooan di rete locale con un collegamento WAN dedicato
Le connessioni VPN da punto a sito e da sito a sito consentono di abilitare la connettività cross-premise in modo efficace. Tuttavia, alcune organizzazioni valutarle hello toohave seguenti svantaggi:

* Le connessioni VPN spostare i dati su Internet hello: espone queste connessioni toopotential problemi di protezione con lo spostamento dei dati in una rete pubblica. Per le connessioni Internet non è inoltre possibile garantire l'affidabilità e la disponibilità.
* TooAzure le connessioni VPN reti virtuali può essere considerata la larghezza di banda limitata per alcune applicazioni e i motivi, man mano che vengono max out a circa 200 Mbps.

Le organizzazioni che devono hello massimo livello di sicurezza e disponibilità per le connessioni cross-premise in genere utilizzano i collegamenti WAN dedicati tooconnect tooremote siti. Azure offre che Hello possibilità toouse un collegamento WAN dedicato che è possibile utilizzare tooconnect il tooan di rete locale rete virtuale di Azure. e viene abilitato tramite Azure ExpressRoute.

Altre informazioni:

* [Panoramica tecnica relativa a ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Connettere reti virtuali di Azure tooEach altri
È possibile che si toouse molte reti virtuali di Azure per le distribuzioni. Esistono molti motivi per cui è possibile farlo. Uno dei motivi hello potrebbe essere toosimplify gestione; un altro potrebbe avvenire per motivi di sicurezza. Indipendentemente dalla motivazione hello o spiegazione logica per l'inserimento di risorse in reti virtuali di Azure diverse, è possibile che si desideri risorse su ciascuno dei hello reti tooconnect tra loro.

Una soluzione potrebbe consistere per i servizi in uno tooservices tooconnect di rete virtuale di Azure in un'altra rete virtuale di Azure scorrendo"Indietro" tramite hello Internet. connessione Hello iniziare in una rete virtuale di Azure, scorrere hello Internet e quindi tornare destinazione toohello rete virtuale di Azure. Questa opzione espone hello connessione toohello sicurezza problemi inerenti tooany comunicazione basata su Internet.

Un'opzione migliore potrebbe essere toocreate un virtuali di Azure VPN da sito a sito rete virtuale di rete in Azure. Questa rete virtuale virtuali di Azure di rete in Azure site-to-site VPN utilizza hello stesso [in modalità tunnel IPsec](https://technet.microsoft.com/library/cc786385.aspx) protocollo come connessione VPN da sito a sito cross-premise hello indicato in precedenza.

Hello vantaggio offerto dall'utilizzo un virtuali di Azure VPN da sito a sito rete virtuale di rete in Azure è che connessione VPN hello viene stabilita attraverso hello dell'infrastruttura di rete di Azure invece di connettersi tramite Internet hello. In questo modo che si un ulteriore livello di sicurezza rispetto toosite-to-site VPN che si connettono tramite hello Internet.

Altre informazioni:

* [Configurare una connessione da rete virtuale a rete virtuale con Azure Resource Manager e PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Disponibilità
La disponibilità è un componente fondamentale di qualsiasi programma di sicurezza. Se gli utenti e i sistemi non può accedere è necessario tooaccess su hello di rete, hello servizio può essere considerato compromessi. Azure offre tecnologie di rete che hello di supporto seguenti meccanismi di disponibilità elevata:

* Bilanciamento del carico basato su HTTP
* Bilanciamento del carico a livello di rete
* Bilanciamento del carico globale

Il bilanciamento del carico è un meccanismo tooequally distribuiscono le connessioni tra più dispositivi. obiettivi di Hello del bilanciamento del carico sono:

* Aumentare la disponibilità: quando si caricano le connessioni di bilanciamento tra più dispositivi, uno o più dispositivi hello può diventare non disponibile e i servizi di hello in esecuzione su hello rimanenti dispositivi online possono continuare contenuto hello tooserve dal servizio hello
* Migliorare le prestazioni: quando si caricano le connessioni di bilanciamento tra più dispositivi, un singolo dispositivo privo di processore hello tootake raggiunto. In alternativa, hello le richieste di memoria e di elaborazione per la gestione contenuto hello è suddiviso in più dispositivi.

### <a name="http-based-load-balancing"></a>Bilanciamento del carico basato su HTTP
Le organizzazioni che esecuzione i servizi basati su web desiderano spesso toohave un bilanciamento del carico basato su HTTP davanti a tali toohelp di servizi web assicurare adeguati livelli di prestazioni e disponibilità elevata. Al contrario di bilanciamento del carico tootraditional basati sulla rete, hello decisioni di bilanciamento del carico effettuate da servizi di bilanciamento del carico basato su HTTP si basano sulle caratteristiche del protocollo HTTP hello, non sui protocolli di livello di rete e di trasporto hello.

tooprovide è basato su HTTP bilanciamento del carico per i servizi basati sul web, Azure fornisce si hello Gateway applicazione Azure. Hello Gateway applicazione Azure supporta:

* Basato su HTTP bilanciamento del carico: le decisioni di bilanciamento del carico vengono apportate in base al protocollo toohello speciali caratteristiche HTTP
* L'affinità di sessione basato su cookie: questa funzionalità garantisce che le connessioni stabilite rimane intatto tra server e client hello tooone dei server hello dietro il bilanciamento del carico. In questo modo si assicura la stabilità delle transazioni.
* Offload SSL: quando viene stabilita una connessione client con bilanciamento del carico hello, che sessione tra hello client e il servizio di bilanciamento del carico hello è crittografata tramite hello HTTPS (SSL /) protocollo. Tuttavia, in prestazioni tooincrease ordine, è necessario hello opzione toohave hello connessione tra bilanciamento del carico hello e server web hello dietro il protocollo HTTP (non crittografato) hello uso di hello carico del servizio di bilanciamento. Infatti, cui viene fatto riferimento tooas "offload SSL" hello web server dietro il bilanciamento del carico hello rimangano hello processore overhead della crittografia e pertanto deve essere in grado di tooservice richieste più rapidamente.
* URL di routing basato sul contenuto: questa funzionalità rende possibile per le decisioni relative toomake del servizio di bilanciamento carico hello su dove tooforward connessioni basano sull'URL di destinazione hello. offrendo quindi maggiore flessibilità rispetto alle soluzioni che prendono decisioni sul bilanciamento del carico in base agli indirizzi IP.

Altre informazioni:

* [Panoramica del gateway applicazione](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Bilanciamento del carico a livello di rete
Al contrario tooHTTP-il bilanciamento del carico, il livello di rete bilanciamento del carico consente di caricare bilanciamento decisioni basate su IP indirizzo e porta (TCP o UDP) ai numeri.
È possibile ottenere i vantaggi di hello livello bilanciamento carico di rete in Azure utilizzando hello bilanciamento del carico di Azure. Alcune caratteristiche principali di hello bilanciamento del carico di Azure includono:

* Bilanciamento del carico a livello di rete in base all'indirizzo IP e ai numeri di porta.
* Supporto per qualsiasi protocollo a livello dell'applicazione.
* Bilancia il carico tooAzure le macchine virtuali e istanze del ruolo di servizi cloud
* Può essere usato per applicazioni e macchine virtuali con connessione Internet (bilanciamento del carico esterno) e senza connessione Internet (bilanciamento del carico interno).
* Endpoint di monitoraggio, che è utilizzato toodetermine se uno dei servizi di hello bilanciamento del carico hello essere non disponibile

Altre informazioni:

* [Bilanciamento del carico Internet tra più macchine virtuali o servizi](../load-balancer/load-balancer-internet-overview.md)
* [Panoramica del bilanciamento del carico interno](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Bilanciamento del carico globale
Alcune organizzazioni sono interessate livello più elevato di hello di disponibilità possibili. Un modo tooreach che questo obiettivo è toohost applicazioni a livello globale distributed Data Center. Quando un'applicazione è ospitata in data center situati in tutto il mondo hello, è possibile per toobecome un'intera area geopolitici non disponibile e ancora disporre di un'applicazione hello e in esecuzione.

Inoltre toohello vantaggi di disponibilità per ottenere l'hosting di applicazioni in data center distribuiti in modo globale, è anche possibile ottenere vantaggi nelle prestazioni. Utilizzando un meccanismo che indirizza le richieste per Data Center toohello hello servizio più vicino al dispositivo toohello che effettua la richiesta hello, è possono ottenere questi vantaggi di prestazioni.

Il bilanciamento del carico a livello globale può fornire entrambi questi vantaggi. In Azure, è possibile ottenere vantaggi di hello globale di bilanciamento del carico tramite Azure Traffic Manager.

Altre informazioni:

* [Gestione traffico di Azure](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Risoluzione dei nomi
La risoluzione dei nomi è una funzione critica per tutti i servizi ospitati in Azure. Da una prospettiva di sicurezza, compromissione della funzione di risoluzione nome hello può causare richieste di reindirizzamento autore dell'attacco tooan dal sito dell'utente malintenzionato tooan i siti. La sicurezza della risoluzione dei nomi è un requisito per tutti i servizi cloud ospitati.

Esistono due tipi di risoluzione dei nomi che è necessario tooaddress:

* Risoluzione dei nomi interna: viene usata dai servizi nelle reti virtuali di Azure, nelle reti locali o in entrambe. I nomi utilizzati per la risoluzione dei nomi interni non sono accessibili tramite Internet hello. Per una sicurezza ottimale, è importante che lo schema di risoluzione del nome interno non è accessibile tooexternal utenti.
* Risoluzione dei nomi esterna: viene usata da utenti e dispositivi esterni alla rete locale e alle reti virtuali di Azure. Questi sono i nomi di hello che sono visibile toohello Internet e sono utilizzate toodirect connessione tooyour servizi cloud.

Per la risoluzione dei nomi interna sono disponibili due opzioni:

* Server DNS della rete virtuale di Azure: quando si crea una nuova rete virtuale di Azure, viene creato automaticamente un server DNS. Questo server DNS può risolvere i nomi di hello macchine hello presente in tale rete virtuale di Azure. Questo server DNS non è configurabile e viene gestito dal gestore di infrastruttura di Azure hello, rendendo così una soluzione di risoluzione del nome sicuro.
* Portare il proprio server DNS, è possibile hello inserimento di un server DNS di propria scelta nella rete virtuale di Azure. Questo server DNS può costituire che un Active Directory integrato il server DNS o una soluzione dedicata per server DNS fornito da un partner di Azure, è possibile ottenere da hello Azure Marketplace.

Altre informazioni:

* [Panoramica di Rete virtuale.](../virtual-network/virtual-networks-overview.md)
* [Gestire server DNS usati da una rete virtuale](../virtual-network/virtual-network-manage-network.md#dns-servers)

Per la risoluzione DNS esterna sono disponibili due opzioni:

* Ospitare il server DNS personalizzato esterno in locale.
* Ospitare il server DNS personalizzato esterno presso un provider di servizi.

Molte grandi organizzazioni ospitano i propri server DNS in locale. È possibile farlo perché hanno hello rete così competenze e toodo presenza globale.

Nella maggior parte dei casi, è meglio toohost la risoluzione dei nomi DNS di servizi con un provider di servizi. Questi provider di servizi hanno esperienza di rete hello e un'elevata disponibilità tooensure presenza globale per i servizi di risoluzione del nome. Disponibilità è essenziale per DNS di servizi perché se la risoluzione dei nomi dei servizi hanno esito negativo, nessuno potrà essere in grado di tooreach i servizi per Internet.

Azure offre una disponibilità elevata e di soluzione DNS esterno ad alte prestazioni in forma di hello di DNS di Azure. Questa soluzione di risoluzione dei nomi esterni si avvale dell'infrastruttura DNS di Azure in tutto il mondo hello. Consente di toohost il dominio in Azure tramite hello credenziali, API, strumenti e fatturazione come altri servizi di Azure. Come parte di Azure, eredita anche i controlli di sicurezza sicuro hello creati nella piattaforma hello.

Altre informazioni:

* [Panoramica di DNS di Azure](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>Architettura della rete perimetrale
Molte organizzazioni aziendali utilizzano DMZ toosegment toocreate loro reti una zona di buffer tra hello Internet e i relativi servizi. rete hello parte DMZ Hello è considerata un'area con sicurezza bassa e risorse di alto valore non vengono inseriti in tale segmento di rete. Verrà visualizzato in genere dispositivi di sicurezza di rete che hanno un'interfaccia di rete nel segmento di rete Perimetrale hello e un'altra interfaccia connessa tooa rete con macchine virtuali e servizi che accettano le connessioni in ingresso da Internet hello.

Esistono numerose variazioni di progettazione di rete Perimetrale e hello decisione toodeploy una rete Perimetrale, quindi il tipo di rete Perimetrale toouse toouse uno, se si è in base ai requisiti di sicurezza di rete.

Altre informazioni:

* [Servizi cloud Microsoft e sicurezza della rete](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Monitoraggio e rilevamento delle minacce

Azure offre funzionalità toohelp in quest'area chiave con anticipata hello, monitoraggio e rilevamento possibilità toocollect ed esaminare il traffico di rete.

### <a name="azure-network-watcher"></a>Azure Network Watcher
Watcher di rete di Azure include un numero elevato di funzionalità che la risoluzione dei problemi, nonché di fornire un nuovo set di strumenti tooassist con identificazione hello problemi di sicurezza.

[Visualizzazione del gruppo di sicurezza ](/network-watcher/network-watcher-security-group-view-overview.md) agevola la conformità di controllo e protezione delle macchine virtuali e può essere utilizzato tooperform controlli a livello di codice, il confronto dei criteri di linee di base hello definiti da regole tooeffective organizzazione per ognuna delle proprie macchine virtuali. Ciò consente di identificare eventuali deviazioni della configurazione.

[Acquisizione pacchetto](/network-watcher/network-watcher-packet-capture-overview.md) consente tooand di traffico di rete toocapture dalla macchina virtuale hello. Oltre a rendere consentendo toocollect statistiche di rete e la risoluzione dei problemi di hello dell'applicazione acquisizione pacchetto problemi può essere preziose in analisi hello di intrusioni di rete. È inoltre possibile utilizzare questa funzionalità insieme alle funzioni di Azure acquisizioni di rete di toostart nella risposta toospecific Azure gli avvisi.

Per ulteriori informazioni su Watcher di rete di Azure e come test di alcune delle funzionalità di hello nei propri laboratori toostart un quadro hello [watcher di rete di Azure Panoramica del monitoraggio](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Azure watcher di rete è ancora in anteprima pubblica in modo che non può avere hello dello stesso livello di disponibilità e affidabilità come servizi che sono in genere il rilascio di disponibilità. Alcune funzionalità potrebbero non essere supportate, potrebbero avere funzioni limitate o potrebbero non essere disponibili in tutte le località di Azure. Per le notifiche più aggiornate di hello su disponibilità e stato del servizio, controllare hello [pagina degli aggiornamenti di Azure](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats e fornisce che maggiore visibilità e controllare i sicurezza hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio set di soluzioni di sicurezza.

Il Centro sicurezza di Azure aiuta a ottimizzare e monitorare la sicurezza di rete offrendo:

* Suggerimenti per la sicurezza di rete
* Monitoraggio dello stato di hello della configurazione di sicurezza di rete
* Avvisa toonetwork basato su minacce sia a livello di endpoint e di rete hello

Altre informazioni:

* [Introduzione tooAzure Centro sicurezza](../security-center/security-center-intro.md)


### <a name="logging"></a>Registrazione
La registrazione a livello di rete è una funzione chiave per qualsiasi scenario di sicurezza di rete. In Azure, è possibile registrare informazioni relative a livello di rete tooget gruppi di sicurezza di rete la registrazione di informazioni. Con la registrazione dei gruppi di sicurezza di rete si ottengono informazioni da:

* [Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) – questi registri vengono utilizzati tooview tutte le operazioni inviate tooyour Azure sottoscrizioni. Questi log sono abilitati per impostazione predefinita e possono essere utilizzati all'interno di hello portale di Azure. In precedenza erano noti come "log di controllo" o "log operativi".
* Log eventi: forniscono informazioni sulle regole applicate ai gruppi di sicurezza di rete.
* Contatore registri – questi registri informare quante volte ogni regola di gruppo è stato applicato toodeny o consentano il traffico.

È inoltre possibile utilizzare [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), una visualizzazione dei dati potente strumento, tooview e analizzare i log.

Altre informazioni:

* [Log Analytics per i gruppi di sicurezza di rete (NSG)](../virtual-network/virtual-network-nsg-manage-log.md)
