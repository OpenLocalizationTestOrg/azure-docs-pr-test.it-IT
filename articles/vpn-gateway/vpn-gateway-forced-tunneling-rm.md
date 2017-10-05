---
title: 'Configurare il tunneling forzato per connessioni di Azure da sito a sito: Resource Manager | Microsoft Docs'
description: Come reindirizzare o forzare tutto il traffico associato a Internet verso il percorso locale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="6e486-103">Configurare il tunneling forzato tramite il modello di distribuzione Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e486-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="6e486-104">Il tunneling forzato consente di reindirizzare o "forzare" tutto il traffico associato a Internet verso la posizione locale tramite un tunnel VPN da sito a sito per l'ispezione e il controllo.</span><span class="sxs-lookup"><span data-stu-id="6e486-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="6e486-105">Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali.</span><span class="sxs-lookup"><span data-stu-id="6e486-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="6e486-106">Senza il tunneling forzato, il traffico verso Internet dalle macchine virtuali in Azure raggiunge sempre direttamente Internet attraversando l'infrastruttura di rete di Azure, senza che si possa analizzare o controllare il traffico.</span><span class="sxs-lookup"><span data-stu-id="6e486-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="6e486-107">L'accesso a Internet non autorizzato potrebbe provocare la divulgazione di informazioni o altri tipi di violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6e486-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="6e486-108">Questo articolo illustra la configurazione del tunneling forzato per le reti virtuali create usando il modello di distribuzione di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="6e486-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="6e486-109">Il tunneling forzato può essere configurato tramite PowerShell e non tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="6e486-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="6e486-110">Se si intende configurare il tunneling forzato per il modello di distribuzione classica, selezionare l'articolo relativo alla distribuzione classica nell'elenco a discesa seguente:</span><span class="sxs-lookup"><span data-stu-id="6e486-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e486-111">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="6e486-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="6e486-112">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="6e486-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="6e486-113">Informazioni sul tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="6e486-113">About forced tunneling</span></span>

<span data-ttu-id="6e486-114">Nel diagramma seguente viene illustrato il funzionamento del tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="6e486-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Tunneling forzato](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="6e486-116">Nell'esempio riportato in precedenza, il tunneling della subnet front-end non viene forzato.</span><span class="sxs-lookup"><span data-stu-id="6e486-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="6e486-117">I carichi di lavoro nella subnet front-end possono continuare ad accettare e a rispondere alle richieste dei clienti direttamente da Internet.</span><span class="sxs-lookup"><span data-stu-id="6e486-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="6e486-118">Il tunneling delle subnet di livello intermedio e back-end viene forzato.</span><span class="sxs-lookup"><span data-stu-id="6e486-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="6e486-119">Tutte le connessioni in uscita da queste due subnet a Internet verranno forzate o reindirizzate verso un sito locale tramite uno dei tunnel VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="6e486-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="6e486-120">Ciò consente di limitare e ispezionare l'accesso a Internet dalle macchine virtuali o dai servizi cloud in Azure, pur continuando ad abilitare l'architettura dei servizi multilivello richiesta.</span><span class="sxs-lookup"><span data-stu-id="6e486-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="6e486-121">È anche possibile applicare il tunneling forzato a tutte le reti virtuali se non sono presenti carichi di lavoro con connessione Internet nelle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6e486-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="6e486-122">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="6e486-122">Requirements and considerations</span></span>

<span data-ttu-id="6e486-123">Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6e486-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="6e486-124">Il reindirizzamento del traffico a un sito locale viene espresso come route predefinita al gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e486-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="6e486-125">Per altre informazioni sulle route definite dall'utente e sulle reti virtuali, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e486-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="6e486-126">Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata.</span><span class="sxs-lookup"><span data-stu-id="6e486-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="6e486-127">La tabella di routing di sistema include i tre gruppi di route seguenti:</span><span class="sxs-lookup"><span data-stu-id="6e486-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="6e486-128">**Route della rete virtuale locale:** direttamente alle macchine virtuali di destinazione nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e486-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="6e486-129">**Route locali:** al gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e486-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="6e486-130">**Route predefinita:** direttamente a Internet.</span><span class="sxs-lookup"><span data-stu-id="6e486-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="6e486-131">I pacchetti destinati agli indirizzi IP privati che non rientrano nelle due route precedenti vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="6e486-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="6e486-132">Questa procedura usa le route definite dall'utente per creare una tabella di routing per aggiungere una route predefinita, quindi associare la tabella di routing alle subnet della rete virtuale per abilitare il tunneling forzato in tali subnet.</span><span class="sxs-lookup"><span data-stu-id="6e486-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="6e486-133">Il tunneling forzato deve essere associato a una rete virtuale con un gateway VPN basato su route.</span><span class="sxs-lookup"><span data-stu-id="6e486-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="6e486-134">È necessario impostare un "sito predefinito" tra i siti locali cross-premise connessi alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e486-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="6e486-135">È anche necessario configurare il dispositivo VPN locale usando 0.0.0.0/0 come selettori di traffico.</span><span class="sxs-lookup"><span data-stu-id="6e486-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="6e486-136">Il tunneling forzato ExpressRoute non viene configurato mediante questo meccanismo, ma è abilitato annunciando una route predefinita tramite le sessioni di peering BGP ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6e486-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="6e486-137">Per altre informazioni, vedere la [Documentazione su ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="6e486-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="6e486-138">Panoramica della configurazione</span><span class="sxs-lookup"><span data-stu-id="6e486-138">Configuration overview</span></span>

<span data-ttu-id="6e486-139">La procedura seguente consente di creare un gruppo di risorse e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e486-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="6e486-140">Si passerà quindi alla creazione di un gateway VPN e alla configurazione del tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="6e486-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="6e486-141">In questa procedura, la rete virtuale 'MultiTier-VNet' include tre subnet: 'Frontend', 'Midtier' e 'Backend' con quattro connessioni cross-premise: 'DefaultSiteHQ' e tre rami.</span><span class="sxs-lookup"><span data-stu-id="6e486-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="6e486-142">La procedura illustrata consente di impostare 'DefaultSiteHQ' come connessione predefinita del sito per il tunneling forzato e di configurare le subnet 'Midtier' e 'Backend' per l'uso del tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="6e486-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6e486-143">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6e486-143">Before you begin</span></span>

<span data-ttu-id="6e486-144">Installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e486-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6e486-145">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="6e486-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="6e486-146">Per accedere</span><span class="sxs-lookup"><span data-stu-id="6e486-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="6e486-147">È possibile configurare il tunneling forzato?</span><span class="sxs-lookup"><span data-stu-id="6e486-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="6e486-148">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6e486-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="6e486-149">Creare una rete virtuale e specificare le subnet.</span><span class="sxs-lookup"><span data-stu-id="6e486-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="6e486-150">Creare i gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="6e486-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="6e486-151">Creare la tabella di route e la regola di route.</span><span class="sxs-lookup"><span data-stu-id="6e486-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="6e486-152">Associare la tabella di route alle subnet Midtier e Backend.</span><span class="sxs-lookup"><span data-stu-id="6e486-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="6e486-153">Creare il gateway con un sito predefinito.</span><span class="sxs-lookup"><span data-stu-id="6e486-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="6e486-154">Questa procedura può richiedere 45 minuti o più perché include le operazioni di creazione e configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="6e486-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="6e486-155">**-GatewayDefaultSite** è il parametro di cmdlet che consente il funzionamento della configurazione del routing forzata. Assicurarsi pertanto di configurare questa impostazione in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="6e486-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="6e486-156">Questo parametro è disponibile solo in PowerShell 1.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6e486-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="6e486-157">Stabilire le connessioni VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="6e486-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```