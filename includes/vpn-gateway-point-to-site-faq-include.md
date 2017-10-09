### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Quali sistemi operativi client è possibile usare con la connettività da punto a sito?

è supportato i seguenti sistemi operativi client Hello:

* Windows 7 (a 32 e 64 bit)
* Windows Server 2008 R2 (solo a 64 bit)
* Windows 8 (a 32 e 64 bit)
* Windows 8.1 (a 32 e 64 bit)
* Windows Server 2012 (solo a 64 bit)
* Windows Server 2012 R2 (solo a 64 bit)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Per la connettività da punto a sito è possibile usare qualsiasi client VPN software che supporta SSTP?

No. Il supporto è limitato solo toohello Windows versioni del sistema operativo elencate in precedenza.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Quanti endpoint client VPN è possibile includere nella configurazione da punto sito?

Un sostegno di too128 VPN client toobe tooconnect in grado di tooa rete virtuale in hello stesso tempo.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>È possibile usare la CA radice della PKI interna per la connettività da punto a sito?

Sì. In precedenza, era possibile utilizzare solo certificati radice autofirmati. È ancora possibile caricare 20 certificati radice.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>È possibile attraversare proxy e firewall con la funzionalità Da punto a sito

Sì. Utilizziamo tootunnel SSTP (Secure Socket Tunneling Protocol) attraverso i firewall. Questo tunnel verrà visualizzato come connessione HTTPs.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Se si riavvia un computer client configurato per Point-to-Site, verrà hello VPN verrà riconnessa automaticamente?

Per impostazione predefinita, computer client hello non verrà ristabilita connessione VPN hello automaticamente.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Supporta Point-to-Site la riconnessione automatica e DDNS su hello client VPN?

La riconnessione automatica e il DNS dinamico non sono supportati attualmente nelle VPN da punto a sito.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>È possibile avere Site-to-Site e per la coesistono di configurazioni Point-to-Site per hello stessa rete virtuale?

Sì. Entrambe queste soluzioni funzionano se si ha un tipo di VPN basata su route per il gateway. Per il modello di distribuzione classica hello, è necessario un gateway dinamico. Facciamo non supporto Point-to-Site per gateway VPN con routing statico o gateway tramite hello `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>È possibile configurare una rete virtuale Point-to-Site client tooconnect toomultiple in hello contemporaneamente?

Sì, è possibile. Ma le reti virtuali hello possono avere un prefisso IP sovrapposti e gli spazi degli indirizzi hello Point-to-Site non devono sovrapporsi tra reti virtuali hello.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Che velocità effettiva è possibile prevedere usando connessioni da sito a sito o da punto a sito?

È difficile toomaintain hello esattamente la velocità effettiva del tunnel VPN hello. IPSec e SSTP sono protocolli VPN con un elevato livello di crittografia. Velocità effettiva è limitata anche dalla latenza di hello e larghezza di banda tra la rete locale e hello Internet.
