---
title: Procedure consigliate di sicurezza di rete aaaAzure | Documenti Microsoft
description: "Questo articolo fornisce una serie di procedure consigliate per la sicurezza di rete usando le funzionalità integrate di Azure."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Procedure consigliate per la sicurezza della rete di Azure
Microsoft Azure consente di dispositivi di rete tooother macchine virtuali e i dispositivi tooconnect inserendoli in reti virtuali di Azure. Una rete virtuale di Azure è un costrutto di rete virtuale che consente di tooconnect rete virtuale interfaccia schede tooa rete virtuale tooallow basata su TCP/IP le comunicazioni tra dispositivi di rete abilitato. Macchine virtuali di Azure connessa tooan rete virtuale di Azure presenti toodevices tooconnect in grado di hello stessa rete virtuale di Azure diverse reti virtuali di Azure, in Internet hello o anche nelle reti di on-premise.

In questo articolo verrà illustrato un insieme di procedure consigliate per la sicurezza della rete di Azure, Queste procedure consigliate derivano dall'esperienza acquisita con la rete di Azure e l'esperienza dei clienti hello come manualmente.

Per ogni procedura consigliata verrà illustrato:

* Quali consigliabile hello
* Motivo per cui si desidera tooenable consigliata
* Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
* Procedura consigliata toohello alternative possibili
* Informazioni come procedura consigliata hello tooenable

Questo articolo Azure rete le procedure consigliate si basa su un parere di consenso e funzionalità della piattaforma Azure e il set di funzionalità, in cui si trovano in fase di hello in questo articolo è stato scritto. Opinioni e le tecnologie cambiano nel tempo e questo articolo verrà aggiornato in un tooreflect regolarmente le modifiche.

Le procedure consigliate per la sicurezza della rete di Azure discusse in questo articolo includono:

* Segmentare logicamente le subnet
* Controllare il comportamento di routing
* Abilitare il tunneling forzato
* Usare i dispositivi di rete virtuale
* Distribuire reti perimetrali per la suddivisione in zone di sicurezza
* Evitare l'esposizione toohello Internet con collegamenti WAN dedicati
* Ottimizzare il tempo di attività e le prestazioni
* Usare il bilanciamento del carico globale
* Disabilitare l'accesso RDP tooAzure macchine virtuali
* Abilitare il Centro sicurezza di Azure
* Estendere il data center in Azure

## <a name="logically-segment-subnets"></a>Segmentare logicamente le subnet
[Reti virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-network/) sono simili LAN tooa nella rete locale. Hello idea alla base di una rete virtuale di Azure è creare una singolo IP indirizzo basato su spazio rete privata in cui è possibile inserire tutti i [macchine virtuali di Azure](https://azure.microsoft.com/services/virtual-machines/). Hello private spazi degli indirizzi IP disponibili sono in una classe (10.0.0.0/8), hello classe B (172.16.0.0/12) e classe C intervalli (192.168.0.0/16).

Toowhat simile locale, è opportuno toosegment spazio degli indirizzi di dimensioni maggiore hello in subnet. È possibile utilizzare [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) basato sulle subnet: principi toocreate le subnet.

Routing tra subnet verrà eseguita automaticamente e non è necessario toomanually configurare tabelle di routing. Tuttavia, impostazione predefinita hello è che non sono presenti controlli di accesso rete tra subnet hello che è creare su hello rete virtuale di Azure. In ordine toocreate rete controlli di accesso tra subnet, è necessario tooput qualcosa tra subnet hello.

Una delle operazioni di hello è possibile utilizzare questa attività è tooaccomplish un [Network Security Group](../virtual-network/virtual-networks-nsg.md) (gruppo). NSGs sono ispezione dei pacchetti semplici regole Consenti/Nega toocreate il traffico di rete di raggiungere i dispositivi che usano hello 5 tuple (IP origine hello, porta di origine, IP di destinazione, porta di destinazione e il protocollo di livello 4). È possibile concedere o negare il traffico tooand dal singolo indirizzo IP, tooand da più indirizzi IP o persino tooand dall'intera subnet.

Utilizzando NSGs per il controllo di accesso alla rete tra subnet consente tooput risorse appartenenti toohello stessa area di protezione o il ruolo nelle proprie subnet. Ad esempio, si pensi a una semplice applicazione a 3 livelli con un livello Web, un livello di logica di applicazione e un livello di database. Inserire le macchine virtuali appartenenti tooeach di questi livelli in proprie subnet. È quindi necessario utilizzare NSGs toocontrol traffico tra subnet hello:

* Macchine virtuali del livello Web solo possono avviare le macchine connessioni toohello applicazione logica e può accettare solo connessioni da Internet hello
* Macchine virtuali di logica dell'applicazione possono avviare solo connessioni con livello di database e può accettare solo connessioni da livello web hello
* Macchine virtuali del livello del database non può avviare una connessione con un valore di fuori di propria subnet e può accettare solo connessioni dal livello di logica di applicazione hello

toolearn più sui gruppi di sicurezza di rete e come è possibile usarli segmento toologically le reti virtuali di Azure, leggere l'articolo hello [che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) (gruppo).

## <a name="control-routing-behavior"></a>Controllare il comportamento di routing
Quando si inserisce una macchina virtuale su una rete virtuale di Azure, si noterà che la macchina virtuale hello possono connettersi tooany altre macchine virtuali nella stessa rete virtuale di Azure, hello anche se hello altre macchine virtuali si trovano in subnet diverse. motivo per cui è possibile motivo di Hello è che è una raccolta di route di sistema che sono abilitati per impostazione predefinita che consenta questo tipo di comunicazione. Questi route predefinite consentono macchine virtuali in hello stessa rete virtuale di Azure tooinitiate tra loro e con hello Internet (per le comunicazioni in uscita toohello Internet solo).

Benché le route di sistema predefinite hello sono utili per molti scenari di distribuzione, sono disponibili si vogliano toocustomize configurazione del routing hello per le distribuzioni. Queste personalizzazioni consentirà tooconfigure hello successivo hop indirizzo tooreach specifiche destinazioni.

È consigliabile configurare route definite dall'utente quando si distribuisce un dispositivo di sicurezza di rete virtuale, che verrà illustrato in una procedura consigliata successiva.

> [!NOTE]
> le route definite dall'utente non sono necessari e route di sistema predefinite hello funzionerà nella maggior parte dei casi.
>
>

È possibile approfondire le route definite dall'utente e la modalità tooconfigure loro leggendo l'articolo hello [quali sono le route definite dall'utente e l'inoltro IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Abilitare il tunneling forzato
toobetter comprendere il tunneling forzato, è utile toounderstand quali "split tunneling".
l'esempio più comune Hello dello split tunneling viene visualizzato con connessioni VPN. Si supponga stabilire una connessione VPN dalla rete aziendale hotel chat tooyour. Questa connessione consente tooconnect tooresources nella rete aziendale e tutte le comunicazioni tooresources nella rete aziendale passare attraverso i tunnel VPN hello.

Cosa accade quando si desidera tooresources tooconnect su hello Internet? Quando è abilitato lo split tunneling, tali connessioni andare direttamente toohello Internet e non tramite hello VPN tunneling. Alcuni esperti di sicurezza considerare questo toobe un potenziale rischio è pertanto consigliabile che lo split tunneling deve essere disabilitata e tutte le connessioni, quelli destinati hello Internet e quelli destinati alle risorse aziendali, il tunnel VPN hello. Il vantaggio di Hello di questa operazione è toohello che le connessioni Internet quindi forzata tramite dispositivi di sicurezza di hello rete aziendale, se i client VPN hello connesso toohello Internet di fuori del tunnel VPN hello non sarebbe case hello.

Ora Associamo questo backup toovirtual macchine in una rete virtuale di Azure. le route predefinita Hello per una rete virtuale di Azure consentono alle macchine virtuali tooinitiate traffico toohello Internet. Questo troppo può rappresentare un rischio per la sicurezza, le connessioni in uscita potrebbe aumentare la superficie di attacco hello di una macchina virtuale e di essere sfruttate da utenti malintenzionati.
Per questo motivo, è consigliabile abilitare il tunneling forzato su macchine virtuali quando è disponibile una connettività cross-premise tra la rete virtuale di Azure e la rete locale. Si discuterà della connettività cross-premise più avanti in questo documento sulle procedure consigliate per le reti di Azure.

Se non si dispone di una connessione cross-premise, assicurarsi sfruttare i vantaggi dei gruppi di sicurezza di rete (descritto in precedenza) o Azure accessori (illustrato di seguito) di sicurezza rete virtuale, le connessioni in uscita tooprevent toohello Internet dal virtuali di Azure Macchine.

altre informazioni sulle toolearn il tunneling forzato e come tooenable, leggere hello articolo [configurare Tunneling forzato tramite PowerShell e Azure Resource Manager](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Usare i dispositivi di rete virtuale
Mentre i gruppi di sicurezza di rete e il Routing definito dall'utente può fornire un certo grado di sicurezza di rete con hello livelli di rete e di trasporto di hello [modello OSI](https://en.wikipedia.org/wiki/OSI_model), vi saranno toobe situazioni in cui si desidera oppure necessario tooenable sicurezza di alto livello dello stack hello. In tali situazioni, è consigliabile distribuire i dispositivi di sicurezza di rete virtuale forniti dai partner di Azure.

I dispositivi di sicurezza di rete di Azure possono offrire livelli di sicurezza notevolmente migliorati rispetto a quanto offerto dai controlli a livello di rete. Alcune delle funzionalità di sicurezza di rete hello fornite da dispositivi di sicurezza di rete virtuale:

* Funzionalità di firewall
* Rilevamento intrusione/Prevenzione intrusioni
* Gestione vulnerabilità
* Controllo applicazione
* Rilevamento anomalie basato su rete
* Filtro Web
* Antivirus
* Protezione botnet

Se è necessario un livello di sicurezza di rete più elevato, ottenibile con i controlli di accesso a livello di rete, è consigliabile indagare e distribuire i dispositivi di sicurezza di rete virtuale di Azure.

toolearn su quali dispositivi di sicurezza di rete virtuale di Azure sono disponibili e le relative funzionalità, visitare hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) e cercare "sicurezza" e "sicurezza di rete".

## <a name="deploy-dmzs-for-security-zoning"></a>Distribuire reti perimetrali per la suddivisione in zone di sicurezza
Una rete Perimetrale "rete perimetrale" è fisico o segmento di rete logica che viene progettato tooprovide un ulteriore livello di sicurezza fra l'asset e hello Internet. scopo di Hello di hello DMZ è tooplace specializzata dispositivi di controllo di accesso di rete sul bordo hello della rete Perimetrale hello in modo che è consentito solo il traffico desiderato passato hello dispositivo di sicurezza di rete e nella rete virtuale di Azure.

Le reti perimetrali sono utili perché sia possibile concentrarsi Gestione controllo l'accesso alla rete, monitoraggio, registrazione e report sui dispositivi hello bordo hello della rete virtuale di Azure. In questo caso, in genere si abilitano la prevenzione DDoS, i sistemi di rilevamento intrusione/prevenzione intrusioni (IDS/IPS), le regole e i criteri dei firewall, il filtro Web, il software antimalware per la rete e molto altro. dispositivi di sicurezza di rete Hello sit tra hello Internet e la rete virtuale di Azure e hanno un'interfaccia su entrambe le reti.

Anche se si tratta di progettazione di base di una rete Perimetrale hello, esistono molte diverse progettazioni di rete Perimetrale, ad esempio back to back tri-homed, multihomed e altri.

Per tutte le distribuzioni a sicurezza elevata è consigliabile prendere in considerazione la distribuzione di un livello di hello DMZ tooenhance di sicurezza di rete per le risorse di Azure.

altre informazioni sulle DMZ e come toodeploy in Azure, leggere hello articolo toolearn [sicurezza di rete e i servizi Cloud Microsoft](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Evitare l'esposizione toohello Internet con collegamenti WAN dedicati
Molte organizzazioni scelto route IT ibrido hello. In ambiente IT ibrido, alcune delle risorse informative della società hello sono in Azure, mentre gli altri rimangono in locale. In molti casi alcuni componenti di un servizio verranno eseguiti in Azure mentre altri componenti resteranno in locale.

In uno scenario IT ibrido di hello, viene in genere presente un tipo di connettività tra più sedi. Questo cross-premise connettività consente hello società tooconnect loro tooAzure reti locali reti virtuali. Sono disponibili due soluzioni di connettività cross-premise:

* Da sito a VPN
* ExpressRoute

[VPN da sito a sito](../vpn-gateway/vpn-gateway-site-to-site-create.md) rappresenta una connessione privata virtuale tra la rete locale e una rete virtuale di Azure. Questa connessione viene eseguita in hello Internet e permette troppo "tunnel" informazioni all'interno di un collegamento tra la rete e Azure crittografato. La rete VPN da sito a sito è una tecnologia sicura e collaudata, che viene distribuita da aziende di ogni dimensione ormai da decenni. La crittografia del tunnel viene eseguita usando la [modalità tunnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Anche se site-to-site VPN è una tecnologia stabilita, affidabile e attendibile, il traffico all'interno del tunnel hello attraversare hello Internet. Inoltre, la larghezza di banda è relativamente vincolata tooa massimo su 200 Mbps.

Se si richiede un livello di sicurezza o prestazioni eccezionale per le connessioni cross-premise, è consigliabile usare Azure ExpressRoute per la connettività cross-premise. ExpressRoute è un collegamento WAN dedicato tra il percorso locale o un provider di hosting di Exchange. Poiché si tratta di una connessione di telecomunicazioni, i dati non verranno trasmessi tramite Internet hello e pertanto non esposto toohello potenziali rischi inerenti ad comunicazioni Internet.

informazioni sul funzionamento di Azure ExpressRoute toolearn e come toodeploy, leggere articolo hello [Panoramica tecnica su ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Ottimizzare il tempo di attività e le prestazioni
Riservatezza, integrità e disponibilità (CIA) costituiscono triad hello del modello di sicurezza più influente odierna. Riservatezza sulla privacy e sulla crittografia, integrità sta verificando che dati non vengono modificati da personale non autorizzato e la disponibilità è garantisce che gli utenti autorizzati siano in grado di tooaccess informazioni di hello che sono autorizzati tooaccess. La carenza in una di queste aree rappresenta una potenziale violazione della sicurezza.

La disponibilità può essere considerata come una questione di tempi di attività e di prestazioni. Se un servizio non è attivo, non è possibile accedere alle informazioni. Se le prestazioni sono ridotte così come dati hello toomake inutilizzabili, quindi è possibile prendere in considerazione hello dati toobe inaccessibile. Pertanto, da una prospettiva di sicurezza, dobbiamo toodo qualsiasi è possibile che i nostri servizi abbiano tempi di attività ottimali e le prestazioni toomake.
Un metodo comune ed effettivo utilizzato tooenhance disponibilità e prestazioni toouse il bilanciamento del carico. Il bilanciamento del carico è un metodo di distribuzione del traffico di rete tra server che fanno parte di un servizio. Ad esempio, se si dispone di server web front-end come parte del servizio, è possibile utilizzare Bilanciamento del carico del traffico hello toodistribute tra più server web front-end.

Questa distribuzione del traffico maggiore disponibilità perché se uno dei server web hello diventa non disponibile, bilanciamento del carico hello interromperà l'invio di server toothat di traffico e i server toohello il traffico di reindirizzamento che sono ancora online. Il bilanciamento del carico consente inoltre le prestazioni, poiché hello processore, rete e overhead di memoria per le risposte alle richieste viene distribuito in tutti i server con carico bilanciato hello.

È consigliabile impiegare il bilanciamento del carico ogni volta possibile e quando adeguato ai servizi. Prenderemo può risultare appropriato in hello le sezioni seguenti.
Hello il livello di rete virtuale di Azure, Azure offre che tre primario caricate le opzioni di bilanciamento del carico:

* Bilanciamento del carico basato su HTTP
* Bilanciamento del carico esterno
* Bilanciamento del carico interno

## <a name="http-based-load-balancing"></a>Bilanciamento del carico basato su HTTP
Bilanciamento del carico basato su HTTP si basano le decisioni sulle quali toosend connessioni al server utilizzando le caratteristiche del protocollo HTTP hello. Azure offre un bilanciamento del carico HTTP che va dal nome hello del Gateway applicazione.

È consigliabile usare Gateway applicazione di Azure nei casi seguenti:

* Le applicazioni che richiedono le richieste da hello stesso client o utente della sessione tooreach hello stessa macchina virtuale back-end. ad esempio applicazioni carrello e server di posta Web.
* Le applicazioni che desidera server farm web toofree dalla terminazione SSL overhead sfruttando del Gateway applicazione [offload SSL](https://f5.com/glossary/ssl-offloading) funzionalità.
* Applicazioni, ad esempio una rete di distribuzione del contenuto, che richiedono più richieste HTTP su hello stesso toobe di connessione TCP a esecuzione prolungata indirizzati o server back-end toodifferent con bilanciamento di carico.

toolearn più sul funzionamento di Gateway applicazione Azure e come è possibile utilizzare nelle distribuzioni, leggere l'articolo hello [Panoramica di Gateway applicazione](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Bilanciamento del carico esterno
Bilanciamento del carico esterno ha luogo quando le connessioni in ingresso da Internet hello il carico viene bilanciato tra i server che si trova in una rete virtuale di Azure. servizio di bilanciamento del carico esterno di Azure Hello può fornire questa funzionalità ed è consigliabile utilizzarlo quando non sono necessarie le sessioni permanenti hello o eseguire l'offload SSL.

Al contrario tooHTTP-il bilanciamento del carico, hello bilanciamento del carico esterno utilizza informazioni ai livelli di rete e di trasporto hello hello OSI rete modello toomake decisioni su quali server tooload saldo di connessione a.

È consigliabile utilizzare il bilanciamento del carico esterno ogni volta che adottano [applicazioni senza stato](http://whatis.techtarget.com/definition/stateless-app) accettando le richieste in ingresso da Internet hello.

toolearn più sul funzionamento di hello bilanciamento del carico esterno di Azure e come è possibile distribuire, leggere l'articolo hello [Introduzione alla creazione di un bilanciamento del carico con connessione Internet in Gestione risorse con PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Bilanciamento del carico interno
Bilanciamento del carico interno è simile tooexternal bilanciamento del carico e utilizza hello stesso meccanismo tooload saldo connessioni toohello server su cui si basano. Hello solo differenza è che il servizio di bilanciamento del carico hello in questo caso accetta connessioni da macchine virtuali che non sono presenti hello Internet. Nella maggior parte dei casi, le connessioni di hello accettati per il bilanciamento del carico vengano avviate dai dispositivi in una rete virtuale di Azure.

È consigliabile utilizzare interno il bilanciamento del carico per gli scenari che trarranno vantaggio da questa funzionalità, ad esempio quando è necessario tooload saldo connessioni tooSQL server o un server web interno.

toolearn più sul funzionamento di bilanciamento del carico Azure interno e come è possibile distribuire, leggere l'articolo hello [Introduzione alla creazione di un bilanciamento del carico interno tramite PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Usare il bilanciamento del carico globale
Cloud pubblico, rende possibile toodeploy distribuite a livello globale le applicazioni che sono componenti che si trovano in Data Center in tutto il mondo hello. Questo è possibile in Microsoft Azure a causa di presenza di tooAzure Data Center globali. Al contrario tecnologie di bilanciamento del carico di toohello indicato in precedenza, il bilanciamento del carico globale rende possibili toomake servizi disponibili anche quando l'intero Data Center potrebbero non essere disponibili.

È possibile ottenere questo tipo di bilanciamento del carico globale in Azure usando [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/). Consente di gestione traffico è saldo tooload possibili servizi tooyour le connessioni in base alla posizione di hello dell'utente hello.

Se, ad esempio, utente hello effettua un servizio di tooyour richiesta da hello Europa, connessione hello è diretto tooyour services si trova in un Data Center Europa. Questa parte di gestione traffico globale di bilanciamento del carico prestazioni tooimprove consente perché la connessione toohello più vicino al Data Center è più veloce rispetto alla connessione toodatacenters che sono lontano.

Sul lato di disponibilità hello, il bilanciamento del carico globale garantisce che il servizio è disponibile anche se un intero Data Center dovrebbe diventare disponibile.

Ad esempio, se un Data Center di Azure dovrebbe diventare disponibile a causa di motivi tooenvironmental o scadenza toooutages (ad esempio errori di rete regionali), le connessioni tooyour è reindirizzato toohello più vicino al Data Center in linea. Il bilanciamento del carico globale viene effettuato grazie all'uso dei criteri DNS che è possibile creare in Gestione traffico.

È consigliabile utilizzare Gestione traffico per sviluppare una soluzione di cloud che dispone di un ambito ampiamente distribuito in più regioni e richiede il livello più alto di hello del tempo di attività possibili.

toolearn ulteriori informazioni su gestione traffico di Azure e come toodeploy, leggere hello articolo [novità di gestione traffico](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Disabilitare l'accesso RDP/SSH tooAzure macchine virtuali
È possibile tooreach macchine virtuali di Azure utilizzando hello [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) e hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) protocolli (SSH). Questi protocolli rendono possibili toomanage le macchine virtuali da posizioni remote e sono standard in Data Center di elaborazione.

Hello potenziale problema di sicurezza con questi protocolli tramite Internet hello è che gli utenti malintenzionati possono usare vari [attacchi di forza bruta](https://en.wikipedia.org/wiki/Brute-force_attack) tecniche toogain accesso tooAzure macchine virtuali. Una volta che gli utenti malintenzionati hello ottengono l'accesso, possono utilizzare la macchina virtuale come un punto di avvio per comprometterne altri computer nella rete virtuale di Azure o attacchi anche i dispositivi di rete all'esterno di Azure.

Per questo motivo, è consigliabile disabilitare diretto RDP e SSH accesso tooyour macchine virtuali di Azure da hello Internet. Dopo avere da hello che Internet è disabilitato l'accesso diretto RDP e SSH, sono disponibili altre opzioni è possibile utilizzare tooaccess queste macchine virtuali per la gestione remota:

* VPN da punto a sito
* Da sito a VPN
* ExpressRoute

[VPN da punto a sito](../vpn-gateway/vpn-gateway-point-to-site-create.md) è un altro termine per indicare una connessione client/server VPN con accesso remoto. Una VPN point-to-site consente tooan di tooconnect un singolo utente rete virtuale di Azure tramite Internet hello. Una volta stabilita connessione point-to-site hello, hello sarà in grado di toouse RDP o SSH tooconnect tooany le macchine virtuali si trova nella rete virtuale di Azure hello che hello utente connesse toovia point-to-site VPN. Si presuppone che l'utente hello è autorizzato tooreach tali macchine virtuali.

Point-to-site VPN è più sicuro rispetto alle connessioni RDP o SSH dirette perché l'utente hello è tooauthenticate due volte prima macchina virtuale con connessione tooa. In primo luogo, hello utente esigenze tooauthenticate (e autorizzato) connessione di VPN point-to-site hello tooestablish; in secondo luogo, hello utente esigenze tooauthenticate (e autorizzato) tooestablish hello RDP o SSH alla sessione.

Oggetto [VPN site-to-site](../vpn-gateway/vpn-gateway-site-to-site-create.md) si connette una rete tooanother tutta la rete tramite hello Internet. È possibile utilizzare un tooconnect VPN site-to-site il tooan di rete locale rete virtuale di Azure. Se si distribuisce una VPN site-to-site, gli utenti della rete locale sarà in grado di tooconnect toovirtual macchine nella rete virtuale di Azure con RDP hello o protocollo SSH failover hello connessione VPN da sito a sito e non è necessario tooallow diretto RDP o SSH accedere a Internet hello.

È inoltre possibile utilizzare un toohello simile di collegamento WAN dedicato tooprovide funzionalità VPN da sito a sito. Hello principali differenze riguardano 1. collegamento WAN dedicato Hello non deve attraversare Internet hello e 2. i collegamenti WAN dedicati sono in genere più stabili e più efficienti. Azure offre una soluzione di collegamento WAN dedicato in forma di hello di [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Abilitare il Centro sicurezza di Azure
Centro sicurezza di Azure consente di impedire, rilevare e rispondere toothreats e fornisce che maggiore visibilità e controllare i sicurezza hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Il Centro sicurezza di Azure aiuta a ottimizzare e monitorare la sicurezza di rete offrendo:

* Suggerimenti per la sicurezza di rete
* Monitoraggio dello stato di hello della configurazione di sicurezza di rete
* Avvisa toonetwork basato su minacce sia a livello di endpoint e di rete hello

È consigliabile abilitare il Centro sicurezza di Azure per tutte le distribuzioni di Azure.

informazioni sul Centro sicurezza di Azure e come tooenable per le distribuzioni, leggere hello articolo toolearn [tooAzure introduzione Centro sicurezza PC](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Estendere il data center in Azure in modo sicuro
Molte organizzazioni IT aziendali le organizzazioni sono ricerca tooexpand in cloud hello anziché crescita i data center locale. Questa espansione rappresenta un'estensione dell'infrastruttura IT esistente nel cloud pubblico hello. Sfruttando cross-premise opzioni di connettività, è possibile tootreat le reti virtuali di Azure solo un'altra subnet in locale come infrastruttura di rete.

Tuttavia, ci sono molte della pianificazione e problemi di progettazione necessarie toobe risolti prima. Ciò è particolarmente importante nell'area di hello di sicurezza di rete. Uno di toounderstand modi migliori hello come si avvicina a una progettazione è un esempio toosee.

Microsoft ha creato hello [diagramma dell'architettura di riferimento estensione Datacenter](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) e toohelp materiale di supporto è comprendere aspetto un'estensione di Data Center. Questo fornisce un'implementazione di riferimento di esempio che è possibile utilizzare tooplan e progettare un cloud di toohello estensione data center aziendale protetto. È consigliabile rivedere questo tooget documento un'idea dei componenti principali di hello di una soluzione di protezione.

toolearn ulteriori informazioni su come estendere il Data Center di toosecurely in Azure, visitare video hello [tooMicrosoft di estendere il Data Center Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
