---
title: rete aaaAzure | Documenti Microsoft
description: "Informazioni sulle funzionalità e i servizi di rete di Azure."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Rete di Azure

Azure offre un'ampia gamma di funzionalità di rete che possono essere usate insieme o separatamente. Fare clic su una delle seguenti funzionalità principali toolearn altre relative informazioni hello:
- [La connettività tra le risorse di Azure](#connectivity): le risorse di Azure di connettersi contemporaneamente in una rete virtuale privata protetta nel cloud hello.
- [Connettività Internet](#internet-connectivity): comunicare tooand dalle risorse di Azure tramite Internet hello.
- [Connettività locale](#on-premises-connectivity): connettersi a un risorse tooAzure di rete locale tramite una rete privata virtuale (VPN) tramite Internet hello o tooAzure una connessione dedicata.
- [Direzione del traffico e di bilanciamento del carico](#load-balancing): tooservers traffico bilanciamento di carico in hello nello stesso percorso e il traffico diretto tooservers in posizioni diverse.
- [Sicurezza](#security): permette di filtrare il traffico di rete tra le subnet della rete o le singole macchine virtuali (VM).
- [Routing](#routing): consente l'uso del routing predefinito o il controllo completo del routing tra le risorse di Azure e quelle locali.
- [Gestibilità](#manageability): permette di monitorare e gestire le risorse di rete di Azure.
- [Strumenti di configurazione e distribuzione](#tools): usare un portale basato sul web o gli strumenti da riga di comando multipiattaforma toodeploy e configurare le risorse di rete.

## <a name="Connectivity"></a>Connettività tra risorse di Azure

Le risorse di Azure, quali ad esempio Macchine virtuali, Servizi cloud, i set di scalabilità di macchine virtuali e gli ambienti del servizio app di Azure possono comunicare tra loro in privato tramite una rete virtuale di Azure. Una rete virtuale è un isolamento logico di hello cloud di Azure dedicato tooyour [sottoscrizione](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). È possibile implementare più reti virtuali in ogni sottoscrizione e [area](https://azure.microsoft.com/regions) di Azure. Ogni rete virtuale è isolata dalle altre. Per ogni rete virtuale è possibile:

- Specificare uno spazio indirizzi IP privato personalizzato con indirizzi pubblici e privati (RFC 1918). Azure Assegna risorse connesso toohello rete virtuale un indirizzo IP privato da assegnare spazio di indirizzi di hello.
- Segmento hello rete virtuale in uno o più subnet e allocare una parte della subnet di tooeach spazio di indirizzi di hello rete virtuale.
- Utilizzare la risoluzione dei nomi fornita da Azure oppure specificare che server DNS per l'utilizzo da risorse connesso tooa rete virtuale.

ulteriori informazioni sul servizio di rete virtuale di Azure hello, leggere hello toolearn [Panoramica di rete virtuale](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo. È possibile connettere reti virtuali tooeach altri, l'abilitazione di risorse collegato tooeither toocommunicate di rete virtuale tra loro attraverso reti virtuali. È possibile utilizzare uno o entrambi hello opzioni tooconnect reti virtuali tooeach altri seguenti:

- **Peering:** risorse Abilita connesso toodifferent reti virtuali di Azure all'interno di hello stessa regione di Azure toocommunicate tra loro. Hello larghezza di banda e latenza tra reti virtuali sono hello hello stesso come se le risorse di hello erano connesso toohello stessa rete virtuale. toolearn ulteriori informazioni su peering, leggere hello [Panoramica peer della rete virtuale](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Gateway VPN:** risorse Abilita connesso toodifferent reti virtuali di Azure in diverse aree di Azure toocommunicate tra loro. Il traffico tra le reti virtuali passa attraverso un gateway VPN di Azure. Larghezza di banda tra reti virtuali è limitato toohello della larghezza di banda del gateway hello. ulteriori informazioni sulla connessione di reti virtuali con un Gateway VPN, leggere hello toolearn [configurare una connessione di rete virtuale a in aree geografiche](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

## <a name="internet-connectivity"></a>Connettività Internet

Tutte le risorse di Azure connessa tooa rete virtuale dispone di connettività in uscita toohello Internet per impostazione predefinita. indirizzo IP privato Hello della risorsa hello è l'indirizzo di rete di origine convertito (SNAT) tooa indirizzo IP da hello dell'infrastruttura di Azure. ulteriori informazioni sulla connettività Internet in uscita, leggere hello toolearn [informazioni sulle connessioni in uscita in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

toocommunicate in ingresso risorse tooAzure hello Internet o toocommunicate toohello in uscita deve essere assegnato un indirizzo IP pubblico a Internet senza SNAT, una risorsa. informazioni su indirizzi IP pubblici, leggere hello toolearn [gli indirizzi IP pubblici](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

## <a name="on-premises-connectivity"></a>Connettività locale

È possibile accedere in modo sicuro alle risorse in una rete virtuale tramite una connessione VPN o una connessione diretta privata. toosend il traffico di rete tra la rete virtuale di Azure e la rete locale, è necessario creare un gateway di rete virtuale. Configurare le impostazioni per hello gateway toocreate hello il tipo di connessione che si desidera, VPN o ExpressRoute.

È possibile connettere il tooa di rete locale virtuale usando qualsiasi combinazione di hello le opzioni seguenti:

**Da punto a sito (VPN su SSTP)**

Hello seguente immagine Mostra toosite punto separate le connessioni tra più computer e una rete virtuale:

![Da punto a sito](./media/networking-overview/point-to-site.png)

Questa connessione viene stabilita tra un singolo computer e una rete virtuale. Questo tipo di connessione è molto utile se principianti con Azure o per gli sviluppatori, perché richiede senza modifiche tooyour una rete esistente. Risulta utile anche quando ci si connette da una posizione remota, ad esempio da casa o durante una conferenza. Le connessioni Point-to-site sono spesso associate a una connessione site-to-site tramite hello stesso gateway di rete virtuale. connessione Hello Usa la comunicazione di tooprovide crittografato hello SSTP protocollo su hello Internet tra computer hello e hello rete virtuale. latenza Hello per una VPN point-to-site è imprevedibile, poiché il traffico di hello attraversa hello Internet.

**Da sito a sito (tunnel VPN IPsec/IKE)**

![Da sito a sito](./media/networking-overview/site-to-site.png)

Questa connessione viene stabilita tra il dispositivo VPN locale e un gateway VPN di Azure. Questo tipo di connessione consente a qualsiasi risorsa locale autorizzare hello tooaccess rete virtuale. connessione di Hello è una VPN IPSec/IKE che fornisce comunicazioni crittografate tramite hello Internet tra il dispositivo locale e il gateway VPN di Azure hello. È possibile connettere più locale siti toohello stesso gateway VPN. Hello in locale il dispositivo VPN in ogni sito deve avere un indirizzo IP esterno pubblico che non è dietro un NAT. latenza Hello per una connessione site-to-site è imprevedibile, poiché il traffico di hello attraversa hello Internet.

**ExpressRoute (connessione privata dedicata)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Questo tipo di connessione viene stabilito tra la rete e Azure tramite un partner ExpressRoute. La connessione è privata. Il traffico non attraversa hello Internet. latenza Hello per una connessione ExpressRoute è prevedibile, poiché il traffico non deve attraversare hello Internet. È possibile combinare ExpressRoute con una connessione da sito a sito.

informazioni su tutte le hello connessione opzioni precedenti, leggere hello toolearn [diagrammi della topologia di connessione](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

## <a name="load-balancing"></a>Bilanciamento del carico e indirizzamento del traffico

Microsoft Azure offre numerosi servizi che consentono di gestire la distribuzione del traffico e il bilanciamento del carico. È possibile utilizzare una delle seguenti funzionalità separatamente o congiuntamente hello:

**Bilanciamento del carico DNS**

Hello del servizio di gestione traffico di Azure fornisce il bilanciamento del carico DNS globale. Gestione traffico risponde tooclients con indirizzo IP hello un endpoint integro, basato su uno dei seguenti metodi di routing hello:
- **Geografico:** i client vengono indirizzati gli endpoint toospecific (Azure, esterna o annidata) in base quale posizione geografica, le query DNS ha origine da. Questo metodo consente l'uso di scenari in cui è importante conoscere l'area geografica di un client e indirizzarlo in base a tale informazione. Ne sono esempi la conformità a requisiti di sovranità dei dati, la localizzazione del contenuto e dell'esperienza utente e la misurazione del traffico da aree diverse.
- **Prestazioni:** indirizzo IP hello restituito toohello client diventa hello "più vicino" toohello. endpoint di Hello 'vicino' non è necessariamente più vicino in termini di distanza geografica. Al contrario, questo metodo determina endpoint più vicino hello misurazione della latenza di rete. Gestione traffico mantiene un Internet latenza tabella tootrack hello tempo di round trip tra intervalli di indirizzi IP e ogni Data Center di Azure.
- **Priorità:** traffico è indirizzato toohello primario (più alta priorità) endpoint. Se l'endpoint primario hello non è disponibile, le route di Traffic Manager hello endpoint secondo toohello di traffico. Se entrambi gli endpoint primario e secondario hello non sono disponibili, hello del traffico toohello terzo, e così via. Disponibilità di endpoint hello è in base allo stato di hello configurato (abilitato o disabilitato) e hello monitoraggio degli endpoint in corso.
- **Round robin ponderato:** per ogni richiesta, Gestione traffico sceglie in modo casuale un endpoint disponibile, probabilità di Hello della scelta di un endpoint si basa su un peso hello endpoint disponibili tooall. Utilizzando hello stesso peso tra tutti i risultati in una distribuzione del traffico anche gli endpoint. L'utilizzo di pesi superiori o inferiori in endpoint specifici provoca toobe tali endpoint ha restituito più o meno frequente nelle risposte DNS hello.

Hello seguente immagine mostra una richiesta per un tooa applicazione indirizzate web endpoint di App Web. Gli endpoint possono anche essere altri servizi di Azure, ad esempio Macchine virtuali o Servizi cloud.

![Gestione traffico](./media/networking-overview/traffic-manager.png)

client di Hello si connette direttamente toothat endpoint. Gestione traffico di Azure rileva se un endpoint non è integro e viene quindi reindirizzata endpoint diversi, integro tooa di client. ulteriori informazioni su gestione traffico, leggere hello toolearn [Panoramica di gestione traffico di Azure](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

**Bilanciamento del carico dell'applicazione**

Hello servizio Gateway di applicazione di Azure fornisce il controller di recapito dell'applicazione (ADC) come servizio. Gateway applicazione offre varie livello 7 (HTTP/HTTPS) bilanciamento del carico funzionalità per le applicazioni, ad esempio un'applicazione web del firewall tooprotect le applicazioni web da attacchi e vulnerabilità. Gateway applicazione consente inoltre la produttività di toooptimize web farm tramite l'offload di gateway applicazione toohello di terminazione SSL con utilizzo intensivo della CPU. 

Altre funzionalità di routing di livello 7 includono la distribuzione round-robin del traffico in ingresso, l'affinità di sessione basato su cookie, il routing basato sul percorso URL e hello possibilità toohost più siti Web protetti da un gateway singola applicazione. Il gateway applicazione può essere configurato come gateway con connessione Internet, come gateway solo interno o come una combinazione di queste due opzioni. È completamente gestito in Azure e offre scalabilità e disponibilità elevata, oltre a un set completo di funzionalità di registrazione e diagnostica che ne migliorano la gestibilità. altre informazioni sull'applicazione Gateway, leggere hello toolearn [Panoramica di Gateway applicazione](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

Hello nella figura seguente mostra URL con Gateway applicazione il routing basato sul percorso:

![gateway applicazione](./media/networking-overview/application-gateway.png)

**Bilanciamento carico di rete**

Hello bilanciamento del carico di Azure offre prestazioni elevate, bassa latenza livello 4 con bilanciamento del carico per tutti i protocolli TCP e UDP. Gestisce le connessioni in ingresso e in uscita. È possibile configurare endpoint con carico bilanciato pubblici e interni È possibile definire regole toomap in ingresso di destinazioni di pool di connessioni tooback-end utilizzando HTTP e TCP probe di integrità opzioni toomanage la disponibilità del servizio. informazioni sul bilanciamento del carico, leggere hello toolearn [Panoramica di bilanciamento del carico](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

Hello seguente immagine illustra un'applicazione multilivello con connessione Internet che usa entrambi servizi di bilanciamento del carico interni ed esterni:

![Bilanciamento del carico](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Sicurezza

È possibile filtrare il traffico tooand da risorse di Azure con hello le opzioni seguenti:

- **Rete:** è possibile implementare una rete di Azure toofilter gruppi di sicurezza in ingresso e in uscita traffico tooAzure risorse. Ogni gruppo di sicurezza di rete contiene una o più regole in ingresso e in uscita. Ogni regola specifica gli indirizzi IP di origine hello, indirizzi IP di destinazione, porta e protocollo che il traffico è filtrato con. NSGs può essere applicato tooindividual subnet e singole macchine virtuali. ulteriori informazioni sulla NSGs, leggere hello toolearn [Panoramica di gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Applicazione:** usando un gateway applicazione con un Web application firewall è possibile proteggere le applicazioni Web da vulnerabilità ed exploit, ad esempio attacchi SQL injection, cross-site scripting e intestazioni non valide. Il gateway applicazione filtra questo tipo di traffico e gli impedisce di raggiungere i server Web. Si è in grado di tooconfigure regole che si desidera attivare. criteri di negoziazione SSL tooconfigure possibilità Hello viene fornito tooallow determinati criteri toobe disabilitato. informazioni sui firewall applicazione web di hello, leggere hello toolearn [firewall applicazione Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

Se è necessaria la funzionalità di rete Azure non fornire o che le applicazioni di rete toouse utilizzare locale, è possibile implementare prodotti hello in macchine virtuali e connetterli tooyour rete virtuale. Hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) contiene numerose e diverse macchine virtuali preconfigurate con applicazioni di rete è attualmente in uso. Queste macchine virtuali preconfigurate sono in genere indicati tooas virtuale ai dispositivi di rete (NVA). e sono disponibili con applicazioni quali firewall e ottimizzazione WAN.

## <a name="routing"></a>Routing

Azure Crea impostazione predefinita le tabelle di route che consentono le risorse subnet tooany connesso toocommunicate qualsiasi rete virtuale tra loro. È possibile implementare uno o entrambi i seguenti tipi di route toooverride hello hello Azure crea route di predefinite:
- **Definite dall'utente:** è possibile creare tabelle di routing personalizzata con le route che controllano in cui il traffico viene indirizzato toofor ogni subnet. altre informazioni sulle route definite dall'utente, leggere hello toolearn [le route definite dall'utente](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **(BGP) Border gateway protocol:** se ci si connette la rete locale tooyour di rete virtuale utilizzando una connessione Gateway VPN di Azure o ExpressRoute, è possibile propagare tooyour delle route BGP reti virtuali. BGP è hello protocollo di routing standard comunemente utilizzato nelle hello Internet tooexchange routing e raggiungibilità informazioni tra due o più reti. Quando usata nel contesto di hello di reti virtuali di Azure, hello Abilita BGP gateway VPN di Azure e i dispositivi VPN locali, peer BGP chiamato o elementi adiacenti, tooexchange "indirizza" che indicano entrambi i gateway disponibilità hello e della raggiungibilità di tali prefissi toogo tramite gateway hello o router coinvolti. BGP inoltre è possibile abilitare il routing di transito tra più reti mediante propagazione di route, un gateway BGP apprende da uno tooall peer BGP altri peer BGP. toolearn ulteriori informazioni su BGP, vedere hello [BGP Panoramica gateway VPN di Azure](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

## <a name="manageability"></a>Gestibilità

Azure offre i seguenti hello toomonitor degli strumenti e gestire la rete:
- **Log attività:** risorse di Azure tutti dispongono di log di attività che forniscono informazioni sulle operazioni eseguite posizionare, lo stato delle operazioni e chi ha avviato l'operazione di hello. ulteriori informazioni sui registri di attività, leggere hello toolearn [attività registra Panoramica](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **I log di diagnostica:** periodico e spontanei eventi vengono creati dalle risorse di rete e registrati negli account di archiviazione di Azure, inviati tooan Hub di eventi di Azure o inviati tooAzure Log Analitica. I log di diagnostica forniscono integrità toohello visione di una risorsa. Sono disponibili log di diagnostica per Azure Load Balancer, gruppi di sicurezza di rete, route e gateway applicazione. ulteriori informazioni sui registri di diagnostica, leggere hello toolearn [Panoramica del log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Metriche:** le metriche sono costituite da contatori e misurazioni delle prestazioni raccolti in un determinato periodo di tempo sulle risorse. Metrica può essere utilizzato tootrigger avvisi in base a soglie. Attualmente le metriche sono disponibili nel gateway applicazione. ulteriori informazioni sulle metriche, leggere hello toolearn [Cenni preliminari sulle metriche](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Risoluzione dei problemi:** informazioni di risoluzione dei problemi è accessibile direttamente nel portale di Azure hello. informazioni di Hello consentono di diagnosticare i problemi comuni con ExpressRoute, Gateway VPN, Gateway applicazione, i log di sicurezza di rete, route, DNS, bilanciamento del carico e gestione traffico.
- **Controllo degli accessi in base al ruolo:** il controllo degli accessi in base al ruolo permette di controllare chi può creare e gestire le risorse di rete. Altre informazioni su RBAC leggendo hello [introduzione RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo. 
- **Acquisizione di pacchetti:** hello Azure Watcher di rete servizio fornisce hello toorun possibilità di acquisizione in una macchina virtuale tramite un'estensione hello VM all'interno di un pacchetto. Questa funzionalità è disponibile per macchine virtuali Windows e Linux. altre informazioni sull'acquisizione di pacchetti, leggere hello toolearn [Panoramica acquisizione pacchetto](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Verificare i flussi di IP:** Watcher di rete consente tooverify IP flussi tra una macchina virtuale di Azure e toodetermine una risorsa remota se i pacchetti sono concesse o negati. Questa funzionalità consente agli amministratori hello tooquickly diagnosticare problemi di connettività. toolearn ulteriori informazioni su come tooverify IP flussi, lettura hello [flusso IP verificare Panoramica](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Risoluzione dei problemi di connettività VPN:** hello funzionalità VPN di risoluzione dei problemi di controllo di rete fornisce hello possibilità tooquery una connessione o il gateway e verificare hello integrità delle risorse di hello. ulteriori informazioni sulla risoluzione dei problemi relativi a connessioni VPN, leggere hello toolearn [connettività VPN risoluzione dei problemi di panoramica](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Visualizzare la topologia della rete:** visualizzare una rappresentazione grafica hello di risorse di rete in una rete virtuale con Watcher di rete. ulteriori informazioni sulla visualizzazione di topologia di rete, leggere hello toolearn [Panoramica della topologia](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.

## <a name="tools"></a>Strumenti di distribuzione e configurazione

È possibile distribuire e configurare le risorse di rete Azure con i seguenti strumenti hello:

- **Portale di Azure:** interfaccia utente grafica che viene eseguita in un browser. Aprire hello [portale di Azure](http://portal.azure.com).
- **Azure PowerShell:** strumenti da riga di comando per la gestione di Azure da computer Windows. Per ulteriori informazioni su Azure PowerShell, la lettura hello [Panoramica di Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Interfaccia della riga di comando di Azure:** strumenti da riga di comando per la gestione di Azure da computer Linux, macOS o Windows. Altre informazioni su hello CLI di Azure per la lettura hello [Panoramica CLI di Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- **Modelli di gestione risorse di Azure:** un file (in formato JSON) che definisce l'infrastruttura di hello e la configurazione di una soluzione di Azure. Usando il modello è possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente. ulteriori informazioni sulla creazione di modelli, leggere hello toolearn [procedure consigliate per la creazione di modelli](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo. Modelli possono essere distribuiti con il portale di Azure, hello CLI o PowerShell. tooget adesso con i modelli, distribuire uno dei hello molti modelli preconfigurati in hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/?term=network) libreria. 

## <a name="pricing"></a>Prezzi

Alcune di hello Azure servizi di rete hanno un addebito, mentre altri sono gratuiti. Hello vista [rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network), [Gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [Gateway applicazione](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [bilanciamento del carico](https://azure.microsoft.com/pricing/details/load-balancer), [Watcherdirete](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) e [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) prezzi pagine per altre informazioni.

## <a name="next-steps"></a>Passaggi successivi

- Creare una rete virtuale di prima e connettersi qualche tooit di macchine virtuali, completando i passaggi hello hello [creare la prima rete virtuale](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- Connettere la rete virtuale di tooa computer completando i passaggi hello hello [configurare una connessione point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
- I server toopublic il traffico Internet il bilanciamento del carico completando i passaggi hello hello [creare un servizio di bilanciamento del carico con connessione Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) articolo.
