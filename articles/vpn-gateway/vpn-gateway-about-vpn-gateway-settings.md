---
title: Impostazioni del gateway VPN per connessioni di Azure cross-premise | Documentazione Microsoft
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
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="fda3f-103">Informazioni sulle impostazioni di configurazione del gateway VPN</span><span class="sxs-lookup"><span data-stu-id="fda3f-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="fda3f-104">Un gateway VPN è un tipo di gateway di rete virtuale che invia traffico crittografato tra la rete virtuale e la posizione locale tramite una connessione pubblica.</span><span class="sxs-lookup"><span data-stu-id="fda3f-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="fda3f-105">È possibile usare un gateway VPN anche per inviare il traffico tra reti virtuali attraverso il backbone di Azure.</span><span class="sxs-lookup"><span data-stu-id="fda3f-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="fda3f-106">Una connessione di gateway VPN si basa sulla configurazione di più risorse, ognuna delle quali contiene impostazioni configurabili.</span><span class="sxs-lookup"><span data-stu-id="fda3f-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="fda3f-107">Le sezioni di questo articolo descrivono le risorse e le impostazioni correlate a un gateway VPN per una rete virtuale creata nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fda3f-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="fda3f-108">Le descrizioni e i diagrammi della topologia per ogni soluzione di connessione sono disponibili nell'articolo [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="fda3f-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="fda3f-109"><a name="gwtype"></a>Tipi di gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="fda3f-110">Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo.</span><span class="sxs-lookup"><span data-stu-id="fda3f-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="fda3f-111">Quando si crea un gateway di rete virtuale, è necessario assicurarsi che il tipo di gateway sia corretto per la configurazione in uso.</span><span class="sxs-lookup"><span data-stu-id="fda3f-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="fda3f-112">I valori disponibili per GatewayType sono:</span><span class="sxs-lookup"><span data-stu-id="fda3f-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="fda3f-113">VPN</span><span class="sxs-lookup"><span data-stu-id="fda3f-113">Vpn</span></span>
* <span data-ttu-id="fda3f-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fda3f-114">ExpressRoute</span></span>

<span data-ttu-id="fda3f-115">Un gateway VPN richiede il valore `-GatewayType` *Vpn* per.</span><span class="sxs-lookup"><span data-stu-id="fda3f-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="fda3f-116">Esempio:</span><span class="sxs-lookup"><span data-stu-id="fda3f-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="fda3f-117"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="fda3f-118">Configurare lo SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="fda3f-119">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fda3f-119">Azure portal</span></span>

<span data-ttu-id="fda3f-120">Se si usa il portale di Azure per creare un gateway di rete virtuale di Resource Manager, è possibile selezionare lo SKU del dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="fda3f-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="fda3f-121">Le opzioni disponibili corrispondono al tipo di gateway e al tipo di VPN selezionati.</span><span class="sxs-lookup"><span data-stu-id="fda3f-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="fda3f-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda3f-122">PowerShell</span></span>

<span data-ttu-id="fda3f-123">L'esempio seguente di PowerShell specifica `-GatewaySku` come VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="fda3f-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="fda3f-124"><a name="resize"></a>Modificare (ridimensionare) uno SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="fda3f-125">Per aggiornare lo SKU del gateway a uno SKU più potente, è possibile usare il cmdlet di PowerShell `Resize-AzureRmVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="fda3f-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="fda3f-126">È anche possibile eseguire il downgrade delle dimensioni dello SKU del gateway usando questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fda3f-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="fda3f-127">L'esempio di PowerShell seguente illustra uno SKU del gateway che viene ridimensionato come VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="fda3f-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="fda3f-128"><a name="connectiontype"></a>Tipi di connessione</span><span class="sxs-lookup"><span data-stu-id="fda3f-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="fda3f-129">Nel modello di distribuzione Resource Manager ogni configurazione richiede un tipo di connessione di gateway di rete virtuale specifico.</span><span class="sxs-lookup"><span data-stu-id="fda3f-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="fda3f-130">I valori di PowerShell per Resource Manager disponibili per `-ConnectionType` sono:</span><span class="sxs-lookup"><span data-stu-id="fda3f-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="fda3f-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="fda3f-131">IPsec</span></span>
* <span data-ttu-id="fda3f-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="fda3f-132">Vnet2Vnet</span></span>
* <span data-ttu-id="fda3f-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fda3f-133">ExpressRoute</span></span>
* <span data-ttu-id="fda3f-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="fda3f-134">VPNClient</span></span>

<span data-ttu-id="fda3f-135">L'esempio PowerShell seguente crea una connessione S2S che richiede il tipo di connessione *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="fda3f-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="fda3f-136"><a name="vpntype"></a>Tipi di VPN</span><span class="sxs-lookup"><span data-stu-id="fda3f-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="fda3f-137">Quando si crea il gateway di rete virtuale per una configurazione di gateway VPN, è necessario specificare un tipo di VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="fda3f-138">Il tipo di VPN scelto dipende dalla topologia di connessione che si desidera creare.</span><span class="sxs-lookup"><span data-stu-id="fda3f-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="fda3f-139">Ad esempio, una connessione P2S richiede un tipo di VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="fda3f-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="fda3f-140">Un tipo di VPN può anche dipendere dall'hardware usato.</span><span class="sxs-lookup"><span data-stu-id="fda3f-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="fda3f-141">Le configurazioni S2S richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="fda3f-142">Alcuni dispositivi VPN supportano solo un determinato tipo di VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="fda3f-143">Il tipo di VPN selezionato deve soddisfare tutti i requisiti di connessione per la soluzione da creare.</span><span class="sxs-lookup"><span data-stu-id="fda3f-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="fda3f-144">Ad esempio, per creare una connessione di gateway VPN S2S, una connessione di gateway VPN P2S sulla stessa rete virtuale, usare il tipo *RouteBased* poiché P2S richiede questo tipo specifico.</span><span class="sxs-lookup"><span data-stu-id="fda3f-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="fda3f-145">È inoltre necessario verificare che il dispositivo VPN supporti una connessione VPN di tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="fda3f-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="fda3f-146">Dopo avere creato un gateway di rete virtuale, non è possibile modificare il tipo di VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="fda3f-147">È necessario eliminare il gateway di rete virtuale e crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="fda3f-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="fda3f-148">Sono disponibili due tipi di VPN:</span><span class="sxs-lookup"><span data-stu-id="fda3f-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="fda3f-149">Nel seguente esempio di PowerShell `-VpnType` viene specificato come *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="fda3f-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="fda3f-150">Quando si crea un gateway, è necessario assicurarsi che -VpnType sia corretto per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="fda3f-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="fda3f-151"><a name="requirements"></a>Requisiti del gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="fda3f-152"><a name="gwsub"></a>Subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="fda3f-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="fda3f-153">Prima di creare un gateway VPN, è necessario creare una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="fda3f-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="fda3f-154">La subnet del gateway contiene gli indirizzi IP usati dalle VM e dai servizi del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="fda3f-155">Quando si crea il gateway di rete virtuale, le VM del gateway vengono distribuite nella subnet del gateway e configurate con le impostazioni del gateway VPN necessarie.</span><span class="sxs-lookup"><span data-stu-id="fda3f-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="fda3f-156">Non si deve mai distribuire altro (ad esempio, VM aggiuntive) nella subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="fda3f-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="fda3f-157">Per poter funzionare correttamente, la subnet del gateway deve essere denominata "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="fda3f-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="fda3f-158">Denominando la subnet del gateway 'GatewaySubnet', Azure riconosce questa subnet come quella in cui distribuire i servizi e le VM del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="fda3f-159">Quando si crea la subnet del gateway, si specifica il numero di indirizzi IP inclusi nella subnet.</span><span class="sxs-lookup"><span data-stu-id="fda3f-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="fda3f-160">Gli indirizzi IP inclusi nella subnet del gateway sono allocati alle VM del gateway e ai servizi del gateway.</span><span class="sxs-lookup"><span data-stu-id="fda3f-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="fda3f-161">Alcune configurazioni richiedono più indirizzi IP di altre.</span><span class="sxs-lookup"><span data-stu-id="fda3f-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="fda3f-162">Esaminare le istruzioni per la configurazione da creare e verificare che la subnet del gateway che si vuole creare soddisfi tali requisiti.</span><span class="sxs-lookup"><span data-stu-id="fda3f-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="fda3f-163">È anche consigliabile verificare che la subnet del gateway contenga una quantità di indirizzi IP sufficiente per supportare possibili future configurazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="fda3f-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="fda3f-164">Anche se è possibile creare una subnet del gateway con dimensioni pari a /29, è consigliabile crearne una con dimensioni pari a /28 o superiori, ad esempio /28, /27, /26 e così via.</span><span class="sxs-lookup"><span data-stu-id="fda3f-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="fda3f-165">In questo modo, se si aggiungono funzionalità in futuro, non sarà necessario rimuovere il gateway ed eliminare e ricreare la subnet del gateway per consentire altri indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="fda3f-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="fda3f-166">L'esempio seguente di PowerShell Resource Manager illustra una subnet del gateway denominata GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="fda3f-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="fda3f-167">La notazione CIDR specifica /27. Questa dimensione ammette un numero di indirizzi IP sufficiente per la maggior parte delle configurazioni attualmente esistenti.</span><span class="sxs-lookup"><span data-stu-id="fda3f-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="fda3f-168"><a name="lng"></a>Gateway di rete locali</span><span class="sxs-lookup"><span data-stu-id="fda3f-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="fda3f-169">Quando si crea una configurazione per il gateway VPN, il gateway di rete locale rappresenta spesso la posizione locale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="fda3f-170">Nel modello di distribuzione classica il gateway di rete locale è definito come sito locale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="fda3f-171">Assegnare un nome e l'indirizzo IP pubblico del dispositivo VPN locale al gateway di rete locale e specificare i prefissi di indirizzo che si trovano nel percorso locale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="fda3f-172">Azure esamina i prefissi di indirizzo di destinazione per il traffico di rete, consulta la configurazione specificata per il gateway di rete locale e indirizza i pacchetti di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="fda3f-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="fda3f-173">È anche possibile specificare i gateway di rete locale per le configurazioni da rete virtuale a rete virtuale che usano una connessione di gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="fda3f-174">L'esempio seguente di PowerShell consente di creare un nuovo gateway di rete locale:</span><span class="sxs-lookup"><span data-stu-id="fda3f-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="fda3f-175">Talvolta è necessario modificare le impostazioni di gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="fda3f-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="fda3f-176">Ad esempio, quando si aggiunge o si modifica l'intervallo di indirizzi oppure se viene modificato l'indirizzo IP del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fda3f-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="fda3f-177">Per una rete virtuale classica, è possibile modificare queste impostazioni nella pagina relativa alle reti locali del portale classico.</span><span class="sxs-lookup"><span data-stu-id="fda3f-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="fda3f-178">Per Resource Manager, vedere [Modificare le impostazioni del gateway di rete locale usando PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="fda3f-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="fda3f-179"><a name="resources"></a>API REST e cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda3f-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="fda3f-180">Per altre risorse tecniche e requisiti di sintassi specifici quando si usano le API REST, i cmdlet PowerShell o l'interfaccia della riga di comando di Azure per le configurazioni di Gateway VPN, vedere le pagine seguenti:</span><span class="sxs-lookup"><span data-stu-id="fda3f-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="fda3f-181">**Classico**</span><span class="sxs-lookup"><span data-stu-id="fda3f-181">**Classic**</span></span> | <span data-ttu-id="fda3f-182">**Gestione risorse**</span><span class="sxs-lookup"><span data-stu-id="fda3f-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="fda3f-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda3f-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="fda3f-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda3f-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="fda3f-185">API REST</span><span class="sxs-lookup"><span data-stu-id="fda3f-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="fda3f-186">API REST</span><span class="sxs-lookup"><span data-stu-id="fda3f-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="fda3f-187">Non supportate</span><span class="sxs-lookup"><span data-stu-id="fda3f-187">Not supported</span></span> | [<span data-ttu-id="fda3f-188">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fda3f-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="fda3f-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fda3f-189">Next steps</span></span>

<span data-ttu-id="fda3f-190">Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="fda3f-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>