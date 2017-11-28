---
title: 'Configurare connessioni coesistenti ExpressRoute e VPN da sito a sito - Resource Manager: Azure| Microsoft Docs'
description: Questo articolo illustra come configurare connessioni VPN da sito a sito ed ExpressRoute coesistenti per il modello di distribuzione di Azure Resource Manager.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="694ee-103">Configurare connessioni coesistenti ExpressRoute e da sito a sito</span><span class="sxs-lookup"><span data-stu-id="694ee-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="694ee-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="694ee-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="694ee-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="694ee-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="694ee-106">La configurazione di connessioni coesistenti di tipo VPN da sito a sito ed ExpressRoute offre diversi vantaggi.</span><span class="sxs-lookup"><span data-stu-id="694ee-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="694ee-107">È possibile configurare una VPN da sito a sito come un percorso di failover sicura per ExressRoute o usare una VPN Site-to-Site tooconnect toosites che non sono connessi tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="694ee-108">Viene illustrata l'hello passaggi tooconfigure entrambi gli scenari in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="694ee-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="694ee-109">In questo articolo si applica al modello di distribuzione di gestione delle risorse toohello e utilizza PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694ee-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="694ee-110">Questa configurazione non è disponibile nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="694ee-111">Circuiti ExpressRoute devono essere pre-configurati prima di seguire le istruzioni di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="694ee-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="694ee-112">Assicurarsi di aver seguito le guide di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [configurare il routing](expressroute-howto-routing-arm.md) prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="694ee-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="694ee-113">Limiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="694ee-113">Limits and limitations</span></span>
* <span data-ttu-id="694ee-114">**L'instradamento del transito non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="694ee-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="694ee-115">Con Azure non è possibile attivare il routing tra la rete locale connessa tramite la VPN da sito a sito e la rete locale connessa tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="694ee-116">**Il gateway SKU Basic non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="694ee-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="694ee-117">È necessario utilizzare un gateway non base SKU per entrambi hello [gateway ExpressRoute](expressroute-about-virtual-network-gateways.md) hello e [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="694ee-118">**È supportato solo il gateway VPN basato su route.**</span><span class="sxs-lookup"><span data-stu-id="694ee-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="694ee-119">È necessario usare un [gateway VPN basato su route](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="694ee-120">**Deve essere configurata una route statica per il gateway VPN.**</span><span class="sxs-lookup"><span data-stu-id="694ee-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="694ee-121">Se la rete locale è connesso tooboth ExpressRoute e una Site-to-Site VPN, è necessario disporre una route statica configurata nel toohello di connessione di rete locale tooroute hello Site-to-Site VPN rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="694ee-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="694ee-122">**Gateway ExpressRoute devono essere configurate per prime e collegati tooa circuito.**</span><span class="sxs-lookup"><span data-stu-id="694ee-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="694ee-123">È necessario creare innanzitutto gateway ExpressRoute hello e collegamento circuito tooa prima di aggiungere gateway VPN Site-to-Site hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="694ee-124">Progetti di configurazione</span><span class="sxs-lookup"><span data-stu-id="694ee-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="694ee-125">Configurare una VPN da sito a sito come percorso di failover per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="694ee-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="694ee-126">È possibile configurare una connessione VPN da sito a sito come backup per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="694ee-127">Si applica solo toovirtual reti collegate toohello Azure percorso di peering privato.</span><span class="sxs-lookup"><span data-stu-id="694ee-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="694ee-128">Non esiste alcuna soluzione di failover basato su VPN per i servizi accessibili tramite i peering pubblico di Azure e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="694ee-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="694ee-129">Hello circuito ExpressRoute è sempre collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="694ee-130">I dati passano attraverso il percorso VPN Site-to-Site hello solo se hello circuito ExpressRoute ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="694ee-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="694ee-131">Mentre il circuito ExpressRoute è preferito tramite VPN Site-to-Site quando entrambe le route sono hello stesso, Azure utilizzerà hello più lunga prefisso corrispondenza toochoose hello route verso la destinazione del pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coesistenza](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="694ee-133">Configurare un toosites tooconnect VPN da sito a sito non è connesso tramite ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="694ee-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="694ee-134">È possibile configurare la rete in cui alcuni siti si connettono direttamente tooAzure tramite VPN Site-to-Site e alcuni siti si connettono tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coesistenza](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="694ee-136">Non è possibile configurare una rete virtuale come router di transito.</span><span class="sxs-lookup"><span data-stu-id="694ee-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="694ee-137">Selezione di hello passaggi toouse</span><span class="sxs-lookup"><span data-stu-id="694ee-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="694ee-138">Esistono due diversi set di procedure toochoose da.</span><span class="sxs-lookup"><span data-stu-id="694ee-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="694ee-139">procedura di configurazione di Hello selezionato dipende se si dispone di una rete virtuale esistente che si desidera tooconnect a o si desidera toocreate una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="694ee-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="694ee-140">Non dispone di una rete virtuale e necessario toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="694ee-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="694ee-141">Se non è disponibile una rete virtuale, questa procedura consente la creazione di una nuova rete virtuale e di nuove connessioni ExpressRoute e VPN da sito a sito usando il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="694ee-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="694ee-142">tooconfigure una rete virtuale, seguire i passaggi hello [toocreate una nuova rete virtuale e le connessioni coesistenti](#new).</span><span class="sxs-lookup"><span data-stu-id="694ee-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="694ee-143">È già disponibile una rete virtuale con modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="694ee-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="694ee-144">E’ possibile che esista già una rete virtuale con una connessione VPN da sito a sito o una connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="694ee-145">Hello [tooconfigure connessioni coesistenti per una rete virtuale di già esistente](#add) sezione disponibili informazioni dettagliate sull'eliminazione del gateway hello e quindi la creazione di nuove connessioni di VPN Site-to-Site ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="694ee-146">Quando si creano hello nuove connessioni, è necessario completare i passaggi di hello in un ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="694ee-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="694ee-147">Non utilizzare istruzioni hello toocreate altri articoli del gateway e connessioni.</span><span class="sxs-lookup"><span data-stu-id="694ee-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="694ee-148">In questa procedura, la creazione di connessioni che possono coesistere richiede toodelete è il gateway e quindi configurare nuovi gateway.</span><span class="sxs-lookup"><span data-stu-id="694ee-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="694ee-149">È tempo di inattività per le connessioni cross-premise mentre eliminare e ricreare il gateway e connessioni, ma non è necessario toomigrate le macchine virtuali o servizi tooa nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="694ee-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="694ee-150">Le macchine virtuali e servizi sarà comunque in grado di toocommunicate out tramite bilanciamento del carico hello durante la configurazione del gateway se sono pertanto toodo configurato.</span><span class="sxs-lookup"><span data-stu-id="694ee-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="694ee-151"><a name="new"></a>connessioni coesistenti e toocreate una nuova rete virtuale</span><span class="sxs-lookup"><span data-stu-id="694ee-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="694ee-152">Questa procedura illustra come creare una rete virtuale e connessioni da sito a sito ed ExpressRoute coesistenti.</span><span class="sxs-lookup"><span data-stu-id="694ee-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="694ee-153">Installare hello l'ultima versione di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694ee-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="694ee-154">Per informazioni sull'installazione hello cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="694ee-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="694ee-155">Hello cmdlet da utilizzare per questa configurazione potrebbe essere leggermente diverso rispetto a ciò che potrebbe acquisire familiarità con.</span><span class="sxs-lookup"><span data-stu-id="694ee-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="694ee-156">I cmdlet di hello toouse che è possibile specificare in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="694ee-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="694ee-157">Accedi tooyour account e configurare un ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="694ee-158">Creare una rete virtuale con una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="694ee-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="694ee-159">Per ulteriori informazioni sulla configurazione di rete virtuale hello, vedere [configurazione di rete virtuale di Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="694ee-160">Hello Subnet del Gateway deve essere /27 o un prefisso (ad esempio /26 o /25) più breve.</span><span class="sxs-lookup"><span data-stu-id="694ee-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="694ee-161">Creare una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="694ee-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="694ee-162">Aggiungere le subnet.</span><span class="sxs-lookup"><span data-stu-id="694ee-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="694ee-163">Salvare la configurazione di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="694ee-164"><a name="gw"></a>Creare un gateway ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="694ee-165">Per ulteriori informazioni sulla configurazione di gateway ExpressRoute hello, vedere [configurazione del gateway ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="694ee-166">Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="694ee-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="694ee-167">Collegare il circuito ExpressRoute toohello di hello ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="694ee-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="694ee-168">Dopo questo passaggio è stato completato, viene stabilita connessione hello tra la rete locale e Azure tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="694ee-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="694ee-169">Per ulteriori informazioni sull'operazione di collegamento hello, vedere [tooExpressRoute reti virtuali collegamento](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="694ee-170"><a name="vpngw"></a>Creare quindi il gateway VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="694ee-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="694ee-171">Per ulteriori informazioni sulla configurazione del gateway VPN hello, vedere [configurare una rete virtuale con una connessione Site-to-Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="694ee-172">Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="694ee-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="694ee-173">necessario Hello VpnType *tipo RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="694ee-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="694ee-174">Il gateway VPN di Azure supporta il protocollo di routing BGP.</span><span class="sxs-lookup"><span data-stu-id="694ee-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="694ee-175">È possibile specificare ASN (numero AS) per la rete virtuale tramite l'aggiunta di switch - Asn hello in hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="694ee-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="694ee-176">Non specificare questo parametro verrà tooAS predefinito numero 65515.</span><span class="sxs-lookup"><span data-stu-id="694ee-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="694ee-177">È possibile trovare hello IP peer BGP e hello sotto forma di numero utilizzato da Azure per il gateway VPN hello in $azureVpn.BgpSettings.BgpPeeringAddress e $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="694ee-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="694ee-178">Per altre informazioni, vedere [Configurare BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) per il gateway VPN di VPN.</span><span class="sxs-lookup"><span data-stu-id="694ee-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="694ee-179">Creare un'entità gateway VPN del sito locale.</span><span class="sxs-lookup"><span data-stu-id="694ee-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="694ee-180">Questo comando non configura il gateway VPN locale.</span><span class="sxs-lookup"><span data-stu-id="694ee-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="694ee-181">Invece, consente di impostazioni del gateway locale hello tooprovide, ad esempio indirizzo IP pubblico hello e hello locale lo spazio degli indirizzi, in modo che hello gateway VPN di Azure può connettersi tooit.</span><span class="sxs-lookup"><span data-stu-id="694ee-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="694ee-182">Se il dispositivo VPN locale supporta solo il routing statico, è possibile configurare le route statiche hello in hello seguente modo:</span><span class="sxs-lookup"><span data-stu-id="694ee-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="694ee-183">Se il dispositivo VPN locale supporta hello BGP e si desidera tooenable il routing dinamico, è necessario tooknow hello BGP peering IP e hello come numero la VPN locale dispositivo usa.</span><span class="sxs-lookup"><span data-stu-id="694ee-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="694ee-184">Configurare il gateway VPN locale dispositivo tooconnect toohello nuovo VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="694ee-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="694ee-185">Per altre informazioni sulla configurazione del dispositivo VPN, vedere l'articolo relativo alla [configurazione del dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="694ee-186">Collegamento hello Site-to-Site VPN gateway in gateway locale toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="694ee-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="694ee-187"><a name="add"></a>connessioni coesistenti tooconfigure per una rete virtuale di già esistente</span><span class="sxs-lookup"><span data-stu-id="694ee-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="694ee-188">Se si dispone di una rete virtuale esistente, è possibile controllare la dimensione della subnet gateway hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="694ee-189">Se subnet del gateway hello /28 o /29, è necessario eliminare il gateway di rete virtuale hello e aumentare la dimensione della subnet gateway hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="694ee-190">Hello passaggi in questa sezione viene illustrato come toodo che.</span><span class="sxs-lookup"><span data-stu-id="694ee-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="694ee-191">Se subnet del gateway hello è /27 o superiore e la rete virtuale hello è connesso tramite ExpressRoute, è possibile ignorare i passaggi di hello riportati di seguito e andare troppo["Passaggio 6: creare un gateway VPN da sito a sito"](#vpngw) nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="694ee-192">Quando si elimina gateway esistente hello, sedi locali perderà rete virtuale tooyour hello mentre si lavora in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="694ee-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="694ee-193">È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694ee-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="694ee-194">Per ulteriori informazioni sull'installazione di cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="694ee-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="694ee-195">Hello cmdlet da utilizzare per questa configurazione potrebbe essere leggermente diverso rispetto a ciò che potrebbe acquisire familiarità con.</span><span class="sxs-lookup"><span data-stu-id="694ee-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="694ee-196">I cmdlet di hello toouse che è possibile specificare in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="694ee-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="694ee-197">Eliminare il gateway ExpressRoute o VPN da sito a sito esistente hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="694ee-198">Eliminare la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="694ee-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="694ee-199">Aggiungere una subnet del gateway di /27 o superiore.</span><span class="sxs-lookup"><span data-stu-id="694ee-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="694ee-200">Se non si dispone di indirizzi IP sufficiente la dimensione di subnet gateway di rete virtuale tooincrease hello a sinistra, è necessario tooadd più spazio di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="694ee-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="694ee-201">Salvare la configurazione di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="694ee-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="694ee-202">A questo punto, si ha una rete virtuale senza gateway.</span><span class="sxs-lookup"><span data-stu-id="694ee-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="694ee-203">toocreate nuovi gateway e completare le connessioni, è possibile procedere con [passaggio 4: creare un gateway ExpressRoute](#gw), trovato in hello precedente set di passaggi.</span><span class="sxs-lookup"><span data-stu-id="694ee-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="694ee-204">gateway VPN di tooadd configurazione point-to-site toohello</span><span class="sxs-lookup"><span data-stu-id="694ee-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="694ee-205">È possibile eseguire operazioni di hello seguenti gateway VPN di tooyour tooadd Point-to-Site configurazione in una configurazione di coesistenza.</span><span class="sxs-lookup"><span data-stu-id="694ee-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="694ee-206">Aggiungere un pool di indirizzi client VPN.</span><span class="sxs-lookup"><span data-stu-id="694ee-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="694ee-207">Caricare hello tooAzure certificato radice VPN del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="694ee-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="694ee-208">In questo esempio si presuppone che il certificato radice hello viene archiviato nel computer locale di hello in cui viene eseguito hello seguendo i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694ee-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="694ee-209">Per altre informazioni sulle VPN da punto a sito, vedere [Configurare una connessione da punto a sito](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="694ee-210">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="694ee-210">Next steps</span></span>
<span data-ttu-id="694ee-211">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="694ee-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
