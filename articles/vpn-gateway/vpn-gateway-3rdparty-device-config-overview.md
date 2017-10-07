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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="2d977-103">Panoramica delle configurazioni di dispositivi VPN di terze parti</span><span class="sxs-lookup"><span data-stu-id="2d977-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="2d977-104">In questo articolo viene fornita una panoramica delle configurazioni di dispositivo VPN locale per la connessione gateway VPN tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2d977-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="2d977-105">esempio Hello rete virtuale di Azure e VPN gateway il programma di installazione sarà tooconnect utilizzati dispositivi VPN locali di toodifferent con hello stessi parametri.</span><span class="sxs-lookup"><span data-stu-id="2d977-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="2d977-106">Requisiti del dispositivo</span><span class="sxs-lookup"><span data-stu-id="2d977-106">Device requirements</span></span>
<span data-ttu-id="2d977-107">I gateway VPN di Azure usano gruppi di protocollo IPsec/IKE standard per i tunnel VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="2d977-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="2d977-108">Fare riferimento troppo[informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) per hello dettagliato i parametri del protocollo IPsec/IKE e gli algoritmi di crittografia predefinita per i gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d977-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="2d977-109">È possibile specificare facoltativamente l'esatta combinazione di hello di algoritmi di crittografia e vantaggi chiave per una connessione specifica come descritto in [sui requisiti di crittografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="2d977-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="2d977-110"><a name ="singletunnel"></a>Tunnel per VPN unico</span><span class="sxs-lookup"><span data-stu-id="2d977-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="2d977-111">topologia prima Hello è costituita da un singolo tunnel VPN S2S tra un gateway VPN di Azure e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="2d977-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="2d977-112">È possibile configurare BGP attraverso i tunnel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="2d977-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![tunnel unico](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="2d977-114">Fare riferimento troppo[configurare connessione site-to-site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) per indicazioni passo passo dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2d977-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="2d977-115">Hello nelle sezioni seguenti vengono elencati i parametri di hello e forniscono un toohelp di script di PowerShell di esempio iniziare.</span><span class="sxs-lookup"><span data-stu-id="2d977-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="2d977-116">Informazioni sul gateway di rete e VPN</span><span class="sxs-lookup"><span data-stu-id="2d977-116">Network and VPN gateway information</span></span>
<span data-ttu-id="2d977-117">In questa sezione elenco parametri hello per esempi di hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="2d977-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="2d977-118">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="2d977-118">**Parameter**</span></span>                | <span data-ttu-id="2d977-119">**Valore**</span><span class="sxs-lookup"><span data-stu-id="2d977-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="2d977-120">Prefissi di indirizzi di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2d977-120">VNet address prefixes</span></span>        | <span data-ttu-id="2d977-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d977-121">10.11.0.0/16</span></span><br><span data-ttu-id="2d977-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d977-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="2d977-123">Indirizzo IP del gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="2d977-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="2d977-124">Indirizzo IP del gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="2d977-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="2d977-125">Prefissi di indirizzi locali</span><span class="sxs-lookup"><span data-stu-id="2d977-125">On-premises address prefixes</span></span> | <span data-ttu-id="2d977-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d977-126">10.51.0.0/16</span></span><br><span data-ttu-id="2d977-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d977-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="2d977-128">Indirizzo IP del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="2d977-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="2d977-129">Indirizzo IP del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="2d977-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="2d977-130">*BGP ASN della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2d977-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="2d977-131">65010</span><span class="sxs-lookup"><span data-stu-id="2d977-131">65010</span></span>                        |
| <span data-ttu-id="2d977-132">*Indirizzo IP del peer BGP di Azure</span><span class="sxs-lookup"><span data-stu-id="2d977-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="2d977-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="2d977-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="2d977-134">*ASN BGP locale</span><span class="sxs-lookup"><span data-stu-id="2d977-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="2d977-135">65050</span><span class="sxs-lookup"><span data-stu-id="2d977-135">65050</span></span>                        |
| <span data-ttu-id="2d977-136">*Indirizzo IP del peer BGP locale</span><span class="sxs-lookup"><span data-stu-id="2d977-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="2d977-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="2d977-137">10.52.255.254</span></span>                |

* <span data-ttu-id="2d977-138">(*) Parametri facoltativi solo per BGP</span><span class="sxs-lookup"><span data-stu-id="2d977-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="2d977-139">Script PowerShell di esempio</span><span class="sxs-lookup"><span data-stu-id="2d977-139">Sample PowerShell script</span></span>
<span data-ttu-id="2d977-140">[Creare una connessione VPN S2S tramite PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2d977-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="2d977-141">In questa sezione fornisce una tooget di script di esempio che è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="2d977-141">This section provides a sample script tooget you started.</span></span>

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

### <span data-ttu-id="2d977-142"><a name ="policybased"></a>[Facoltativo] Usare criteri IPsec/IKE personalizzati con "UsePolicyBasedTrafficSelectors"</span><span class="sxs-lookup"><span data-stu-id="2d977-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="2d977-143">Se il dispositivo VPN non supporta i selettori di traffico "any-to-any" (configurazione di base/VTI-basato su route), sarà anche necessario toocreate criteri IPsec/IKE personalizzati e configurare l'opzione "UsePolicyBasedTrafficSelectors" come descritto in [in questo articolo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2d977-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d977-144">È necessario un criterio IPsec/IKE in ordine tooenable "UsePolicyBasedTrafficSelectors" opzione nella connessione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d977-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="2d977-145">script di esempio Hello seguente crea un criterio IPsec/IKE con hello seguenti algoritmi e parametri:</span><span class="sxs-lookup"><span data-stu-id="2d977-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="2d977-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="2d977-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="2d977-147">IPsec: AES256, SHA1, PFS24, durata dell'associazione di sicurezza 7200 secondi e 20480000KB (20 GB)</span><span class="sxs-lookup"><span data-stu-id="2d977-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="2d977-148">Applica i criteri di hello e quindi consente "UesPolicyBasedTrafficSelectors" connessione hello.</span><span class="sxs-lookup"><span data-stu-id="2d977-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="2d977-149"><a name ="bgp"></a>[Facoltativo] Usare BGP per la connessione VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="2d977-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="2d977-150">Facoltativamente, è possibile utilizzare il protocollo BGP sulla connessione hello.</span><span class="sxs-lookup"><span data-stu-id="2d977-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="2d977-151">Vedere [BGP per gateway VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2d977-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="2d977-152">Sono presenti due differenze:</span><span class="sxs-lookup"><span data-stu-id="2d977-152">There are two differences:</span></span>

<span data-ttu-id="2d977-153">prefissi di indirizzi locali Hello possono essere un indirizzo host singolo, l'indirizzo IP del peer BGP hello locale:</span><span class="sxs-lookup"><span data-stu-id="2d977-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="2d977-154">È necessario impostare "-EnableBGP" troppo$ True quando si crea la connessione hello:</span><span class="sxs-lookup"><span data-stu-id="2d977-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="2d977-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d977-155">Next steps</span></span>
<span data-ttu-id="2d977-156">Vedere [la configurazione di gateway VPN attivo-attivo per Cross-premise e le connessioni di rete virtuale a](vpn-gateway-activeactive-rm-powershell.md) per passaggi tooconfigure attivo-attivo cross-premise e connessioni di rete virtuale a.</span><span class="sxs-lookup"><span data-stu-id="2d977-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

