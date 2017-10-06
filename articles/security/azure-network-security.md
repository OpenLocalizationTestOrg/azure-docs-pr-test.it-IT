---
title: Sicurezza di rete aaaAzure | Documenti Microsoft
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
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Sicurezza di rete di Azure

Sappiamo che sicurezza processo cloud hello e come sia importante che trovare informazioni accurate e aggiornate sulla sicurezza di Azure. Uno dei toouse delle ragioni migliore Azure di hello per le applicazioni e servizi è tootake sfruttare ampia gamma di strumenti di sicurezza e funzionalità di Azure. Questi strumenti e funzionalità rendono toocreate possibili soluzioni di protezione su hello piattaforma Azure.

Microsoft Azure garantisce la riservatezza, l'integrità e la disponibilità dei dati dei clienti, assicurando anche al tempo stesso una rendicontazione trasparente. toohelp è comprendere meglio insieme hello di controlli di sicurezza di rete implementata in Microsoft Azure dal punto di vista del cliente hello, in questo articolo, "Sicurezza di rete di Azure," viene scritto tooprovide un'analisi completa la sicurezza di rete hello controlli disponibili con Microsoft Azure.

Questo documento è destinato a tooinform su hello svariati rete controlli che si possono configurare la protezione di hello tooenhance di distribuire soluzioni di hello in Azure. Se si è interessati in quali Microsoft does dell'infrastruttura di rete hello toosecure di hello piattaforma Azure, vedere sezione sicurezza di Azure hello hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Piattaforma Azure

Azure è una piattaforma di servizi cloud pubblici che supporta un'ampia gamma di sistemi operativi, linguaggi di programmazione, framework, strumenti, database e dispositivi.  Può eseguire contenitori Linux con integrazione con Docker, compilare app con JavaScript, Python, .NET, PHP, Java e Node.js e creare back-end per dispositivi iOS, Android e Windows. Servizi cloud di Azure supportano hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si compila, o eseguire la migrazione di risorse IT a, un provider di servizi di cloud pubblico, ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli hello e servizi di hello assicurano toomanage hello del basato su cloud Asset.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende possono soddisfare i requisiti di sicurezza. Inoltre, Azure offre una vasta raccolta di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni dell'organizzazione.

## <a name="abstract"></a>Sunto

I servizi cloud pubblici Microsoft offrono servizi e infrastruttura su scala elevata, capacità di livello aziendale e molte opzioni per la connettività ibrida. È possibile scegliere tooaccess questi servizi tramite Internet hello o con Azure ExpressRoute, che fornisce la connettività di rete privata. piattaforma Microsoft Azure Hello consente tooseamlessly estendere l'infrastruttura cloud hello e compilare le architetture a più livelli. Inoltre, le terze parti possono abilitare capacità avanzate offrendo servizi di sicurezza e appliance virtuali.

I servizi di rete di Azure permettono di ottimizzare la flessibilità, la disponibilità, la resilienza, la sicurezza e l'integrità da progettazione. Questo white paper offre informazioni dettagliate sulle funzioni di rete hello di Azure e informazioni su come i clienti possono utilizzare toohelp funzionalità di sicurezza nativa di Azure protezione delle risorse di informazioni.

Hello deve includere gruppi di destinatari di questo white paper:

- Responsabili tecnici, amministratori di rete e sviluppatori che cercano soluzioni di sicurezza disponibili e supportate in Azure.

-   Indirizzate o dirigenti di processo di business che desiderano tooget una panoramica generale hello Azure tecnologie di rete e i servizi che sono rilevanti in riferimento alla sicurezza di rete in hello cloud pubblico di Azure.

## <a name="azure-networking-big-picture"></a>Quadro generale della rete di Azure
Microsoft Azure include un toosupport di infrastruttura di rete affidabile l'applicazione e i requisiti di connettività del servizio. Connettività di rete è possibile tra le risorse disponibili in Azure, tra la versione locale e Azure ospitati, risorse e tooand da hello Internet e Azure.

![Quadro generale della rete di Azure](media/azure-network-security/azure-network-security-fig-1.png)

Hello [dell'infrastruttura di rete di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) Abilita è toosecurely tooeach altre risorse di Azure di connettersi con le reti virtuali (Vnet). Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello Azure cloud rete dedicata tooyour sottoscrizione. È possibile connettere reti virtuali tooyour sulle reti locali.

Azure supporta dedicato collegamento WAN connettività tooyour locale rete e una rete virtuale di Azure con [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). collegamento Hello tra Azure e il sito utilizza una connessione dedicata che non viene trasmesso hello rete Internet pubblica. Se l'applicazione Azure è in esecuzione in più Data Center, è possibile utilizzare [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute richieste degli utenti in modo intelligente tra istanze di un'applicazione hello. È inoltre possibile inviare traffico tooservices non è in esecuzione in Azure se sono accessibili da Internet hello.

## <a name="enterprise-view-of-azure-networking-components"></a>Visualizzazione a livello aziendale dei componenti di rete di Azure
Azure offre numerosi componenti di rete che sono rilevanti toonetwork discussioni di sicurezza. si descrivono i componenti di rete e lo stato attivo sulla sicurezza hello problemi toothem correlati.

> [!Note]
> Non tutti gli aspetti di rete di Azure sono descritti: prende in esame solo quelli considerati toobe fondamentale nel pianificare e progettare un'infrastruttura di rete sicura per i servizi e applicazioni distribuite in Azure.

In questo articolo, hello copertura seguito funzionalità aziendali di rete di Azure:

-   Connettività di rete di base

-   Connettività ibrida

-   Security Controls

-   Convalida della rete

### <a name="basic-network-connectivity"></a>Connettività di rete di base

Hello [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) Abilita servizio si toosecurely tooeach altre risorse di Azure di connettersi con le reti virtuali (VNet). Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello Azure rete infrastruttura dedicata tooyour sottoscrizione. È inoltre possibile connettere reti virtuali tooeach altri e le reti che usano connessioni VPN da sito a sito locale e dedicati tooyour [collegamenti WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Connettività di rete di base](media/azure-network-security/azure-network-security-fig-2.png)

Con hello comprende che si usano server toohost macchine virtuali in Azure, la domanda hello è la modalità di connessione rete tooa tali macchine virtuali. Hello risposta è che le macchine virtuali di connettersi tooan [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Reti virtuali di Azure sono come le reti virtuale hello è utilizzare locale con le proprie soluzioni di piattaforma di virtualizzazione, ad esempio Microsoft Hyper-V o VMware.

#### <a name="intra-vnet-connectivity"></a>Connettività tra reti virtuali

È possibile connettere reti virtuali tooeach altri, l'abilitazione di risorse collegato tooeither toocommunicate di rete virtuale tra loro attraverso reti virtuali. È possibile utilizzare uno o entrambi hello opzioni tooconnect reti virtuali tooeach altri seguenti:

- **Peering:** risorse Abilita connesso toodifferent reti virtuali di Azure all'interno di hello stesso toocommunicate località di Azure tra loro. Hello larghezza di banda e latenza tra reti virtuali sono hello hello stesso come se le risorse di hello erano connesso toohello stessa rete virtuale. lettura toolearn ulteriori informazioni su peering, [peering di rete virtuale](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Peering](media/azure-network-security/azure-network-security-fig-3.png)

- **Connessione di rete virtuale a:** risorse Abilita connesso toodifferent rete virtuale di Azure all'interno di hello uguali o diversi percorsi di Azure. A differenza del peering, la larghezza di banda tra le reti virtuali è limitata perché il traffico deve passare attraverso un gateway VPN di Azure.

![Connessione da rete virtuale a rete virtuale](media/azure-network-security/azure-network-security-fig-4.png)


ulteriori informazioni sulla connessione di reti virtuali con una connessione di rete virtuale a, leggere hello toolearn [configurare un articolo di connessione di rete virtuale a](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Funzionalità della rete virtuale di Azure:

Come si può notare, una rete virtuale di Azure fornisce le macchine virtuali tooconnect toohello rete in modo che possano connettersi alle risorse di rete tooother in modo sicuro. Tuttavia, la connettività di base è l'inizio di hello solo. Hello seguenti funzionalità del servizio di rete virtuale di Azure hello esporre le caratteristiche di sicurezza di rete virtuale di Azure hello:

-   Isolamento

-   Connettività Internet

-   Connettività delle risorse di Azure

-   Connettività di rete virtuale

-   Connettività locale

-   Filtro del traffico

-   Routing.

**Isolamento**

Le reti virtuali sono [isolate](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) le une dalle altre. È possibile creare reti virtuali separate per lo sviluppo, test e produzione che usa hello stesso [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) blocchi di indirizzi. È altrimenti possibile creare più reti virtuali che usano blocchi di indirizzi CIDR diversi e connettere tra loro le reti. Una rete virtuale può essere segmentata in più subnet.

Azure fornisce la risoluzione dei nomi interna per le macchine virtuali e [servizi Cloud](https://azure.microsoft.com/services/cloud-services/) le istanze del ruolo connesso tooa rete virtuale. È possibile configurare facoltativamente toouse una rete virtuale dei propri server DNS, anziché utilizzare la risoluzione dei nomi interno di Azure.

È possibile implementare più reti virtuali in ogni [sottoscrizione](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) e [area](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) di Azure. Ogni rete virtuale è isolata dalle altre. Per ogni rete virtuale è possibile:

-   Specificare uno spazio indirizzi IP privato personalizzato con indirizzi pubblici e privati (RFC 1918). Azure assegna le risorse collegate toohello rete virtuale un indirizzo IP privato dallo spazio di indirizzi hello, assegnare.

-   Segmento hello rete virtuale in uno o più subnet e allocare una parte della subnet di tooeach spazio di indirizzi di hello rete virtuale.

-   Utilizzare la risoluzione dei nomi fornita da Azure oppure specificare che server DNS per l'utilizzo da risorse connesso tooa rete virtuale. ulteriori informazioni sulla risoluzione dei nomi in reti virtuali, leggere hello toolearn [risoluzione dei nomi per le macchine virtuali e servizi Cloud](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Connettività Internet**

Tutti [macchine virtuali (VM) di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/) e accederanno a istanze del ruolo di servizi Cloud sono connesso tooa rete virtuale toohello Internet, per impostazione predefinita. È inoltre possibile abilitare le risorse toospecific di accesso in ingresso, in base alle esigenze. (VM) e accederanno a istanze del ruolo di servizi Cloud sono connesso tooa rete virtuale toohello Internet, per impostazione predefinita. È inoltre possibile abilitare le risorse toospecific di accesso in ingresso, in base alle esigenze.

Tutte le risorse collegate tooa rete virtuale dispone di connettività in uscita toohello Internet per impostazione predefinita. indirizzo IP privato Hello della risorsa hello è l'indirizzo di rete di origine convertito (SNAT) tooa indirizzo IP da hello dell'infrastruttura di Azure. È possibile modificare la connettività predefinito hello implementando routing personalizzato e filtrare il traffico. ulteriori informazioni sulla connettività Internet in uscita, leggere hello toolearn [informazioni sulle connessioni in uscita in Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate in ingresso risorse tooAzure hello Internet o toocommunicate toohello in uscita deve essere assegnato un indirizzo IP pubblico a Internet senza SNAT, una risorsa. informazioni su indirizzi IP pubblici, leggere hello toolearn [gli indirizzi IP pubblici](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Connettività delle risorse di Azure**

[Risorse di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) , ad esempio servizi Cloud e macchine virtuali possono essere connesso toohello stessa rete virtuale. le risorse di Hello possono connettersi tooeach altri indirizzi IP privati, anche se sono presenti in subnet diverse. Azure offre predefinito routing tra subnet, le reti virtuali e reti locali, in modo da non avere tooconfigure e gestire le route.

È possibile connettere più risorse di Azure tooa rete virtuale, ad esempio macchine virtuali (VM), servizi Cloud, gli ambienti del servizio App e il set di scalabilità di macchine virtuali. Macchine virtuali si connettono tooa subnet all'interno di una rete virtuale tramite un'interfaccia di rete (NIC). altre informazioni sulle schede di rete, leggere hello toolearn [interfacce di rete](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Connettività di rete virtuale**

[Le reti virtuali](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) può essere connesso tooeach altri, l'abilitazione di risorse collegato tooany toocommunicate di rete virtuale con qualsiasi risorsa di qualsiasi altra rete virtuale.

È possibile connettere reti virtuali tooeach altri, l'abilitazione di risorse collegato tooeither toocommunicate di rete virtuale tra loro attraverso reti virtuali. È possibile utilizzare uno o entrambi hello opzioni tooconnect reti virtuali tooeach altri seguenti:

- **Peering:** risorse Abilita connesso toodifferent reti virtuali di Azure all'interno di hello stesso toocommunicate località di Azure tra loro. Hello larghezza di banda e latenza tra reti virtuali è hello stesso come se le risorse di hello erano connesso toohello hello VNet.toolearn stesso ulteriori informazioni su peering, leggere hello [peering di rete virtuale](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Connessione di rete virtuale a:** risorse Abilita connesso toodifferent rete virtuale di Azure all'interno di hello uguali o diversi percorsi di Azure. A differenza del peering, la larghezza di banda tra le reti virtuali è limitata perché il traffico deve passare attraverso un gateway VPN di Azure. ulteriori informazioni sulla connessione di reti virtuali con una connessione di rete toolearn. toolearn leggere più, hello [configurare una connessione di rete virtuale a](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Connettività locale**

Le reti virtuali possono essere connesso troppo[locale](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) reti tramite connessioni di rete privata tra la rete e Azure o tramite una connessione VPN site-to-site failover hello Internet.

È possibile connettere il tooa di rete locale virtuale usando qualsiasi combinazione di hello le opzioni seguenti:

- **Rete privata virtuale (VPN) Point-to-site:** stabilita tra una singola rete connessa tooyour PC e hello rete virtuale. Questo tipo di connessione è molto utile se principianti con Azure o per gli sviluppatori, perché richiede senza modifiche tooyour una rete esistente. connessione Hello Usa la comunicazione di tooprovide crittografato hello SSTP protocollo su hello Internet tra hello PC e hello rete virtuale. Poiché il traffico di hello attraversa hello Internet, è imprevedibile latenza Hello per una VPN point-to-site.

- **VPN da sito a sito:** viene stabilita una connessione tra il dispositivo VPN e un gateway VPN di Azure. Questo tipo di connessione consente a qualsiasi risorsa locale, si autorizza tooaccess una rete virtuale. connessione di Hello è una VPN IPsec/IKE che fornisce comunicazioni crittografate tramite hello Internet tra il dispositivo locale e il gateway VPN di Azure hello. Poiché il traffico di hello attraversa hello Internet, è imprevedibile latenza Hello per una connessione site-to-site.

- **Azure ExpressRoute:** viene stabilita una connessione tra la rete e Azure tramite un partner ExpressRoute. La connessione è privata. Il traffico non attraversa hello Internet. Poiché il traffico non deve attraversare Internet hello, latenza Hello per una connessione ExpressRoute è stimabile. informazioni su tutte le hello connessione opzioni precedenti, leggere hello toolearn [diagrammi della topologia di connessione](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtro del traffico**

Il [traffico di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) delle VM e delle istanze del ruolo Servizi cloud può essere filtrato in ingresso e in uscita per indirizzo IP e porta di origine, indirizzo IP e porta di destinazione e protocollo.

È possibile filtrare il traffico di rete tra subnet utilizzando uno o entrambi hello le opzioni seguenti:

- **Gruppi di sicurezza (gruppo) di rete:** ogni gruppo può contenere più regole di sicurezza in ingresso e in uscita che consentono il traffico toofilter dal protocollo, porta e indirizzo IP di origine e destinazione. È possibile applicare un tooeach gruppo NIC in una macchina virtuale. È inoltre possibile applicare una subnet toohello NSG una scheda di rete o altre risorse di Azure, è connesso. ulteriori informazioni sulla NSGs, leggere hello toolearn [gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Appliance di rete virtuale:** un'appliance di rete virtuale è una VM che esegue software con una funzione di rete, ad esempio un firewall. Consente di visualizzare un elenco di NVAs disponibile in hello Azure Marketplace. Sono anche disponibili appliance virtuali di rete che eseguono l'ottimizzazione WAN e altre funzioni per il traffico di rete. Le appliance virtuali di rete vengono in genere usate con route BGP o definite dall'utente. È inoltre possibile utilizzare un traffico toofilter NVA tra reti virtuali.

**Routing**

Facoltativamente, è possibile sostituire il routing predefinito di Azure configurando route personalizzate o usando route BGP attraverso un gateway di rete.

Azure crea le tabelle di route che consentono le risorse subnet tooany connesso toocommunicate qualsiasi rete virtuale tra loro, per impostazione predefinita. È possibile implementare uno o entrambi i seguenti opzioni toooverride hello hello route predefinite che Azure crea:

- **Le route definite dall'utente:** è possibile creare tabelle di routing personalizzata con le route che controllano in cui il traffico viene indirizzato toofor ogni subnet. altre informazioni sulle route definite dall'utente, leggere hello toolearn [le route definite dall'utente](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Le route BGP:** se ci si connette la rete locale tooyour di rete virtuale utilizzando una connessione Gateway VPN di Azure o ExpressRoute, è possibile propagare tooyour delle route BGP reti virtuali.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>La connettività internet ibrida: la connessione di rete locale tooan
È possibile connettere il tooa di rete locale virtuale usando qualsiasi combinazione di hello le opzioni seguenti:

-   Connettività Internet

-   VPN da punto a sito

-   VPN da sito a sito

-   ExpressRoute

#### <a name="internet-connectivity"></a>Connettività Internet

Come suggerisce il nome, la connettività Internet rende accessibile da Internet, hello i carichi di lavoro in modo da esporre tooworkloads diversi endpoint pubblici che risiedono all'interno di rete virtuale hello. Questi carichi di lavoro potrebbero essere esposte tramite [bilanciamento del carico con connessione Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) o semplicemente assegnando un indirizzo IP pubblico indirizzi toohello macchina virtuale. In questo modo diventa possibile per tutti gli elementi presenti su hello Internet toobe in grado di tooreach tale macchina virtuale, a condizione che un firewall host, [(gruppo) di gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), e [le route definite dall'utente](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) consentire che toohappen.

In questo scenario, è possibile esporre un'applicazione che richiede toobe pubblica toohello Internet e di essere in grado di tooconnect tooit da ovunque, o da percorsi specifici a seconda della configurazione di hello dei carichi di lavoro.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>VPN da punto a sito o VPN da sito a sito
Questi due rientra nella hello stessa categoria. È necessario che entrambi i toohave di rete virtuale, un Gateway VPN ed è possibile connettersi utilizzando un Client VPN per la workstation come parte di hello tooit [configurazionePoint-to-Site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) oppure è possibile configurare locale [dispositivo VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe in grado di tooterminate una VPN site-to-site. In questo modo, i dispositivi in locale possono connettersi tooresources all'interno di hello rete virtuale.

Una configurazione da punto a sito (P2S) consente di creare una connessione sicura da una rete virtuale di computer tooa singoli client. P2S è una connessione VPN tramite SSTP (Secure Sockets Tunneling Protocol).

![VPN da punto a sito](media/azure-network-security/azure-network-security-fig-5.png)

Le connessioni Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio da casa o un centro di conferenze o quando si dispone solo di pochi client che richiedono una rete virtuale di tooconnect tooa.

Le connessioni P2S non richiedono un dispositivo VPN o un indirizzo IP pubblico. Stabilire una connessione VPN hello da computer client hello. Pertanto, P2S non è consigliabile tooAzure tooconnect modo nel caso in cui necessaria una connessione permanente da molti dispositivi locali e i computer tooyour rete di Azure.

![VPN da sito a sito](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Per ulteriori informazioni sulle connessioni Point-to-Site, vedere hello [Point-to-Site FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2).

Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente. Questa connessione viene eseguita in hello Internet e permette troppo "tunnel" informazioni all'interno di un collegamento tra la rete e Azure crittografato. La rete VPN da sito a sito è una tecnologia sicura e collaudata, che viene distribuita da aziende di ogni dimensione ormai da decenni. La crittografia del tunnel viene eseguita usando la [modalità tunnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Anche se site-to-site VPN è una tecnologia stabilita, affidabile e attendibile, il traffico all'interno del tunnel hello attraversare hello Internet. Inoltre, la larghezza di banda è relativamente vincolata tooa massimo pari a circa 200 Mbps.

Se si richiede un livello di sicurezza o prestazioni eccezionale per le connessioni cross-premise, è consigliabile usare Azure ExpressRoute per la connettività cross-premise. ExpressRoute è un collegamento WAN dedicato tra il percorso locale o un provider di hosting di Exchange. Poiché si tratta di una connessione di telecomunicazioni, i dati non verranno trasmessi tramite Internet hello e pertanto non esposto toohello potenziali rischi inerenti ad comunicazioni Internet.

> [!Note]
> Per altre informazioni al riguardo, vedere [Informazioni sul gateway VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Collegamento WAN dedicato
Microsoft Azure ExpressRoute consente di estendere le reti locali in hello Azure su una connessione privata dedicata mediante un provider di connettività.

Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. In questo modo toooffer connessioni ExpressRoute più affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet.

![ Collegamento WAN dedicato](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Per informazioni su come tooconnect tooMicrosoft la rete tramite ExpressRoute, vedere [modelli di connettività di ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) e [Panoramica tecnica su ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Come con le opzioni di hello site-to-site VPN, ExpressRoute consente inoltre tooresources tooconnect che non sono necessariamente in una sola rete virtuale. A seconda di hello SKU, infatti, è possibile connettere reti virtuali too10. Se si dispone di hello [componente aggiuntivo premium](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), connessioni tooup too100 reti sono possibili, a seconda della larghezza di banda. informazioni su ciò che questi tipi di connessioni cerca ad esempio, leggere toolearn [diagrammi della topologia di connessione](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Controlli di sicurezza
Una rete virtuale di Azure offre una rete logica e sicura, isolata dalle altre reti virtuali, e supporta molti controlli di sicurezza usati nelle reti locali. I clienti di creare la propria struttura utilizzando: subnet, usare i propri intervallo di indirizzi IP privati, configurare le tabelle di route, gruppi di sicurezza di rete di controllo di accesso (elenchi), gateway e dispositivi virtuali toorun i carichi di lavoro nel cloud hello.

di seguito Hello sono controlli di sicurezza, che è possibile scegliere le reti virtuali di Azure:

-   Controlli di accesso alla rete

-   Route definite dall'utente

-   Appliance di sicurezza di rete

-   gateway applicazione

-   Web application firewall di Azure

-   Controllo di disponibilità di rete

#### <a name="network-access-controls"></a>Controlli di accesso alla rete
Mentre hello rete virtuale di Azure (VNet) è l'elemento fondamentale di hello del modello di rete Azure fornisce isolamento e protezione, hello [gruppi di sicurezza (rete)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) sono hello principale dello strumento consentono il traffico di rete tooenforce e controllo regole a livello di rete hello.

![ Controlli di accesso alla rete](media/azure-network-security/azure-network-security-fig-8.png)


È possibile controllare l'accesso per consentire o negare la comunicazione tra i carichi di lavoro hello in una rete virtuale, da sistemi in reti tramite connettività cross-premise, o la comunicazione Internet diretta.

Nel diagramma hello, sia le reti virtuali e NSGs risiedono in un livello specifico nello stack di sicurezza complessiva Azure hello, dove NSGs UDR e ai dispositivi di rete virtuale possono essere utilizzato toocreate sicurezza limiti tooprotect hello le distribuzioni di applicazioni nella rete hello protetto.

NSGs un traffico tooevaluate 5 tuple (e vengono utilizzati nelle regole di hello che è configurare per hello NSG):

-   [Indirizzo IP di origine e di destinazione](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Porta di origine e di destinazione](https://technet.microsoft.com/library/dd197515)

-   Protocollo: [Transmission Control Protocol (TCP)](https://technet.microsoft.com/library/cc940037.aspx) o [User Datagram Protocol (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Ciò significa che è possibile controllare l'accesso tra una singola macchina virtuale e un gruppo di macchine virtuali, o un singolo tooanother VM singola macchina virtuale, o tra le subnet intere. Anche in questo caso, occorre tenere presente che si tratta di un semplice filtro dei pacchetti con stato, non di un'ispezione completa dei pacchetti. In un gruppo di sicurezza di rete non c'è alcuna convalida del protocollo, IDS a livello di rete o funzionalità IPS.

Il gruppo di sicurezza di rete include alcune regole predefinite che è opportuno conoscere. Si tratta di:

-   **Consentire il traffico all'interno di una rete virtuale specifica:** tutte le macchine virtuali su hello stessa rete virtuale di Azure possono comunicare tra loro.

-   **Consenti tooinbound di bilanciamento del carico di Azure:** questa regola consente il traffico da qualsiasi indirizzo di destinazione tooany indirizzo origine servizio di bilanciamento del carico di Azure hello.

-   **Nega tutto in ingresso:** questa regola blocca tutto il traffico acquisti da hello Internet che è stato consentito in modo esplicito.

-   **Consenti tutto il traffico in uscita toohello Internet:** questa regola consente a macchine virtuali tooinitiate connessioni toohello Internet. Per evitare queste connessioni avviate, toocreate tooblock una regola tali connessioni o se applicare il tunneling forzato.

#### <a name="system-routes-and-user-defined-routes"></a>Route di sistema e route definite dall'utente

Quando si aggiunta macchine virtuali (VM) tooa rete virtuale (VNet) in Azure, noterai che le macchine virtuali hello siano in grado di toocommunicate tra loro attraverso la rete hello, automaticamente. Non è necessario un gateway, toospecify anche se hello macchine virtuali presenti in subnet diverse.

Hello lo stesso vale per la comunicazione da hello macchine virtuali toohello rete Internet pubblica e rete locale di tooyour anche quando una connessione ibrida da Azure tooyour proprietario Data Center è presente.

![Le route di sistema](media/azure-network-security/azure-network-security-fig-9.png)

Questo flusso di comunicazione è possibile poiché Azure Usa una serie di sistema route toodefine come flussi di traffico IP. Route di sistema di controllare il flusso di hello di comunicazione in hello seguenti scenari:

-   Dall'interno hello stessa subnet.

-   Da un tooanother subnet all'interno di una rete virtuale.

-   Da macchine virtuali toohello Internet.

-   Da una rete virtuale tooanother rete virtuale tramite un gateway VPN.

-   Da una rete virtuale tramite il Peering reti virtuali di tooanother rete virtuale ([servizio concatenamento](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   Da una rete virtuale tooyour rete locale tramite un gateway VPN.

Molte aziende dispongono di sicurezza rigidi e i requisiti di conformità che richiedono l'ispezione locale della rete tutti i pacchetti tooenforce specifici criteri. Azure fornisce un meccanismo denominato [il tunneling forzato](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) che instrada il traffico da hello locale tooon macchine virtuali, creare una route personalizzata o da [protocollo BGP (Border Gateway)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) annunci tramite ExpressRoute o VPN.

Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente. Reindirizzamento del traffico tooan locale sito viene espresso come un gateway VPN di Azure toohello di Route predefinita.

Hello nella sezione seguente sono elencate la limitazione corrente hello della tabella di routing hello e le route per una rete virtuale di Azure:

-   Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata. tabella di routing sistema Hello è hello seguenti tre gruppi di route:

 -  **Route di rete virtuale locale:** direttamente toohello destinazione macchine virtuali in hello stessa rete virtuale

 - **Route locali:** gateway VPN di Azure toohello

 -  **Route predefinita:** direttamente toohello Internet. I pacchetti destinati toohello gli indirizzi IP privati non coperti da route hello due precedenti vengono eliminati.

-   Con la versione di hello delle route definite dall'utente, è possibile creare una route predefinita di un tooadd tabella di routing e quindi associare hello routing tabella tooyour rete virtuale subnet tooenable forzato tunneling su queste subnet.

-   È necessario un sito"predefinito" tooset tra rete virtuale connessa toohello hello cross-premise siti locali.

-   Il tunneling forzato deve essere associato a una rete virtuale che disponga di un gateway VPN (non un gateway statico).

- Il tunneling forzato ExpressRoute non viene configurato tramite questo meccanismo, ma è invece abilitato annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering.

> [!Note]
> Per ulteriori informazioni, vedere hello [documentazione di ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) per ulteriori informazioni.

#### <a name="network-security-appliances"></a>Appliance di sicurezza di rete
Mentre i gruppi di sicurezza di rete e le route definite dall'utente possono fornire un certo grado di sicurezza di rete con hello livelli di rete e di trasporto di hello [modello OSI](https://en.wikipedia.org/wiki/OSI_model), vi saranno toobe situazioni in cui si desidera o necessario tooenable protezione a livelli superiori dello stack di rete hello. In tali situazioni, è consigliabile distribuire i dispositivi di sicurezza di rete virtuale forniti dai partner di Azure.

![Appliance di sicurezza di rete](./media/azure-network-security/azure-network-security-fig-10.png)

Dispositivi di sicurezza di rete di Azure migliorano la sicurezza di rete virtuale e le funzioni di rete e che siano disponibili da numerosi fornitori tramite hello [Azure Marketplace](https://azuremarketplace.microsoft.com). Queste Appliance virtuale sicurezza possono essere distribuito tooprovide:

-   Firewall a disponibilità elevata

-   Prevenzione delle intrusioni

-   Rilevamento delle intrusioni

-   Web application firewall

-   Ottimizzazione WAN

-   Routing.

-   Bilanciamento del carico.

-   VPN

-   Gestione dei certificati

-   Active Directory

-   Autenticazione a più fattori

#### <a name="application-gateway"></a>gateway applicazione

Il [gateway applicazione di Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni.

 ![gateway applicazione](./media/azure-network-security/azure-network-security-fig-11.png)

Gateway applicazione permette di disponibilità e prestazioni di toooptimize web farm tramite l'offload della CPU con utilizzo intensivo SSL terminazione toohello gateway applicazione (offload SSL). Offre inoltre funzionalità di routing di livello 7, tra cui:

-   Distribuzione round-robin del traffico in ingresso

-   Affinità di sessione basata su cookie

-   Routing basato su percorsi URL

-   Capacità toohost più siti Web protetti da un singolo Gateway applicazione


Oggetto [firewall applicazione web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) viene inoltre fornito come parte del gateway applicazione hello. Questo offre una protezione di applicazioni tooweb vulnerabilità web e gli attacchi comuni. Il gateway applicazione può essere configurato come gateway con connessione Internet, come gateway solo interno o come una combinazione di queste due opzioni.

È possibile eseguire il Web application firewall del gateway applicazione in modalità di rilevamento o di prevenzione. Un caso di utilizzo comune è per gli amministratori toorun traffico tooobserve modalità di rilevamento per modelli pericolosi. Quando vengono rilevati potenziali attacchi, attivare la modalità tooprevention blocca il traffico in ingresso sospetto.

 ![gateway applicazione](./media/azure-network-security/azure-network-security-fig-12.png)

Inoltre, WAF di Gateway applicazione consente di monitorare le applicazioni web da attacchi di utilizzo di un log in tempo reale di WAF integrata con [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) e [Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/) tootrack WAF avvisi e monitorare facilmente le tendenze.

Hello JSON formattato log passa direttamente account di archiviazione del cliente toohello. L'utente ha il controllo completo sui log e può applicare i propri criteri di conservazione.

È anche possibile inserire i log nel proprio sistema di analisi usando l'[integrazione dei log di Azure](https://aka.ms/AzLog). WAF log vengono inoltre integrato con [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) quindi è possibile usare OMS log analitica tooexecute sofisticato granulari per le query.

#### <a name="azure-web-application-firewall-waf"></a>Web application firewall (WAF) di Azure

Le applicazioni Web sono sempre più destinazioni di attacchi dannosi che sfruttano le vulnerabilità di note comuni, ad esempio SQL injection, attacchi di cross-site scripting e altri attacchi che vengono visualizzati in hello [primi OWASP 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Prevenzione degli attacchi tramite questo tipo in un'applicazione hello richiede attività di manutenzione rigorosi, l'applicazione di patch e il monitoraggio a più livelli della topologia applicazione hello.

 ![Web application firewall (WAF) di Azure](./media/azure-network-security/azure-network-security-fig-13.png)

Un [Web application firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) centralizzato permette di proteggersi dagli attacchi Web e semplifica la gestione della sicurezza, senza richiedere alcuna modifica alle applicazioni.

Una soluzione WAF può inoltre riflettere minaccia alla sicurezza tooa più veloce per l'applicazione di patch una vulnerabilità nota in una posizione centrale e la protezione di ognuna delle singole applicazioni web. Gateway applicazione esistente può essere facilmente convertito tooa web applicazione firewall abilitato applicazioni gateway.

#### <a name="network-availability-controls"></a>Controlli di disponibilità di rete

Sono disponibili il traffico di rete toodistribute diverse opzioni utilizzando Microsoft Azure. Queste opzioni funzionano in modo diverso, vantano un set di funzionalità differenti e supportano diversi scenari. Possono essere utilizzate singolarmente o in combinazione.

Seguenti sono hello i controlli di disponibilità di rete:

-   Azure Load Balancer

-   gateway applicazione

-   Gestione traffico

**Azure Load Balancer**

Offre prestazioni elevate, disponibilità e la rete tooyour applicazioni. Si tratta di un servizio di bilanciamento del carico di livello 4 (TCP, UDP) che distribuisce il traffico in ingresso tra istanze integre di servizi definiti in un set con carico bilanciato.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer può essere configurato per:

-   Caricare il saldo in ingresso Internet traffico toovirtual macchine. Questa configurazione è nota come [bilanciamento del carico Internet tra più macchine virtuali o servizi](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Bilanciare il carico del traffico tra macchine virtuali in una rete virtuale, tra macchine virtuali nei servizi cloud o tra computer locali e macchine virtuali in una rete virtuale cross-premise. Questa configurazione è nota come [bilanciamento del carico interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Inoltrare il traffico esterno tooa macchina virtuale specifica.

Tutte le risorse nel cloud hello necessario raggiungibile da Internet hello un toobe di indirizzo IP pubblico. infrastruttura di cloud Hello in Azure Usa gli indirizzi IP non instradabili per le risorse. Azure Usa il servizio NAT (Network address translation) con toohello toocommunicate gli indirizzi IP pubblico Internet.

 **Gateway applicazione**

 Gateway applicazione funziona al livello di applicazione hello (livello 7 nello stack di riferimento di hello OSI rete). Opera come un servizio proxy inverso, chiusura connessione client hello e inoltro richiede gli endpoint tooback-end.

 **Gestione traffico**

Gestione traffico di Microsoft Azure consente di distribuzione hello toocontrol del traffico utente per gli endpoint del servizio in diversi Data Center. Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e macchine virtuali di Azure. È anche possibile usare Gestione traffico con endpoint esterni, non di Azure.

Gestione traffico Usa hello sistema DNS (Domain Name) toodirect client richiede un endpoint di toohello più appropriato in base a un [metodo di routing del traffico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) e l'integrità di hello degli endpoint hello. Traffic Manager fornisce una gamma di routing del traffico metodi toosuit le diverse esigenze applicative, integrità dell'endpoint [monitoraggio](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)e il failover automatico. Gestione traffico è toofailure resilienti, ad esempio hello malfunzionamento di un'intera regione di Azure.

Gestione traffico di Azure consente distribuzione hello toocontrol del traffico tra l'endpoint dell'applicazione. Un endpoint è un servizio con connessione Internet ospitato all'interno o all'esterno di Azure.

Gestione traffico offre due vantaggi principali:

-   Distribuzione del traffico in base tooone di numerose [metodi di routing del traffico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Monitoraggio continuo dell'integrità degli endpoint](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) e failover automatico quando si verificano errori sugli endpoint.

Quando un client tenta tooconnect tooa servizio, innanzitutto necessario risolvere il nome DNS hello dell'indirizzo IP del servizio tooan hello. client Hello si connette quindi il servizio hello tooaccess di toothat IP indirizzo. Gli endpoint in base alle regole di hello del metodo di routing del traffico hello del servizio Gestione traffico Usa DNS toodirect client toospecific. I client si connettono direttamente endpoint toohello selezionato. Gestione traffico non è un proxy o un gateway. Gestione traffico non vedere il passaggio tra hello client e servizio di hello del traffico hello.

### <a name="azure-network-validation"></a>Convalida della rete di Azure

La convalida della rete di Azure è tooensure che hello rete di Azure funziona come viene configurato e la convalida può essere eseguita usando hello rete hello toomonitor disponibili servizi e funzionalità. Con il Watcher di rete di Azure, è possibile accedere a un gran numero di registrazione e le funzionalità di diagnostica che consentono insights toounderstand le prestazioni di rete e l'integrità. Tali funzionalità sono accessibili tramite il portale, PowerShell, l'interfaccia della riga di comando, API Rest e SDK.

Sicurezza operativa Azure fa riferimento toohello servizi, i controlli e toousers disponibili funzionalità per la protezione dei dati, applicazioni e altre risorse in Microsoft Azure. Sicurezza operative di Azure si basa su un framework che incorpora informazioni hello ottenute tramite una varie funzionalità che sono univoci tooMicrosoft, tra cui Microsoft Security Development Lifecycle (SDL), Microsoft Security risposta Centre hello hello programma e sensibilizzare complete panorama delle minacce sicurezza informatica hello.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure Storage analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Gestione risorse di Azure

#### <a name="azure-resource-manager"></a>Azure Resource Manager

persone Hello e processi che utilizzano Microsoft Azure sono ad esempio funzionalità di sicurezza della piattaforma hello più importanti hello. Questa sezione illustra le funzionalità dell'infrastruttura del data center globale di Microsoft che consentono di migliorare e gestire la sicurezza, la continuità e la privacy.

infrastruttura di Hello per l'applicazione è in genere costituito da numerosi componenti, forse una macchina virtuale, account di archiviazione e rete virtuale, o un'app web, database, server di database e i servizi di terze parti. Questi componenti non appaiono come entità separate, ma come parti correlate e interdipendenti di una singola entità Si desidera toodeploy, gestire e monitorarli come gruppo. Gestione risorse di Azure consente toowork con risorse hello nella soluzione come gruppo.

È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per la soluzione in un'operazione singola, coordinata. Per la distribuzione viene usato un modello; questo modello può essere usato per diversi ambienti, ad esempio di testing, staging e produzione. Gestione risorse offre sicurezza, il controllo e assegnazione di tag toohelp funzionalità Gestione delle risorse dopo la distribuzione.

**vantaggi di Hello dell'utilizzo di gestione risorse**

Gestione risorse offre numerosi vantaggi:

-   È possibile distribuire, gestire e monitorare tutte le risorse di hello per la soluzione come un gruppo, anziché gestire singolarmente queste risorse.

-   Più volte, è possibile distribuire la soluzione in tutto il ciclo di sviluppo hello e che le risorse vengono distribuite in uno stato coerente di fiducia.

-   È possibile gestire l'infrastruttura con modelli dichiarativi, piuttosto che con script.

-   È possibile definire le dipendenze di hello tra risorse, in modo che vengono distribuiti nell'ordine corretto hello.

-   È possibile applicare tooall servizi di controllo di accesso nel gruppo di risorse perché il controllo di accesso basato sui ruoli (RBAC) in modo nativo viene integrato nella piattaforma di gestione di hello.

-   È possibile applicare tag tooresources toologically organizzare tutte le risorse di hello nella sottoscrizione.

-   È possibile ottenere informazioni dettagliate sulla fatturazione per l'organizzazione visualizzando i costi di un gruppo di risorse che condividono un tag.

> [!Note]
> Gestione risorse fornisce un nuovo toodeploy modo e gestire le soluzioni. Se è stato utilizzato un modello di distribuzione precedente hello e si desidera toolearn sulle modifiche di hello, vedere [distribuzione classica e gestione di informazioni sulle risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Registrazione e monitoraggio della rete di Azure

Azure offre numerosi strumenti toomonitor, impedire, rilevare e rispondere toonetwork gli eventi di sicurezza. Hello tooyou disponibili più potenti strumenti in questa area includono:

-   Network Watcher

-   Monitoraggio a livello di risorsa di rete

-   Log Analytics

### <a name="network-watcher"></a>Network Watcher

[Controllo di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -basata sullo Scenario di monitoraggio viene fornito con funzionalità di hello Watcher di rete. Il servizio include l'acquisizione pacchetti, l'hop successivo, la verifica del flusso IP, la visualizzazione dei gruppi di sicurezza e i registri dei flussi dei gruppi di sicurezza di rete. Monitoraggio a livello di scenario è inclusa una visualizzazione di tooend finale delle risorse di rete in Monitoraggio risorse di rete di contrasto tooindividual.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

Watcher di rete è un servizio internazionale che consente di toomonitor e diagnosticare le condizioni di livello rete scenario, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.

Watcher di rete presenta attualmente hello seguenti funzionalità:

#### <a name="topology"></a>Topologia

La [topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) restituisce un grafico delle risorse di rete in una rete virtuale. grafico di Hello illustra l'interconnessione hello tra hello risorse toorepresent hello fine tooend la connettività di rete. Nel portale di hello topologia restituisce oggetti risorsa hello in base a intervalli di rete virtuale. relazioni Hello sono rappresentate dalle linee tra le risorse di hello di fuori di area di hello Watcher di rete, anche se nella risorsa hello gruppo non verrà visualizzato. risorse di Hello restituite nella visualizzazione portale hello sono un subset di componenti che sono rappresentate hello. toosee hello completo elenco di risorse di rete, è possibile utilizzare [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) o [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Poiché le risorse vengono restituite in due relazioni vengono modellati in connessione hello tra essi.

- **Contenimento**: la rete virtuale contiene una subnet che contiene una scheda di interfaccia di rete.

- **Associazione**: una scheda di interfaccia di rete è associata a una macchina virtuale.

#### <a name="variable-packet-capture"></a>Acquisizione pacchetti variabile

Controllo di rete [acquisizione pacchetto variabile](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) consente toocreate pacchetto acquisizione sessioni tootrack traffico tooand da una macchina virtuale. Acquisizione di pacchetti consente toodiagnose anomalie di rete sia reattivo e proactivity. Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.

L'acquisizione di pacchetti è un'estensione macchina virtuale che viene avviata da remoto tramite Network Watcher. Questa funzionalità semplifica il compito di hello di esecuzione manuale di acquisizione pacchetto eseguita nella macchina virtuale desiderata hello, che consente di risparmiare tempo prezioso. Acquisizione pacchetto può essere attivato tramite il portale di hello, PowerShell, CLI o API REST. Un esempio di modalità di attivazione è rappresentata dagli avvisi della macchina virtuale.

#### <a name="ip-flow-verify"></a>Verifica del flusso IP

[Verificare i flussi IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) controlla se un pacchetto è consentito o negato tooor da una macchina virtuale in base alle informazioni di 5 tuple. Tali informazioni sono costituite da direzione, protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota. Se i pacchetti hello viene negato da un gruppo di sicurezza, viene restituito il nome di hello della regola hello negato pacchetti hello. Mentre è possibile scegliere qualsiasi indirizzo IP di origine o destinazione, questa funzionalità consente agli amministratori di diagnosticare rapidamente i problemi di connettività da o toohello internet e da o toohello nell'ambiente locale.

La verifica del flusso IP esamina l'interfaccia di rete di una macchina virtuale. Il flusso del traffico viene quindi verificata in base a tooor impostazioni hello configurato dall'interfaccia di rete. Questa funzionalità è utile per confermare se una regola in un gruppo di sicurezza di rete sta bloccando tooor di traffico in ingresso o in uscita da una macchina virtuale.

#### <a name="next-hop"></a>Hop successivo

Determina hello [hop successivo](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) per i pacchetti indirizzati in hello dell'infrastruttura di rete di Azure, abilitazione qualsiasi toodiagnose è configurato correttamente le route definite dall'utente. Il traffico proveniente da una macchina virtuale viene inviato a destinazione tooa in base a route valide di hello associate a una scheda di rete. Hop successivo Ottiene il tipo dell'hop successivo di hello e l'indirizzo IP di un pacchetto da una macchina virtuale specifica e una scheda di rete. In questo modo toodetermine se hello pacchetto è in corso destinazione toohello diretti o è holed traffico hello in nero.

Hop successivo restituisce anche tabella di route hello associata all'hop successivo hello. Quando si eseguono query hop successivo itinerario hello è definito come una route definita dall'utente, verrà restituito tale route. In caso contrario l'hop successivo restituisce la route di sistema.

#### <a name="security-group-view"></a>Visualizzazione dei gruppi di sicurezza

Ottiene le regole di sicurezza efficace e applicato hello che vengono applicate in una macchina virtuale. I gruppi di sicurezza di rete sono associati a un livello di subnet o a un livello di scheda di interfaccia di rete. Quando associato a un livello di subnet, si applica le istanze VM hello tooall nella subnet hello. Rete [visualizzazione del gruppo di sicurezza](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) restituisce tutti i NSGs hello configurato e regole che sono associate a un livello di interfaccia di rete e subnet per una macchina virtuale per fornire informazioni sulle configurazione hello. Inoltre, le regole di sicurezza efficace hello vengono restituite per ognuna delle schede NIC hello in una macchina virtuale. Usando la visualizzazione dei gruppi di sicurezza di rete, è possibile valutare le vulnerabilità di rete di una VM, ad esempio le porte aperte. È anche possibile verificare se il gruppo di sicurezza di rete funzioni come previsto in base a un [confronto tra hello configurato e regole di sicurezza efficace hello](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Registrazione dei flussi dei gruppi di sicurezza di rete

 Registri di flusso per gruppi di sicurezza di rete consentono toocapture registri tootraffic correlati che vengono concesse o negate le regole di sicurezza hello gruppo hello. flusso di Hello è definito dalle informazioni tupla con 5: indirizzo IP di origine, IP di destinazione, porta di origine, destinazione porta e protocollo.

[I registri del flusso di gruppo di sicurezza di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Risoluzione dei problemi di connessione e del gateway di rete virtuale

Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure. Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse. La funzionalità di [risoluzione dei problemi delle risorse](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) può essere chiamata da PowerShell, dall'interfaccia della riga di comando o dall'API REST. Quando viene chiamato, Watcher di rete Controlla integrità hello di un gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.

Questa sezione vengono fornite indicazioni hello diverse operazioni di gestione che sono attualmente disponibili per la risoluzione dei problemi di risorse.

-   [Risolvere i problemi relativi a un gateway di rete virtuale](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Risolvere i problemi relativi a una connessione](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Limite sottoscrizioni di rete

[Limiti della sottoscrizione di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) forniti i dettagli di utilizzo di hello di ogni risorsa di rete hello in una sottoscrizione in un'area con il numero massimo di hello delle risorse disponibili.

#### <a name="configuring-diagnostics-log"></a>Configurazione dei log di diagnostica

Network Watcher offre una visualizzazione dei [log di diagnostica](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview). contenente tutte le risorse di rete che supportano la registrazione diagnostica. Da questa visualizzazione è possibile abilitare e disabilitare le risorse di rete in modo facile e veloce.

### <a name="network-resource-level-monitoring"></a>Monitoraggio a livello di risorsa di rete

Hello seguenti caratteristiche sono disponibile per il monitoraggio a livello di risorse:

#### <a name="audit-log"></a>Log di controllo

Vengono registrate le operazioni eseguite come parte della configurazione di hello delle reti. Questi log di controllo sono essenziali tooestablish le conformità diversi. Questi registri possono essere visualizzati nel portale di Azure hello o recuperati utilizzando strumenti quali Power BI o gli strumenti di terze parti. I log di controllo sono disponibili tramite il portale di hello, PowerShell, CLI e API Rest.

> [!Note]
> Per altre informazioni sui log di controllo, vedere [Operazioni di controllo con Gestione risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
I log di controllo sono disponibili per le operazioni eseguite su tutte le risorse di rete.


#### <a name="metrics"></a>Metriche

Le metriche sono costituite da contatori e misurazioni delle prestazioni raccolti in un determinato periodo di tempo. Attualmente le metriche sono disponibili per il gateway applicazione. Metrica può essere utilizzato tootrigger avvisi in base alla soglia. Gateway applicazione Azure per impostazione predefinita Controlla integrità hello di tutte le risorse nel relativo pool back-end e rimuove automaticamente qualsiasi risorsa considerato non integro dal pool hello. Gateway applicazione continua a istanze di tipo non integro hello toomonitor e li aggiunge eseguire il pool back-end integro toohello quando diventano disponibili e rispondono toohealth probe. Gateway applicazione invia hello probe di integrità con hello è definita nelle impostazioni HTTP back-end di hello stessa porta. Questa configurazione assicura che probe hello è test hello stessa porta che i clienti utilizzassero back-end toohello tooconnect.

> [!Note]
> Vedere [diagnostica del Gateway applicazione](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview come metrica può essere utilizzato toocreate avvisi.

#### <a name="diagnostic-logs"></a>Log di diagnostica

Eventi periodici e spontanei vengono creati dalle risorse di rete e registrati negli account di archiviazione, inviate tooan Hub eventi o Analitica di Log. Questi log forniscono informazioni dettagliate sui integrità hello di una risorsa. e possono essere visualizzati con strumenti quali Power BI e Log Analytics. come i log di diagnostica tooview, visitare toolearn [Analitica Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Sono disponibili log di diagnostica per il [servizio di bilanciamento del carico](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), i [gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), le route e il [gateway applicazione](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher offre una visualizzazione dei log di diagnostica contenente tutte le risorse di rete che supportano la registrazione diagnostica. Da questa visualizzazione è possibile abilitare e disabilitare le risorse di rete in modo facile e veloce.

### <a name="log-analytics"></a>Log Analytics

[Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) è un servizio in [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) che monitora il toomaintain ambienti cloud e locali loro disponibilità e prestazioni. Vengono raccolti i dati generati dalle risorse negli ambienti di cloud e locali e da altre analisi di tooprovide strumenti monitoraggio in più origini.

Log Analitica offre hello seguenti soluzioni per il monitoraggio delle reti:

-   Monitoraggio delle prestazioni di rete

-   Analisi gateway applicazione di Azure

-   Analisi gruppo di sicurezza di rete di Azure

#### <a name="network-performance-monitor-npm"></a>Monitoraggio prestazioni rete (NPM)
Hello [Network Performance Monitor](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) soluzione di gestione è una soluzione che consente di monitorare hello integrità, disponibilità e raggiungibilità di reti di monitoraggio di rete.

È utilizzato toomonitor connettività tra:

-   cloud pubblico e risorse locali

-   data center e percorsi utente (filiali)

-   subnet che ospita i diversi livelli di un'applicazione a più livelli.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Analisi gateway applicazione di Azure in Log Analytics

Hello seguendo i registri è supportato per i gateway applicazione:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Hello seguenti metriche è supportato per i gateway applicazione:

-   Velocità effettiva in cinque minuti

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Analisi gruppo di sicurezza di rete di Azure in Log Analytics

Hello log seguenti sono supportati per [gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** contiene voci per il gruppo le regole sono applicate tooVMs e i ruoli di istanza in base all'indirizzo MAC. lo stato di Hello per queste regole verrà raccolti ogni 60 secondi.

- **NetworkSecurityGroupRuleCounter:** contiene voci per quante volte ogni gruppo di regole viene applicata toodeny o consentire il traffico.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulla sicurezza, vedere alcuni degli approfondimenti sull'argomento:

-   [Log Analytics per i gruppi di sicurezza di rete (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Tale interruzione cloud hello di unità di rete innovazioni](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [: SONiC hello software commutatore che alimenta hello Microsoft Cloud globali di rete](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [How Microsoft builds its fast and reliable global network (Informazioni sul modo in cui Microsoft crea una rete globale veloce e affidabile)](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Lighting up network innovation (Realizzare l'innovazione della rete)](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
