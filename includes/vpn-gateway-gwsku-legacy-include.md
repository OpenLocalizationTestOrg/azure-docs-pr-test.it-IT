gli SKU di gateway VPN (precedente) legacy di Hello sono:

* Basic
* Standard
* HighPerformance

Gateway VPN non usare gateway UltraPerformance hello SKU. Per informazioni su hello UltraPerformance SKU, vedere hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentazione.

Quando si lavora con hello SKU legacy, considerare hello seguenti:

* Se si desidera un tipo di VPN PolicyBased toouse, è necessario utilizzare hello SKU Basic. Le VPN basate su criteri, precedentemente denominate routing statico, non sono supportate negli altri SKU.
* Il protocollo BGP non è supportato nella SKU Basic hello.
* Coesistenza Gateway VPN di ExpressRoute configurazioni non sono supportate nella SKU Basic hello.
* Connessioni Gateway VPN S2S attivo-attivo possono essere configurate in hello HighPerformance SKU.
