---
title: aaaAbout 3rd party dispositivo configurazione tooconnect tooAzure VPN gateway VPN | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di 3 configurazioni di dispositivo VPN di terze parti per la connessione gateway VPN tooAzure.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Panoramica delle configurazioni di dispositivi VPN di terze parti
In questo articolo viene fornita una panoramica delle configurazioni di dispositivo VPN locale per la connessione gateway VPN tooAzure. esempio Hello rete virtuale di Azure e VPN gateway il programma di installazione sarà tooconnect utilizzati dispositivi VPN locali di toodifferent con hello stessi parametri.

## <a name="device-requirements"></a>Requisiti del dispositivo
I gateway VPN di Azure usano gruppi di protocollo IPsec/IKE standard per i tunnel VPN S2S. Fare riferimento troppo[informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) per hello dettagliato i parametri del protocollo IPsec/IKE e gli algoritmi di crittografia predefinita per i gateway VPN di Azure. È possibile specificare facoltativamente l'esatta combinazione di hello di algoritmi di crittografia e vantaggi chiave per una connessione specifica come descritto in [sui requisiti di crittografia](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Tunnel per VPN unico
topologia prima Hello è costituita da un singolo tunnel VPN S2S tra un gateway VPN di Azure e il dispositivo VPN locale. È possibile configurare BGP attraverso i tunnel VPN hello.

![tunnel unico](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Fare riferimento troppo[configurare connessione site-to-site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) per indicazioni passo passo dettagliate. Hello nelle sezioni seguenti vengono elencati i parametri di hello e forniscono un toohelp di script di PowerShell di esempio iniziare.

### <a name="network-and-vpn-gateway-information"></a>Informazioni sul gateway di rete e VPN
In questa sezione elenco parametri hello per esempi di hello precedenti.

| **Parametro**                | **Valore**                    |
| ---                          | ---                          |
| Prefissi di indirizzi di rete virtuale        | 10.11.0.0/16<br>10.12.0.0/16 |
| Indirizzo IP del gateway VPN di Azure         | Indirizzo IP del gateway VPN di Azure         |
| Prefissi di indirizzi locali | 10.51.0.0/16<br>10.52.0.0/16 |
| Indirizzo IP del dispositivo VPN locale    | Indirizzo IP del dispositivo VPN locale    |
| *BGP ASN della rete virtuale                | 65010                        |
| *Indirizzo IP del peer BGP di Azure           | 10.12.255.30                 |
| *ASN BGP locale         | 65050                        |
| *Indirizzo IP del peer BGP locale     | 10.52.255.254                |

* (*) Parametri facoltativi solo per BGP

### <a name="sample-powershell-script"></a>Script PowerShell di esempio
[Creare una connessione VPN S2S tramite PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello istruzioni dettagliate. In questa sezione fornisce una tooget di script di esempio che è stato avviato.

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <a name ="policybased"></a>[Facoltativo] Usare criteri IPsec/IKE personalizzati con "UsePolicyBasedTrafficSelectors"
Se il dispositivo VPN non supporta i selettori di traffico "any-to-any" (configurazione di base/VTI-basato su route), sarà anche necessario toocreate criteri IPsec/IKE personalizzati e configurare l'opzione "UsePolicyBasedTrafficSelectors" come descritto in [in questo articolo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> È necessario un criterio IPsec/IKE in ordine tooenable "UsePolicyBasedTrafficSelectors" opzione nella connessione hello toocreate.

script di esempio Hello seguente crea un criterio IPsec/IKE con hello seguenti algoritmi e parametri:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, durata dell'associazione di sicurezza 7200 secondi e 20480000KB (20 GB)

Applica i criteri di hello e quindi consente "UesPolicyBasedTrafficSelectors" connessione hello.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Facoltativo] Usare BGP per la connessione VPN da sito a sito
Facoltativamente, è possibile utilizzare il protocollo BGP sulla connessione hello. Vedere [BGP per gateway VPN](vpn-gateway-bgp-resource-manager-ps.md). Sono presenti due differenze:

prefissi di indirizzi locali Hello possono essere un indirizzo host singolo, l'indirizzo IP del peer BGP hello locale:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

È necessario impostare "-EnableBGP" troppo$ True quando si crea la connessione hello:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Passaggi successivi
Vedere [la configurazione di gateway VPN attivo-attivo per Cross-premise e le connessioni di rete virtuale a](vpn-gateway-activeactive-rm-powershell.md) per passaggi tooconfigure attivo-attivo cross-premise e connessioni di rete virtuale a.

