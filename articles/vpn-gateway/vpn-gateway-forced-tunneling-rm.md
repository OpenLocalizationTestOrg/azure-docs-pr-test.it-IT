---
title: 'Configurare il tunneling forzato per connessioni di Azure da sito a sito: Resource Manager | Microsoft Docs'
description: Come tooredirect o 'force' tutti tooyour di sfondo del traffico associato a Internet posizione locale.
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
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="afe72-103">Configurare il tunneling forzato con modello di distribuzione Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="afe72-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="afe72-104">Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato.</span><span class="sxs-lookup"><span data-stu-id="afe72-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="afe72-105">Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali.</span><span class="sxs-lookup"><span data-stu-id="afe72-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="afe72-106">Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure sempre attraversa dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit.</span><span class="sxs-lookup"><span data-stu-id="afe72-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="afe72-107">Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="afe72-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="afe72-108">In questo articolo illustra la configurazione forzato tunneling per le reti virtuali create con modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="afe72-109">Il tunneling forzato può essere configurato tramite PowerShell, non tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="afe72-110">Se si desidera tooconfigure tunneling per il modello di distribuzione classica hello forzato, è possibile selezionare articolo classico da hello segue l'elenco a discesa:</span><span class="sxs-lookup"><span data-stu-id="afe72-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="afe72-111">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="afe72-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="afe72-112">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="afe72-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="afe72-113">Informazioni sul tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="afe72-113">About forced tunneling</span></span>

<span data-ttu-id="afe72-114">Hello seguente diagramma illustra il funzionamento del tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="afe72-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Tunneling forzato](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="afe72-116">Nell'esempio riportato sopra, hello hello tunneled front-end subnet non è forzato.</span><span class="sxs-lookup"><span data-stu-id="afe72-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="afe72-117">i carichi di lavoro Hello nella subnet front-end hello continuare tooaccept e rispondere toocustomer richieste da hello Internet direttamente.</span><span class="sxs-lookup"><span data-stu-id="afe72-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="afe72-118">Hello subnet di livello intermedio e back-end devono essere forzate tunnel.</span><span class="sxs-lookup"><span data-stu-id="afe72-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="afe72-119">Tutte le connessioni in uscita da tali toohello due subnet Internet sarà tooan forzata o reindirizzato nuovamente nel sito locale tramite uno dei tunnel VPN S2S hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="afe72-120">Questo consente toorestrict e controllare l'accesso a Internet dalle macchine virtuali o nel cloud servizi in Azure, continuando tooenable l'architettura del servizio a più livelli necessaria.</span><span class="sxs-lookup"><span data-stu-id="afe72-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="afe72-121">Se sono non presenti carichi di lavoro con connessione Internet nelle reti virtuali, è possibile applicare forzato tunneling toohello intere reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="afe72-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="afe72-122">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="afe72-122">Requirements and considerations</span></span>

<span data-ttu-id="afe72-123">Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="afe72-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="afe72-124">Reindirizzamento del traffico tooan locale sito viene espresso come un gateway VPN di Azure toohello di Route predefinita.</span><span class="sxs-lookup"><span data-stu-id="afe72-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="afe72-125">Per altre informazioni sulle route definite dall'utente e sulle reti virtuali, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afe72-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="afe72-126">Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata.</span><span class="sxs-lookup"><span data-stu-id="afe72-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="afe72-127">tabella di routing sistema Hello è hello seguenti tre gruppi di route:</span><span class="sxs-lookup"><span data-stu-id="afe72-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="afe72-128">**Route di rete virtuale locale:** direttamente toohello destinazione macchine virtuali in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="afe72-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="afe72-129">**Le route locali:** gateway VPN di Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="afe72-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="afe72-130">**Route predefinita:** direttamente toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="afe72-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="afe72-131">I pacchetti destinati toohello gli indirizzi IP privati non coperti da route hello due precedenti vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="afe72-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="afe72-132">Questa procedura utilizza le route definite dall'utente (UDR) toocreate un tooadd tabella di routing una route predefinita e quindi associare hello routing tabella tooyour rete virtuale subnet tooenable forzato tunneling su queste subnet.</span><span class="sxs-lookup"><span data-stu-id="afe72-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="afe72-133">Il tunneling forzato deve essere associato a una rete virtuale con un gateway VPN basato su route.</span><span class="sxs-lookup"><span data-stu-id="afe72-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="afe72-134">È necessario un sito"predefinito" tooset tra rete virtuale connessa toohello hello cross-premise siti locali.</span><span class="sxs-lookup"><span data-stu-id="afe72-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="afe72-135">Inoltre, hello locale dispositivo VPN deve essere configurato utilizzando 0.0.0.0/0 come selettori di traffico.</span><span class="sxs-lookup"><span data-stu-id="afe72-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="afe72-136">Il tunneling forzato ExpressRoute non viene configurato tramite questo meccanismo, ma è invece abilitato annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering.</span><span class="sxs-lookup"><span data-stu-id="afe72-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="afe72-137">Per ulteriori informazioni, vedere hello [documentazione di ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="afe72-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="afe72-138">Panoramica della configurazione</span><span class="sxs-lookup"><span data-stu-id="afe72-138">Configuration overview</span></span>

<span data-ttu-id="afe72-139">Hello seguente procedura consente di creare un gruppo di risorse e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="afe72-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="afe72-140">Si passerà quindi alla creazione di un gateway VPN e alla configurazione del tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="afe72-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="afe72-141">In questa procedura, dispone di tre subnet rete virtuale hello 'MultiTier-VNet': 'Front-end', 'Midtier' e 'Back-end', con quattro connessioni più sedi: 'DefaultSiteHQ' e tre rami.</span><span class="sxs-lookup"><span data-stu-id="afe72-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="afe72-142">procedura Hello imposta hello 'DefaultSiteHQ' come connessione di hello predefinita del sito per il tunneling forzato e configurare hello 'Midtier' e 'Back-end' subnet toouse il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="afe72-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="afe72-143">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="afe72-143">Before you begin</span></span>

<span data-ttu-id="afe72-144">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="afe72-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="afe72-145">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="afe72-146">toolog in</span><span class="sxs-lookup"><span data-stu-id="afe72-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="afe72-147">È possibile configurare il tunneling forzato?</span><span class="sxs-lookup"><span data-stu-id="afe72-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="afe72-148">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="afe72-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="afe72-149">Creare una rete virtuale e specificare le subnet.</span><span class="sxs-lookup"><span data-stu-id="afe72-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="afe72-150">Creare hello gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="afe72-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="afe72-151">Creare una regola route e di tabella di route hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="afe72-152">Associare hello route tabella toohello Midtier e subnet di back-end.</span><span class="sxs-lookup"><span data-stu-id="afe72-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="afe72-153">Creare hello Gateway con un sito predefinito.</span><span class="sxs-lookup"><span data-stu-id="afe72-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="afe72-154">Questo passaggio accetta alcuni toocomplete tempo, in alcuni casi a 45 minuti o più, perché la creazione e la configurazione di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="afe72-155">Hello **- GatewayDefaultSite** è hello parametro del cmdlet che consente di hello forzato routing toowork di configurazione, fare attenzione tooconfigure questa impostazione in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="afe72-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="afe72-156">Questo parametro è disponibile solo in PowerShell 1.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="afe72-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="afe72-157">Stabilire le connessioni VPN da sito a sito hello.</span><span class="sxs-lookup"><span data-stu-id="afe72-157">Establish hello Site-to-Site VPN connections.</span></span>

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