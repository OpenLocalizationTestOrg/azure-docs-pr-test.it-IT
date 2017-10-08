---
title: impostazioni del gateway per le connessioni di Azure cross-premise aaaVPN | Documenti Microsoft
description: Informazioni sulle impostazioni del gateway VPN per i gateway di rete virtuale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Informazioni sulle impostazioni di configurazione del gateway VPN

Un gateway VPN è un tipo di gateway di rete virtuale che invia traffico crittografato tra la rete virtuale e la posizione locale tramite una connessione pubblica. È anche possibile utilizzare un traffico di toosend VPN gateway tra reti virtuali in hello backbone di Azure.

Una connessione gateway VPN si basa sulla configurazione di hello di più risorse, ognuno dei quali contiene le impostazioni configurabili. Nelle sezioni di Hello in questo articolo viene hello risorse e impostazioni correlate al gateway VPN tooa per una rete virtuale creata nel modello di distribuzione di gestione risorse. È possibile trovare le descrizioni e i diagrammi di topologia per ogni soluzione di connessione in hello [sul Gateway VPN](vpn-gateway-about-vpngateways.md) articolo.

## <a name="gwtype"></a>Tipi di gateway

Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo. Quando si crea un gateway di rete virtuale, è necessario assicurarsi che il tipo di gateway hello sia corretto per la configurazione.

i valori disponibili per il tipo di gateway - Hello sono:

* VPN
* ExpressRoute

Un gateway VPN richiede hello `-GatewayType` *Vpn*.

Esempio:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKU del gateway

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Configurare il gateway di hello SKU

#### <a name="azure-portal"></a>Portale di Azure

Se si utilizza hello toocreate portale Azure un gateway di rete virtuale di gestione delle risorse, è possibile selezionare lo SKU del gateway hello utilizzando l'elenco a discesa hello. vengono visualizzate le opzioni di Hello corrispondono toohello tipo di Gateway e il tipo VPN selezionato.

#### <a name="powershell"></a>PowerShell

esempio di PowerShell seguente Hello specifica hello `-GatewaySku` come VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Modificare (ridimensionare) uno SKU del gateway

Se si desidera tooupgrade tooa SKU del gateway SKU più potente, è possibile utilizzare hello `Resize-AzureRmVirtualNetworkGateway` cmdlet di PowerShell. È anche possibile effettuare il downgrade di dimensioni SKU di gateway hello utilizzando questo cmdlet.

Hello esempio PowerShell seguente viene illustrato che un gateway SKU ridimensionata tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Tipi di connessione

Nel modello di distribuzione di gestione risorse hello, ogni configurazione richiede un tipo di connessione di gateway di rete virtuale specifica. Hello PowerShell di gestione risorse disponibili i valori del parametro `-ConnectionType` sono:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

Nel seguente esempio di PowerShell di hello, verrà creata una connessione di S2S che richiede il tipo di connessione hello *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Tipi di VPN

Quando si crea il gateway di rete virtuale hello per una configurazione di gateway VPN, è necessario specificare un tipo di VPN. tipo VPN che si sceglie di Hello dipende dalla topologia di connessione hello che si desidera toocreate. Ad esempio, una connessione P2S richiede un tipo di VPN RouteBased. Un tipo di VPN può dipendere anche da hardware hello che si sta utilizzando. Le configurazioni S2S richiedono un dispositivo VPN. Alcuni dispositivi VPN supportano solo un determinato tipo di VPN.

Hello tipo VPN selezionato deve soddisfare tutti i requisiti di connessione hello per soluzione hello desiderato toocreate. Ad esempio, se si desidera toocreate una connessione di gateway VPN S2S, un gateway VPN P2S per hello stessa rete virtuale, utilizzare il tipo VPN *tipo RouteBased* perché P2S richiede un tipo RouteBased VPN. È inoltre necessario che il dispositivo VPN è supportata una connessione VPN RouteBased tooverify. 

Dopo aver creato un gateway di rete virtuale, è possibile modificare il tipo VPN hello. È possibile toodelete hello gateway di rete virtuale e crearne uno nuovo. Sono disponibili due tipi di VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

esempio di PowerShell seguente Hello specifica hello `-VpnType` come *tipo RouteBased*. Quando si crea un gateway, è necessario assicurarsi che hello - VpnType sia corretto per la configurazione.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Requisiti del gateway

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Subnet del gateway

Prima di creare un gateway VPN, è necessario creare una subnet del gateway. subnet del gateway Hello contiene indirizzi IP hello tale gateway di rete virtuale hello macchine virtuali e servizi utilizzano. Quando si crea il gateway di rete virtuale, gateway di macchine virtuali sono subnet del gateway toohello distribuito e configurato con impostazioni del gateway VPN hello necessario. È non necessario distribuire mai subnet del gateway toohello qualsiasi altra operazione (ad esempio, altre macchine virtuali). subnet del gateway Hello devono essere denominate 'GatewaySubnet' toowork correttamente. Denominazione subnet del gateway hello consente 'GatewaySubnet' Azure sapere che si è gateway di rete virtuale hello toodeploy subnet hello macchine virtuali e servizi.

Quando si crea una subnet del gateway hello, specificare il numero di indirizzi IP che hello subnet hello contiene. gli indirizzi IP di Hello nella subnet del gateway hello sono allocati toohello macchine virtuali del gateway e il servizio gateway. Alcune configurazioni richiedono più indirizzi IP di altre. Esaminare le istruzioni di hello per configurazione hello toocreate desiderato e verificare che la subnet gateway hello desiderato toocreate soddisfi tali requisiti. Inoltre, si consiglia di toomake che la subnet gateway contenga sufficiente IP indirizzi tooaccommodate future ulteriori configurazioni possibili. Anche se è possibile creare una subnet del gateway con dimensioni pari a /29, è consigliabile crearne una con dimensioni pari a /28 o superiori, ad esempio /28, /27, /26 e così via. In questo modo, se si aggiunge una funzionalità in futuro, hello non hanno tootear il gateway, quindi eliminare e ricreare hello gateway subnet tooallow per più indirizzi IP.

Hello Gestione risorse di PowerShell riportato di seguito una subnet del gateway denominata GatewaySubnet. È possibile visualizzare la notazione CIDR hello specifica un /27, che consente agli indirizzi IP sufficienti per la maggior parte delle configurazioni esistenti.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Gateway di rete locali

Quando si crea una configurazione di gateway VPN, il gateway di rete locale hello rappresenta spesso il percorso locale. Nel modello di distribuzione classica hello, gateway di rete locale hello è tooas di cui si fa riferimento un sito locale. 

Assegnare un nome di gateway di rete locale hello, indirizzo IP pubblico del dispositivo VPN locale di hello hello e specificare i prefissi di indirizzo hello che si trovano nel percorso locale hello. Azure esamina i prefissi di indirizzo di destinazione hello il traffico di rete, consulta configurazione hello specificate per il gateway di rete locale e indirizza i pacchetti di conseguenza. È anche possibile specificare i gateway di rete locale per le configurazioni da rete virtuale a rete virtuale che usano una connessione di gateway VPN.

esempio di PowerShell seguente Hello crea un nuovo gateway di rete locale:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Talvolta è necessario impostazioni del gateway di rete locale hello toomodify. Ad esempio, quando si aggiunge o Modifica intervallo di indirizzi hello o se cambia indirizzo IP di hello del dispositivo VPN hello. Per una rete virtuale classica, è possibile modificare queste impostazioni nel portale classico di hello nella pagina reti locali hello. Per Resource Manager, vedere [Modificare le impostazioni del gateway di rete locale usando PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>API REST e cmdlet PowerShell

Per ulteriori risorse tecniche e requisiti di sintassi specifica per l'utilizzo di CLI di Azure, i cmdlet di PowerShell o le API REST per le configurazioni del Gateway VPN, vedere hello seguenti pagine:

| **Classico** | **Gestione risorse** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [API REST](https://msdn.microsoft.com/library/jj154113) |[API REST](/rest/api/network/virtualnetworkgateways) |
| Non supportate | [Interfaccia della riga di comando di Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).