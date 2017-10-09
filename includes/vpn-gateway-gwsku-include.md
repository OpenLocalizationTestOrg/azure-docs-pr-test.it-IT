Quando si crea un gateway di rete virtuale, è necessario gateway hello toospecify SKU che si desidera toouse. Selezionare gli SKU di hello che soddisfano i requisiti in base ai tipi di hello di carichi di lavoro, le velocità effettive, funzionalità e i contratti di servizio.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Carichi di lavoro di produzione *e* di sviluppo e test

A causa delle differenze toohello nei contratti di servizio e i set di funzionalità, è consigliabile hello seguenti SKU per la produzione *e* dev-test:

| **Carico di lavoro**                       | **SKU**               |
| ---                                | ---                    |
| **Carichi di lavoro critici, di produzione** | VpnGw1, VpnGw2, VpnGw3 |
| **Sviluppo e test o modello di verifica**   | Basic                  |
|                                    |                        |

Se si utilizza hello precedente SKU, indicazioni di SKU hello produzione sono Standard e ad alte prestazioni SKU. Per informazioni su hello precedente SKU, vedere [SKU di Gateway (SKU legacy)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Set di funzionalità degli SKU del gateway

Hello nuovo gateway SKU semplificata hello set di funzionalità offerte nei gateway hello:

| **SKU**| **Funzionalità**|
| ---    | ---         |
|**Basic**   | **VPN basata su route**: 10 tunnel con P2S<br><br>**VPN basata su criteri (IKEv1)**: 1 tunnel, nessuna connessione P2S|
| **VpnGw1, VpnGw2 e VpnGw3** | **Le VPN basate su route**: dei tunnel too30 (*), P2S, BGP, criteri IPsec/IKE attivo-attivo, personalizzati, coesistenza ExpressRoute/VPN |
|        |             |

(*) È possibile configurare tooconnect "PolicyBasedTrafficSelectors" una route dispositivi basati su VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple locale basata su criteri firewall. Fare riferimento troppo[toomultiple gateway VPN di connessione locale basata su criteri di dispositivi VPN con PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) per informazioni dettagliate.

###  <a name="resize"></a>Ridimensionamento degli SKU di gateway

1. È possibile eseguire il ridimensionamento tra gli SKU VpnGw1, VpnGw2 e VpnGw3.
2. Quando si lavora con gateway precedente hello SKU, è possibile ridimensionare tra Basic, Standard e ad alte prestazioni SKU.
2. Si **Impossibile** ridimensionamento da toohello SKU Basic/Standard/ad alte prestazioni nuovo VpnGw2/VpnGw1/VpnGw3 SKU. In alternativa, è necessario [migrare](#migrate) toohello SKU di nuovo.

###  <a name="migrate"></a>La migrazione dal vecchio SKU toohello nuovo SKU

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
