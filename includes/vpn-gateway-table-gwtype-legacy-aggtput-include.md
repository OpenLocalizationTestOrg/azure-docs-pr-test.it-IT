Hello nella tabella seguente mostra i tipi di gateway hello e velocità effettiva aggregata di hello stimato per lo SKU del gateway. Questa tabella si applica toohello Gestione risorse e i modelli di distribuzione classica. 

I prezzi variano a seconda dello SKU del gateway. Per altre informazioni, vedere [Gateway VPN Prezzi](https://azure.microsoft.com/pricing/details/vpn-gateway).

Si noti che gateway UltraPerformance hello che SKU non è rappresentato in questa tabella. Per informazioni su hello UltraPerformance SKU, vedere hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentazione.

|  | **Velocità effettiva del gateway VPN (1)** | **Tunnel IPsec massimi del gateway VPN (2)** | **Velocità effettiva del gateway di ExpressRoute** | **Coesistenza gateway VPN ed ExpressRoute** |
| --- | --- | --- | --- | --- |
| **SKU Basic (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |No |
| **SKU Standard (4)(5)** |100 Mbps |10 |1000 Mbps |Sì |
| **SKU con prestazioni elevate (4)** |200 Mbps |30 |2000 Mbps |Sì |


(1) velocità effettiva VPN hello è una stima approssimativa basata sulle misure hello tra reti virtuali in hello stessa area di Azure. Non è una velocità effettiva garantita per le connessioni cross-premise tra hello Internet. Misura la velocità effettiva massima possibile hello è.

(2) numero di hello di tunnel, fare riferimento tooRouteBased VPN. Una VPN PolicyBased può supportare solo un tunnel VPN da sito a sito.

(3) il protocollo BGP non è supportato per SKU Basic hello.

(4) Le VPN basate su criteri non sono supportate in questo SKU. Sono supportati per hello SKU Basic.

(5) Le connessioni del gateway VPN S2S attivo/attivo non sono supportate per questo SKU. Attivo-attivo è supportato in hello HighPerformance SKU.

(6) Lo SKU Basic è deprecato per l'uso con ExpressRoute.
