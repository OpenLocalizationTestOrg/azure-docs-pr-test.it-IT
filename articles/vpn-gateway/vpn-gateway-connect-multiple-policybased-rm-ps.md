---
title: 'Collegare Azure VPN gateway toomultiple locale basata su criteri VPN dispositivi: Gestione risorse di Azure: PowerShell | Documenti Microsoft'
description: In questo articolo illustra la configurazione di Azure basate su route VPN gateway toomultiple basato su criteri di dispositivi VPN tramite Gestione risorse di Azure e PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="89c94-103">La connessione VPN di Azure gateway toomultiple locale basata su criteri dispositivi VPN con PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c94-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="89c94-104">In questo articolo consente di configurare un Azure basato su route VPN gateway tooconnect toomultiple locale basata su criteri dispositivi VPN sfruttando i criteri IPsec/IKE personalizzati per le connessioni VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="89c94-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="89c94-105">Informazioni sui gateway VPN basati su criteri e basati su route</span><span class="sxs-lookup"><span data-stu-id="89c94-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="89c94-106">Criteri: *e* basato su route dispositivi VPN può variare come i selettori di traffico IPsec hello sono impostati su una connessione:</span><span class="sxs-lookup"><span data-stu-id="89c94-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="89c94-107">**Basata su criteri** dispositivi VPN utilizzano combinazioni di hello di prefissi da entrambi toodefine reti come il traffico è crittografati/decrittografati tramite i tunnel IPsec.</span><span class="sxs-lookup"><span data-stu-id="89c94-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="89c94-108">Sono basati in genere su dispositivi firewall che eseguono il filtro dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="89c94-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="89c94-109">Crittografia e decrittografia IPsec del tunnel vengono aggiunti filtri pacchetti toohello e motore di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="89c94-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="89c94-110">**Basato su route** dispositivi VPN usano selettori di traffico any per qualsiasi (carattere jolly) e consentono di routing/inoltro tabelle i tunnel IPsec toodifferent il traffico diretto.</span><span class="sxs-lookup"><span data-stu-id="89c94-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="89c94-111">Sono basati in genere su piattaforme router in cui ogni tunnel IPsec è modellato come interfaccia di rete o interfaccia di tunnel virtuale.</span><span class="sxs-lookup"><span data-stu-id="89c94-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="89c94-112">Hello nei diagrammi seguenti evidenziare due modelli di hello:</span><span class="sxs-lookup"><span data-stu-id="89c94-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="89c94-113">Esempio di VPN basata su criteri</span><span class="sxs-lookup"><span data-stu-id="89c94-113">Policy-based VPN example</span></span>
![basata su criteri](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="89c94-115">Esempio di VPN basata su route</span><span class="sxs-lookup"><span data-stu-id="89c94-115">Route-based VPN example</span></span>
![basata su route](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="89c94-117">Supporto di Azure per la VPN basata su criteri</span><span class="sxs-lookup"><span data-stu-id="89c94-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="89c94-118">Azure supporta attualmente entrambe le modalità di gateway VPN: gateway VPN basati su route e gateway VPN basati su criteri.</span><span class="sxs-lookup"><span data-stu-id="89c94-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="89c94-119">Sono basati su piattaforme interne diverse e quindi su specifiche diverse:</span><span class="sxs-lookup"><span data-stu-id="89c94-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="89c94-120">**Gateway VPN basato su criteri**</span><span class="sxs-lookup"><span data-stu-id="89c94-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="89c94-121">**Gateway VPN basato su route**</span><span class="sxs-lookup"><span data-stu-id="89c94-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="89c94-122">**SKU del gateway di Azure**</span><span class="sxs-lookup"><span data-stu-id="89c94-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="89c94-123">Basic</span><span class="sxs-lookup"><span data-stu-id="89c94-123">Basic</span></span>                       | <span data-ttu-id="89c94-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="89c94-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="89c94-125">**Versione IKE**</span><span class="sxs-lookup"><span data-stu-id="89c94-125">**IKE version**</span></span>          | <span data-ttu-id="89c94-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="89c94-126">IKEv1</span></span>                       | <span data-ttu-id="89c94-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="89c94-127">IKEv2</span></span>                                    |
| <span data-ttu-id="89c94-128">**Max. connessioni da sito a sito**</span><span class="sxs-lookup"><span data-stu-id="89c94-128">**Max. S2S connections**</span></span> | <span data-ttu-id="89c94-129">**1**</span><span class="sxs-lookup"><span data-stu-id="89c94-129">**1**</span></span>                       | <span data-ttu-id="89c94-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="89c94-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="89c94-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="89c94-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="89c94-132">Con i criteri IPsec/IKE personalizzato di hello, è ora possibile configurare Azure basato su route VPN gateway toouse basata su prefisso selettori di traffico con l'opzione "**PolicyBasedTrafficSelectors**", i dispositivi VPN basata su criteri locali tooon tooconnect.</span><span class="sxs-lookup"><span data-stu-id="89c94-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="89c94-133">Questa funzionalità consente tooconnect da una rete virtuale di Azure e toomultiple gateway VPN locale basata su criteri dispositivi VPN/firewall, rimuovere il limite di singola connessione hello hello corrente Azure basata su criteri gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="89c94-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="89c94-134">tooenable la connettività, devono supportare i dispositivi VPN basata su criteri di on-premise **IKEv2** tooconnect toohello Azure basato su route gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="89c94-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="89c94-135">Controllare le specifiche dei dispositivi VPN.</span><span class="sxs-lookup"><span data-stu-id="89c94-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="89c94-136">reti locali Hello connessione tramite i dispositivi VPN basata su criteri con questo meccanismo possono connettersi solo toohello rete virtuale Azure. **Impossibile transito tooother sulle reti locali o reti virtuali tramite hello stesso gateway VPN di Azure**.</span><span class="sxs-lookup"><span data-stu-id="89c94-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="89c94-137">opzione di configurazione Hello fa parte del criterio di connessione IPsec/IKE personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="89c94-138">Se si abilita l'opzione selettore di hello traffico basata su criteri, è necessario specificare i criteri di hello completa (algoritmi di crittografia e l'integrità IPsec/IKE chiave punti di forza e durate SA).</span><span class="sxs-lookup"><span data-stu-id="89c94-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="89c94-139">Hello seguente diagramma mostra il routing di transito tramite gateway VPN di Azure perché non funziona con l'opzione di hello basata su criteri:</span><span class="sxs-lookup"><span data-stu-id="89c94-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![transito basato su criteri](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="89c94-141">Come illustrato nel diagramma hello, gateway VPN di Azure hello dispone i selettori di traffico da hello tooeach di rete virtuale di prefissi di rete locale hello, ma non i prefissi di hello tra le connessioni.</span><span class="sxs-lookup"><span data-stu-id="89c94-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="89c94-142">Ad esempio, il sito locale 2, sito 3 e 4 sito può ogni comunicano tooVNet1 rispettivamente, ma non è possibile connettersi tramite hello Azure VPN gateway tooeach altri.</span><span class="sxs-lookup"><span data-stu-id="89c94-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="89c94-143">viene illustrata l'Hello hello incrociare i selettori di traffico che non sono disponibili in gateway VPN di Azure hello in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="89c94-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="89c94-144">Configurare selettori di traffico basati su criteri in una connessione</span><span class="sxs-lookup"><span data-stu-id="89c94-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="89c94-145">Hello istruzioni in seguito in questo articolo hello stesso esempio, come descritto in [criteri IPsec/IKE configurare per le connessioni S2S o di rete virtuale a](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish una connessione VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="89c94-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="89c94-146">Come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="89c94-146">This is shown in hello following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="89c94-148">Hello tooenable del flusso di lavoro di questo tipo di connettività:</span><span class="sxs-lookup"><span data-stu-id="89c94-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="89c94-149">Creare la rete virtuale hello, gateway VPN e gateway di rete locale per la connessione tra più sedi locali</span><span class="sxs-lookup"><span data-stu-id="89c94-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="89c94-150">Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="89c94-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="89c94-151">Applicare i criteri di hello quando si crea una connessione S2S o di rete virtuale a, e **abilitare i selettori di traffico basata su criteri hello** connessione hello</span><span class="sxs-lookup"><span data-stu-id="89c94-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="89c94-152">Se la connessione hello è già stata creata, è possibile applicare o aggiornare la connessione esistente hello criteri tooan</span><span class="sxs-lookup"><span data-stu-id="89c94-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="89c94-153">Abilitare i selettori di traffico basati su criteri in una connessione</span><span class="sxs-lookup"><span data-stu-id="89c94-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="89c94-154">Assicurarsi di aver completato [parte 3 dell'articolo di criteri IPsec/IKE configurare hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) per questa sezione.</span><span class="sxs-lookup"><span data-stu-id="89c94-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="89c94-155">Hello seguente viene illustrato come utilizzare hello stessi parametri e passaggi:</span><span class="sxs-lookup"><span data-stu-id="89c94-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="89c94-156">Passaggio 1: creare una rete virtuale hello gateway VPN e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="89c94-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="89c94-157">1. Dichiarare le variabili & connessione tooyour sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="89c94-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="89c94-158">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="89c94-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="89c94-159">Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="89c94-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
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
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="89c94-160">hello toouse cmdlet di gestione risorse, accertarsi di passare in modalità tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="89c94-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="89c94-161">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="89c94-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="89c94-162">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="89c94-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="89c94-163">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="89c94-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="89c94-164">2. Creare la rete virtuale hello, gateway VPN e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="89c94-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="89c94-165">Hello di esempio seguente crea rete virtuale hello, TestVNet1 con tre subnet e il gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="89c94-166">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="89c94-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="89c94-167">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="89c94-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="89c94-168">Passaggio 2: Creare una connessione VPN da sito a sito con un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="89c94-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="89c94-169">1. Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="89c94-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c94-170">È necessario un criterio IPsec/IKE in ordine tooenable "UsePolicyBasedTrafficSelectors" opzione nella connessione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="89c94-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="89c94-171">Hello seguente viene creato un criterio IPsec/IKE con questi algoritmi e parametri:</span><span class="sxs-lookup"><span data-stu-id="89c94-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="89c94-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="89c94-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="89c94-173">IPsec: AES256, SHA256, PFS24, durata dell'associazione di sicurezza 3600 secondi e 2048 KB</span><span class="sxs-lookup"><span data-stu-id="89c94-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="89c94-174">2. Creare una connessione VPN S2S hello con i selettori di traffico basata su criteri e i criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="89c94-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="89c94-175">Creare una connessione VPN S2S e applicare i criteri IPsec/IKE hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="89c94-176">Tenere presenti parametri aggiuntivi hello "-UsePolicyBasedTrafficSelectors $True" che consente i selettori di traffico basata su criteri in connessione hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="89c94-177">Dopo aver completato i passaggi di hello, hello connessione VPN S2S utilizzare hello definiti criteri IPsec/IKE e abilitare i selettori di traffico basata su criteri in connessione hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="89c94-178">È possibile ripetere hello stessi passaggi tooadd altre connessioni tooadditional locale basata su criteri dispositivi VPN da hello stesso gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="89c94-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="89c94-179">Aggiornare i selettori di traffico basati su criteri per una connessione</span><span class="sxs-lookup"><span data-stu-id="89c94-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="89c94-180">Hello ultima sezione viene illustrato come i selettori di traffico basata su criteri hello tooupdate opzione per una connessione VPN S2S esistente.</span><span class="sxs-lookup"><span data-stu-id="89c94-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="89c94-181">1. Ottenere la connessione di hello</span><span class="sxs-lookup"><span data-stu-id="89c94-181">1. Get hello connection</span></span>
<span data-ttu-id="89c94-182">Ottenere la risorsa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="89c94-183">2. Selezionare opzione di selettori hello traffico basata su criteri</span><span class="sxs-lookup"><span data-stu-id="89c94-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="89c94-184">Hello seguente linea indica se i selettori di traffico basata su criteri hello vengono utilizzati per la connessione hello:</span><span class="sxs-lookup"><span data-stu-id="89c94-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="89c94-185">Se la riga hello restituisce "**True**", quindi i selettori di traffico basata su criteri sono configurati su connessione hello; in caso contrario restituisce "**False**."</span><span class="sxs-lookup"><span data-stu-id="89c94-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="89c94-186">3. Aggiornare i selettori di traffico basata su criteri hello in una connessione</span><span class="sxs-lookup"><span data-stu-id="89c94-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="89c94-187">Dopo aver ottenuto la risorsa di connessione hello, è possibile abilitare o disabilitare l'opzione hello.</span><span class="sxs-lookup"><span data-stu-id="89c94-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="89c94-188">Disabilitare UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="89c94-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="89c94-189">esempio Hello Disabilita opzione selettori di hello traffico basata su criteri, ma lascia hello criteri IPsec/IKE invariato:</span><span class="sxs-lookup"><span data-stu-id="89c94-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="89c94-190">Abilitare UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="89c94-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="89c94-191">esempio Hello Abilita l'opzione selettori hello traffico basata su criteri, ma lascia hello criteri IPsec/IKE invariato:</span><span class="sxs-lookup"><span data-stu-id="89c94-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="89c94-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89c94-192">Next steps</span></span>
<span data-ttu-id="89c94-193">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="89c94-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="89c94-194">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="89c94-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="89c94-195">Vedere anche [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configurare i criteri IPsec/IKE per le connessioni da sito a sito o da rete virtuale a rete virtuale) per altre informazioni sui criteri IPsec/IKE personalizzati.</span><span class="sxs-lookup"><span data-stu-id="89c94-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
