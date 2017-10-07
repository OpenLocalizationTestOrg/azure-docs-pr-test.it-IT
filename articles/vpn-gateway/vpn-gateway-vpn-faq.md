---
title: domande frequenti su Gateway VPN aaaAzure | Documenti Microsoft
description: domande frequenti su Gateway VPN Hello. Domande frequenti relative alle connessioni cross-premise di Rete virtuale di Microsoft Azure, alle connessioni con configurazioni ibride e ai gateway VPN.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>Domande frequenti sul gateway VPN

## <a name="connecting"></a>La connessione di reti toovirtual

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>È possibile connettere reti virtuali in diverse aree di Azure?

Sì. Non esistono vincoli di area. Una rete virtuale può connettersi tooanother rete virtuale in hello stessa area, o in un'area diversa di Azure. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>È possibile connettere reti virtuali in diverse sottoscrizioni?

Sì.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>È possibile collegare siti toomultiple da una singola rete virtuale?

È possibile connettersi toomultiple siti tramite Windows PowerShell e hello API REST di Azure. Vedere hello [multisito e la connettività di rete virtuale a](#V2VMulti) sezione Domande frequenti.

### <a name="what-are-my-cross-premises-connection-options"></a>Quali sono le opzioni di connessione cross-premise?

Hello seguente cross-premise le connessioni sono supportate:

* Da sito a sito: connessione VPN tramite IPsec (IKE v1 e IKE v2). Per questo tipo di connessione è necessario un dispositivo VPN o RRAS. Per altre informazioni, vedere [Da sito a sito](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Da punto a sito: connessione VPN tramite SSTP (Secure Sockets Tunneling Protocol). Questa connessione non richiede un dispositivo VPN. Per altre informazioni, vedere [Da punto a sito](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Da-rete: questo tipo di connessione è hello uguale a una configurazione da sito a sito. Rete virtuale tooVNet è una connessione VPN tramite IPsec (IKE v1 e IKE v2). Non richiede un dispositivo VPN. Per altre informazioni, vedere [Da rete virtuale a rete virtuale](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Multi-sito-si tratta di una variante di una configurazione da sito a sito che consente di tooconnect più siti tooa virtuale rete locale. Per altre informazioni, vedere [Multisito](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute-ExpressRoute è tooAzure una connessione diretta dalla rate WAN, non una connessione VPN tramite hello rete Internet pubblica. Per ulteriori informazioni, vedere hello [Panoramica tecnica su ExpressRoute](../expressroute/expressroute-introduction.md) hello e [domande frequenti su ExpressRoute](../expressroute/expressroute-faqs.md).

Per altre informazioni sulle connessioni del gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Qual è la differenza hello tra una connessione Site-to-Site e da punto a sito?

Le configurazioni **da sito a sito** (tunnel VPN IPsec/IKE) connettono il percorso locale ad Azure. Ciò significa che è possibile connettersi da tutti i computer che si trova sul macchina virtuale di tooany locale o istanza del ruolo all'interno della rete virtuale, a seconda della tooconfigure routing e le autorizzazioni. Questa opzione è ottimale per una connessione cross-premise sempre disponibile ed è adatta per le configurazioni ibride. Questo tipo di connessione si basa su un dispositivo VPN IPsec (dispositivo hardware o software accessorio), che deve essere distribuito al confine hello della rete. toocreate questo tipo di connessione, è necessario un indirizzo IPv4 accessibile pubblicamente che non è dietro un NAT.

**Point-to-Site** configurazioni (VPN tramite SSTP) consentono di connettersi da un singolo computer ovunque tooanything situati nella rete virtuale. Utilizza i client VPN incorporato di Windows hello. Come parte della configurazione hello Point-to-Site, installare un certificato e un pacchetto di configurazione client VPN, che contiene le impostazioni di hello che consentono la macchina virtuale tooany tooconnect di computer o istanza del ruolo all'interno di rete virtuale hello. È molto utile quando si desidera che sulla rete virtuale di tooconnect tooa, ma non in locale. È anche un'ottima scelta se non si dispone di accesso tooVPN hardware o un indirizzo IPv4 accessibile pubblicamente, entrambi i quali sono necessari per una connessione Site-to-Site.

È possibile configurare la rete virtuale di toouse entrambi Site-to-Site e digitare Point-to-Site contemporaneamente, purché la creazione della connessione da sito a sito tramite una rete VPN basata su route per il gateway. Tipi di VPN basate su route vengono chiamati gateway dinamico in modello di distribuzione classica hello.

## <a name="gateways"></a>Gateway di rete virtuale

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Un gateway VPN corrisponde a un gateway di rete virtuale?

Un gateway VPN è un tipo di gateway di rete virtuale, che invia traffico crittografato tra la rete virtuale e la posizione locale tramite una connessione pubblica. È inoltre possibile utilizzare un traffico di toosend VPN gateway tra reti virtuali. Quando si crea un gateway VPN, utilizzare il valore di - il tipo di gateway hello 'Vpn'. Per altre informazioni, [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>Cos'è un gateway basato su criteri (con routing statico)?

I gateway basati su criteri implementano VPN basate su criteri. Le VPN basate su criteri di crittografano e indirizzano i pacchetti attraverso i tunnel IPsec in base alle combinazioni di hello di prefissi di indirizzo tra la rete locale e hello rete virtuale di Azure. criteri Hello (o il selettore di traffico) viene in genere definito come un elenco di accesso nella configurazione VPN hello.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Cos'è un gateway basato su route (con routing dinamico)?

Implementare i gateway basato su route hello VPN basate su route. Le VPN basate su route utilizzano "routing" hello IP inoltro o il routing di pacchetti toodirect tabella nelle interfacce tunnel corrispondenti. interfacce di tunnel Hello quindi crittografare o decrittografare i pacchetti hello da e verso i tunnel hello. Hello selettore criteri o di traffico per le VPN basate su route sono configurate come any-to-any (o i caratteri jolly).

### <a name="do-i-need-a-gatewaysubnet"></a>Il valore 'GatewaySubnet' è necessario?

Sì. subnet del gateway Hello contiene indirizzi IP hello che utilizzano servizi gateway di rete virtuale hello. È necessario toocreate una subnet del gateway per la rete virtuale in ordine tooconfigure un gateway di rete virtuale. Tutte le subnet gateway devono essere denominate 'GatewaySubnet' toowork correttamente. Non assegnare un nome diverso alla subnet del gateway. E non distribuire macchine virtuali o qualsiasi altra operazione toohello subnet del gateway.

Quando si crea una subnet del gateway hello, specificare il numero di indirizzi IP che hello subnet hello contiene. gli indirizzi IP Hello nella subnet del gateway hello vengono allocati toohello il servizio gateway. Alcune configurazioni richiedono ulteriori toobe di indirizzi IP allocati toohello Servizi gateway rispetto ad altri utenti. Si desidera che la subnet gateway contenga sufficiente crescita futura tooaccommodate di indirizzi IP e i possibili configurazioni di connessione aggiuntive nuovo toomake. Anche se è possibile creare una subnet del gateway con dimensioni pari a /29, è consigliabile crearne una con dimensioni pari a /27 o superiori, ad esempio /27, /26, /25 e così via. Esaminare i requisiti di hello per configurazione hello toocreate desiderato e verificare che la subnet gateway hello che è verrà soddisfare tali requisiti.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>È possibile distribuire macchine virtuali o subnet del gateway toomy istanze ruolo?

No.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>È possibile ottenere l'indirizzo IP del gateway VPN prima di crearlo?

No. Hai toocreate il primo tooget hello indirizzo IP del gateway. Hello modifiche all'indirizzo IP se si elimina e ricrea il gateway VPN.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>È possibile richiedere un indirizzo IP pubblico statico per il gateway VPN?

No. È supportata solo l'assegnazione di indirizzi IP dinamici. Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour. tempo di Hello solo modifiche all'indirizzo IP gateway VPN hello quando è hello gateway viene eliminato e ricreato. indirizzo IP pubblico del gateway VPN Hello non cambia tra il ridimensionamento, reimpostare o altri interni/aggiornamenti del gateway VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>Come si ottiene l'autenticazione del tunnel VPN?

Il tunnel VPN di Azure usa chiavi precondivise (PSK) per l'autenticazione. Si genera una chiave già condivisa (PSK) quando si crea tunnel VPN hello. È possibile modificare hello autogenerati PSK tooyour con i cmdlet di PowerShell di chiave precondivisa impostare hello o l'API REST.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>È possibile usare hello API di impostazione della chiave precondivisa tooconfigure my basata su criteri (routing statico) gateway VPN?

Sì, hello API di impostazione della chiave precondivisa e PowerShell cmdlet può essere utilizzato tooconfigure Azure VPN (statica) basata su criteri sia basato su route () VPN con routing dinamico.

### <a name="can-i-use-other-authentication-options"></a>È possibile usare altre opzioni di autenticazione?

Ci sono chiavi già condivise toousing limitato (PSK) per l'autenticazione.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Come è possibile specificare che il traffico viene indirizzato tramite gateway VPN hello?

#### <a name="resource-manager-deployment-model"></a>Modello di distribuzione di Gestione risorse

* PowerShell: utilizzare "AddressPrefix" toospecify traffico per il gateway di rete locale hello.
* Portale di Azure: passare il gateway di rete locale toohello > Configurazione > dello spazio di indirizzi.

#### <a name="classic-deployment-model"></a>Modello di distribuzione classica

* Portale di Azure: passare a rete virtuale classica toohello > le connessioni VPN > le connessioni VPN da sito a sito > nome sito locale > sito locale > spazio degli indirizzi Client. 
* Portale classico: aggiungere tutti gli intervalli che si desidera inviare tramite il gateway hello per la rete virtuale nella pagina reti hello in reti locali. 

### <a name="can-i-configure-forced-tunneling"></a>È possibile configurare il tunneling forzato?

Sì. Vedere [Configurare il tunneling forzato](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>È possibile configurare il server VPN in Azure e usarlo come rete di tooconnect toomy locale?

Sì, è possibile distribuire un server in Azure da hello Azure Marketplace o creare propri router VPN o personali gateway VPN. È necessario route definite dall'utente tooconfigure nella rete virtuale tooensure traffico viene indirizzato correttamente tra le reti locali e le subnet della rete virtuale.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Perché determinate porte sono aperte nella mia gateway VPN?

Sono necessarie per la comunicazione di infrastruttura di Azure. Sono protette (bloccate) dai certificati di Azure. Senza il certificato corretto, le entità esterne, inclusi i clienti di hello tali gateway, non sarà in grado di toocause qualsiasi effetto su tali endpoint.

Un gateway VPN è fondamentalmente un dispositivo multihomed con una scheda di rete toccando nella rete privata di hello cliente e una scheda di rete con connessione hello rete pubblica. Entità dell'infrastruttura di Azure non è possibile toccare in reti private del cliente per motivi di conformità, pertanto è necessario endpoint pubblici tooutilize per la comunicazione di infrastruttura. gli endpoint pubblici Hello periodicamente vengono analizzati dal controllo di sicurezza di Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Altre informazioni sui tipi di gateway, i requisiti e la velocità effettiva

Per altre informazioni, [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="s2s"></a>Connessioni da sito a sito e dispositivi VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Quali sono gli aspetti di cui tenere conto nella scelta di un dispositivo VPN?

È stato convalidato un set di dispositivi VPN da sito a sito standard in collaborazione con fornitori di dispositivi. Un elenco di dispositivi VPN sicuramente compatibili, le istruzioni di configurazione corrispondente o esempi e le specifiche di dispositivo è reperibile in hello [informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) articolo. Tutti i dispositivi di famiglie di dispositivi hello indicate la compatibilità nota dovrebbero funzionare con rete virtuale. toohelp configurare il dispositivo VPN, vedere esempio di configurazione del dispositivo toohello o collegamento che corrisponde il gruppo di dispositivi tooappropriate.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Dove è possibile reperire le impostazioni di configurazione per i dispositivi VPN?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Come è possibile modificare gli esempi di configurazione del dispositivo VPN?

Per informazioni sulla modifica degli esempi, vedere [Modifica degli esempi di configurazione di dispositivo](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Dove è possibile reperire i parametri IPsec e IKE?

Per informazioni sui parametri IPsec/IKE, vedere [Parametri](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Perché il tunnel VPN basato su criteri si arresta quando il traffico è inattivo?

Questo comportamento è previsto per gateway VPN basate su criteri (anche note come routing statico). Quando il traffico di hello tramite tunnel hello è inattivo per più di 5 minuti, tunnel hello verrà eliminata verso il basso. Quando il traffico viene avviato il flusso in entrambe le direzioni, tunnel hello verranno ristabilite immediatamente.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>È possibile utilizzare software VPN tooconnect tooAzure?

Sono supportati server RRAS (Routing e Accesso remoto) in Windows Server 2012 per la configurazione da sito a sito cross-premise.

Con il gateway dovrebbero funzionare altre soluzioni software VPN, purché siano conformi tooindustry implementazioni di IPsec standard. Contattare il fornitore di hello del software hello per le istruzioni di configurazione e supporto.

## <a name="P2S"></a>Connessioni da punto a sito

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Connessioni da rete virtuale a rete virtuale e multisito

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>È possibile utilizzare il traffico di tootransit gateway VPN di Azure tra my siti locali o di una rete virtuale tooanother?

**Modello di distribuzione Resource Manager**<br>
Sì. Vedere hello [BGP](#bgp) sezione per ulteriori informazioni.

**Modello di distribuzione classica**<br>
Traffico in transito tramite gateway VPN di Azure, è possibile utilizzare il modello di distribuzione classica hello, ma si basa su spazi di indirizzi definiti in modo statico nel file di configurazione di rete hello. Il protocollo BGP non è ancora supportato con i gateway VPN e reti virtuali di Azure utilizzando il modello di distribuzione classica hello. Senza BGP la definizione manuale degli spazi di indirizzi in transito è soggetta a errori e non è consigliata.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure genera hello stesso IPsec/IKE già condivise per tutte le connessioni VPN per hello chiave stessa rete virtuale?

No, per impostazione predefinita vengono generate chiavi precondivise diverse per connessioni VPN diverse. Tuttavia, è possibile utilizzare hello impostare VPN Gateway chiave API REST o PowerShell cmdlet tooset hello chiave valore desiderato. chiave di Hello deve essere una stringa alfanumerica di lunghezza compresa tra 1 too128 caratteri.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Si ottiene maggiore larghezza di banda con più VPN da sito a sito per una singola rete virtuale?

No, tutti i tunnel VPN, inclusi VPN Point-to-Site, condividono hello stesso Azure VPN gateway e hello larghezza di banda disponibile.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>È possibile configurare più tunnel tra una rete virtuale e un sito locale usando una VPN multisito?

Sì, ma è necessario configurare BGP su entrambi toohello tunnel nello stesso percorso.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>È possibile usare VPN da punto a sito con la rete virtuale con più tunnel VPN?

Sì, VPN da punto a sito (P2S) utilizzabile con gateway VPN hello connessione siti locali toomultiple e altre reti virtuali.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>È possibile collegare una rete virtuale con VPN IPsec toomy circuito ExpressRoute?

Sì, questa operazione è supportata. Per altre informazioni, vedere [Configurare connessioni ExpressRoute e VPN da sito a sito coesistenti](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="ipsecike"></a>Criteri IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Connettività cross-premise e macchine virtuali

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Se la macchina virtuale è in una rete virtuale e dispone di una connessione cross-premise, come è necessario connettersi toohello macchina virtuale?

Sono disponibili diverse opzioni. Se si dispone di RDP è abilitato per la macchina virtuale, è possibile connettersi macchina virtuale tooyour utilizzando l'indirizzo IP privato hello. In tal caso, specificare l'indirizzo IP privato hello e la porta hello che si desidera tooconnect troppo (in genere 3389). È necessario porta hello tooconfigure sulla macchina virtuale per il traffico di hello.

È inoltre possibile connettere macchine virtuali tooyour dall'indirizzo IP privato da un'altra macchina virtuale in cui è memorizzato hello stessa rete virtuale. Macchina virtuale di tooyour RDP non è possibile tramite l'indirizzo IP privato hello se ci si connette da una posizione all'esterno della rete virtuale. Ad esempio, se si dispone di una rete virtuale Point-to-Site configurata e non si stabilisce una connessione dal computer, è possibile connettersi macchina virtuale toohello per indirizzo IP privato.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Se la macchina virtuale è in una rete virtuale con connettività cross-premise, tutto il traffico hello dalla macchina virtuale passa attraverso tale connessione?

No. Solo il traffico hello che ha una destinazione IP inclusa in hello rete virtuale locale rete intervalli di indirizzi IP specificati verranno sottoposte al gateway di rete virtuale hello. Traffico ha una destinazione IP si trova all'interno di rete virtuale hello sempre all'interno di rete virtuale hello. Il traffico inviato attraverso reti pubbliche toohello di hello del servizio di bilanciamento carico o se viene utilizzato il tunneling forzato, inviato tramite gateway VPN di Azure hello.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Come risolvere un tooa connessione RDP VM

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Domande frequenti su Rete virtuale

Visualizzare le informazioni di rete virtuali aggiuntive in hello [domande frequenti sulla rete virtuale](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).
* Per altre informazioni sulle impostazioni di configurazione del gateway VPN, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).
