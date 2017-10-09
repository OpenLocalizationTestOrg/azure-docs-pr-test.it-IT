### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>BGP è supportato in tutti gli SKU del gateway VPN di Azure?
No. BGP è supportato nei gateway VPN **Standard** e **HighPerformance** di Azure. **Basic** NON è supportato.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>È possibile usare il protocollo BGP con i gateway VPN di Azure basati su criteri?
No, BGP è supportato unicamente nei gateway VPN basati su route.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>È possibile usare un numero sistema autonomo (ASN) privato?
Sì, è possibile usare il proprio ASN privato o ASN pubblici sia per le reti locali che per le reti virtuali di Azure.

### <a name="are-there-asns-reserved-by-azure"></a>Esistono ASN riservati da Azure?
Sì, hello ASN seguenti sono riservati da Azure per il peering interno ed esterno:

* ASN pubblici: 8075, 8076, 12076
* ASN privati: 65515, 65517, 65518, 65519, 65520

È possibile specificare questi ASN per i dispositivi VPN locali durante la connessione gateway VPN tooAzure.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Ci sono altri ASN che non è possibile usare?
Sì, hello seguente ASN è [riservato dall'autorità IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) e non può essere configurato nel Gateway VPN di Azure:

23456, 64496-64511, 65535-65551 e 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>È possibile utilizzare hello ASN stesso sia per on-premise reti VPN e reti virtuali di Azure?
No, è necessario assegnare ASN diversi alle reti locali e alle reti virtuali di Azure, se vengono connesse insieme tramite BGP. Ai gateway VPN di Azure è assegnato un ASN predefinito di 65515, sia che BGP sia abilitato o meno per la connettività cross-premise. È possibile eseguire l'override di questa impostazione predefinita tramite l'assegnazione di un altro numero ASN durante la creazione di gateway VPN hello o modificare ASN hello dopo aver creato il gateway hello. È necessario tooassign il toohello ASN locale corrispondente gateway di rete locale di Azure.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>L'indirizzo di prefissi verrà gateway VPN di Azure annunciare toome?
Gateway VPN di Azure annunceranno hello route tooyour locale BGP dispositivi seguenti:

* Prefissi di indirizzo di rete virtuale.
* Prefissi di indirizzo per ogni gateway VPN di Azure connessa toohello di gateway di rete locale
* Le route ottenute da altri BGP peering sessioni connesse toohello gateway VPN di Azure, **ad eccezione di predefinito o più route overlapped con un prefisso di rete virtuale**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>È possibile annunciare gateway VPN di tooAzure (0.0.0.0/0) di route predefinita?
Sì.

Tenere presente questo forzerà tutto il traffico di rete virtuale in uscita verso il sito locale e impedirà hello macchine virtuali di rete virtuale di accettare le comunicazioni pubbliche da hello Internet direttamente, tale RDP o SSH da hello Internet toohello macchine virtuali.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>È possibile annunciare prefissi esatta hello come my prefissi di rete virtuale?

No, hello pubblicità stesso prefisso a uno dei prefissi di indirizzo di rete virtuale verrà bloccata o filtrato in base hello piattaforma Azure. È tuttavia possibile pubblicizzare un prefisso che rappresenta un superset di ciò che si trova all'interno della rete virtuale. 

Ad esempio, se la rete virtuale utilizzata hello indirizzo spazio 10.0.0.0/16, è possibile pubblicizzare 10.0.0.0/8. ma non 10.0.0.0/16 o 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>È possibile usare BGP con le connessioni tra reti virtuali?
Sì, è possibile usare BGP sia per connessioni cross-premise che per connessioni tra reti virtuali.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>È possibile combinare connessioni BGP con connessioni non BGP per i gateway VPN di Azure?
Sì, è possibile combinare entrambe BGP e le connessioni non BGP per hello stesso gateway VPN di Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Il gateway VPN di Azure supporta il routing di transito BGP?
Sì, il routing di transito BGP è supportato con eccezione hello che gateway VPN di Azure verrà **non** annunciare predefinito instrada i peer BGP tooother. transito tooenable routing attraverso più gateway VPN di Azure, è necessario abilitare il protocollo BGP in tutte le connessioni di rete virtuale a intermedia.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>È possibile stabilire più di un tunnel tra il gateway VPN di Azure e la rete locale?
Sì, è possibile stabilire più di un tunnel VPN S2S tra un gateway VPN di Azure e la rete locale. Si noti che tutti questi tunnel verranno conteggiati rispetto al numero totale di hello di tunnel per il gateway VPN di Azure e che è necessario abilitare il protocollo BGP su entrambi i tunnel.

Ad esempio, se si dispone di due tunnel ridondanti tra il gateway VPN di Azure e una delle reti locali, si utilizzerà 2 tunnel fuori quota totale di hello per il gateway VPN di Azure (10 per il livello Standard) e 30 per ad alte prestazioni.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>È possibile stabilire più tunnel tra due reti virtuali di Azure con BGP?
Sì, ma almeno uno dei gateway di rete virtuale hello deve essere nella configurazione attivo-attivo.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>È possibile usare BGP per VPN S2S in una configurazione di coesistenza tra VPN ExpressRoute/S2S?
Sì. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Quale indirizzo viene usato dal gateway VPN di Azure per l'indirizzo IP del peer BGP?
gateway VPN di Azure Hello allocherà un singolo indirizzo IP hello intervallo GatewaySubnet definito per la rete virtuale hello. Per impostazione predefinita, è hello secondo ultimo indirizzo dell'intervallo di hello. Ad esempio, se il GatewaySubnet 10.12.255.0/27, compreso tra 10.12.255.0 too10.12.255.31, hello indirizzi IP Peer BGP nel gateway VPN di Azure hello sarà 10.12.255.30. È possibile trovare queste informazioni quando si elencano le informazioni di gateway VPN di Azure hello.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Quali sono i requisiti di hello per gli indirizzi IP Peer BGP hello dispositivo VPN?
L'indirizzo del peer BGP locali **non deve** essere hello stesso come indirizzo IP pubblico hello del dispositivo VPN. Utilizzare un diverso indirizzo IP dispositivo VPN hello per l'IP del Peer BGP. Può essere un indirizzo assegnato toohello loopback interfaccia sul dispositivo hello. Specificare l'indirizzo in hello Gateway di rete locale che rappresentano hello posizione corrispondente.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>Cosa è necessario specificare come i prefissi di indirizzo per hello Gateway di rete locale quando si utilizza il protocollo BGP?
Gateway di rete locale Azure specifica i prefissi di indirizzo iniziale hello per la rete locale hello. Con il protocollo BGP, è necessario allocare prefisso host hello (/ 32 prefisso) dell'indirizzo IP Peer BGP come spazio di indirizzi hello per la rete locale. Se l'IP del Peer BGP 10.52.255.254, è necessario specificare "10.52.255.254/32" come localNetworkAddressSpace hello di hello Gateway di rete locale che rappresenta la rete locale. Si tratta di tooensure che hello Azure VPN gateway stabilisce sessione BGP hello attraverso i tunnel VPN S2S hello.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>Cosa è necessario aggiungere dispositivo VPN locale di toomy per sessione di peering BGP hello?
È necessario aggiungere una route di host dell'indirizzo IP del Peer BGP Azure hello su dispositivo VPN che punta tunnel VPN S2S IPsec toohello. Se, ad esempio, hello Azure VPN Peer IP è "10.12.255.30", si deve aggiungere una route di host per "10.12.255.30" con un'interfaccia di hop successivo di interfaccia di tunnel IPsec corrispondente hello sul dispositivo VPN.

