domande frequenti per rete virtuale a Hello applica connessioni Gateway tooVPN. Per informazioni sul peering reti virtuali, vedere [Peering di rete virtuale](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>È previsto un addebito per il traffico tra le reti virtuali?

Traffico di rete virtuale all'interno di hello stessa area geografica è gratuita per entrambe le direzioni quando si utilizza una connessione gateway VPN. Tra l'area di rete virtuale a uscita traffico viene addebitato con hello velocità di trasferimento dati in uscita tra reti virtuali in base alle aree di origine hello. Fare riferimento toohello [Gateway VPN di pagina dei prezzi](https://azure.microsoft.com/pricing/details/vpn-gateway/) per informazioni dettagliate. Se ci si connette le reti virtuali utilizzando Peering reti virtuali, anziché Gateway VPN, vedere hello [pagina dei prezzi di rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>Il traffico di rete virtuale a attraversare Internet hello?

No. Il traffico di rete virtuale a viaggia attraverso hello backbone di Microsoft Azure, non hello Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Il traffico tra reti virtuali è sicuro?

Sì, è protetto mediante la crittografia IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>È necessario un tooconnect dispositivo VPN reti virtuali insieme?

No. Per il collegamento di più reti virtuali di Azure non è necessario un dispositivo VPN, a meno che non sia necessaria la connettività cross-premise.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>La reti virtuali richiedono toobe in hello stessa regione?

No. reti virtuali di Hello possono trovarsi in hello uguali o diverse aree di Azure (posizioni).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Se hello reti virtuali non è nello stesso hello necessario di sottoscrizione, le sottoscrizioni di hello toobe associato hello AD stesso tenant?

No.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>È possibile usare la connessione da rete virtuale a rete virtuale insieme alle connessioni multisito?

Sì. La connettività di rete virtuale può essere usata contemporaneamente con VPN multisito,

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>A quanti siti locali e reti virtuali può connettersi una rete virtuale?

Vedere la tabella [Requisiti del gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>È possibile utilizzare tooconnect per rete virtuale a macchine virtuali o servizi all'esterno di una rete virtuale cloud?

No. La connettività da VNet a VNet supporta la connessione di reti virtuali. Non supporta la connessione di macchine virtuali o servizi cloud non inclusi in una rete virtuale.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>È possibile estendere un servizio cloud o un endpoint del servizio di bilanciamento del carico in più reti virtuali?

No. Un servizio cloud o un endpoint di bilanciamento del carico non può estendersi tra reti virtuali, anche se sono connesse tra loro.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>È possibile usare una VPN di tipo PolicyBased per connessioni da rete virtuale a rete virtuale o multisito?

No. La connettività tra reti virtuali e multisito richiede la presenza di gateway VPN con tipi VPN RouteBased (in precedenza denominato routing dinamico).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>È possibile connettere una rete virtuale con un tooanother tipo VPN tipo RouteBased rete virtuale con un tipo di VPN PolicyBased?

No, entrambe le reti virtuali DEVONO usare VPN basate su route (denominate in precedenza routing dinamico).

### <a name="do-vpn-tunnels-share-bandwidth"></a>I tunnel VPN condividono la larghezza di banda?

Sì. Tutti i tunnel VPN della rete virtuale hello condividono larghezza di banda disponibile hello nel gateway VPN di Azure hello e hello stesso VPN gateway tempi di attività contratto di servizio in Azure.

### <a name="are-redundant-tunnels-supported"></a>Sono supportati i tunnel ridondanti?

I tunnel ridondanti tra una coppia di reti virtuali sono supportati quando un gateway di rete virtuale è configurato come attivo/attivo.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>È consentita la sovrapposizione di spazi di indirizzi per configurazioni da rete virtuale a rete virtuale?

No. Gli intervalli di indirizzi IP non possono sovrapporsi.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Possono esistere spazi di indirizzi sovrapposti tra le reti virtuali connesse e i siti locali?

No. Gli intervalli di indirizzi IP non possono sovrapporsi.



