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
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="32c03-103">Informazioni sulle impostazioni di configurazione del gateway VPN</span><span class="sxs-lookup"><span data-stu-id="32c03-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="32c03-104">Un gateway VPN è un tipo di gateway di rete virtuale che invia traffico crittografato tra la rete virtuale e la posizione locale tramite una connessione pubblica.</span><span class="sxs-lookup"><span data-stu-id="32c03-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="32c03-105">È anche possibile utilizzare un traffico di toosend VPN gateway tra reti virtuali in hello backbone di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c03-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="32c03-106">Una connessione gateway VPN si basa sulla configurazione di hello di più risorse, ognuno dei quali contiene le impostazioni configurabili.</span><span class="sxs-lookup"><span data-stu-id="32c03-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="32c03-107">Nelle sezioni di Hello in questo articolo viene hello risorse e impostazioni correlate al gateway VPN tooa per una rete virtuale creata nel modello di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="32c03-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="32c03-108">È possibile trovare le descrizioni e i diagrammi di topologia per ogni soluzione di connessione in hello [sul Gateway VPN](vpn-gateway-about-vpngateways.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="32c03-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="32c03-109"><a name="gwtype"></a>Tipi di gateway</span><span class="sxs-lookup"><span data-stu-id="32c03-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="32c03-110">Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo.</span><span class="sxs-lookup"><span data-stu-id="32c03-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="32c03-111">Quando si crea un gateway di rete virtuale, è necessario assicurarsi che il tipo di gateway hello sia corretto per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="32c03-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="32c03-112">i valori disponibili per il tipo di gateway - Hello sono:</span><span class="sxs-lookup"><span data-stu-id="32c03-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="32c03-113">VPN</span><span class="sxs-lookup"><span data-stu-id="32c03-113">Vpn</span></span>
* <span data-ttu-id="32c03-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="32c03-114">ExpressRoute</span></span>

<span data-ttu-id="32c03-115">Un gateway VPN richiede hello `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="32c03-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="32c03-116">Esempio:</span><span class="sxs-lookup"><span data-stu-id="32c03-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="32c03-117"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="32c03-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="32c03-118">Configurare il gateway di hello SKU</span><span class="sxs-lookup"><span data-stu-id="32c03-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="32c03-119">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="32c03-119">Azure portal</span></span>

<span data-ttu-id="32c03-120">Se si utilizza hello toocreate portale Azure un gateway di rete virtuale di gestione delle risorse, è possibile selezionare lo SKU del gateway hello utilizzando l'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="32c03-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="32c03-121">vengono visualizzate le opzioni di Hello corrispondono toohello tipo di Gateway e il tipo VPN selezionato.</span><span class="sxs-lookup"><span data-stu-id="32c03-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="32c03-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c03-122">PowerShell</span></span>

<span data-ttu-id="32c03-123">esempio di PowerShell seguente Hello specifica hello `-GatewaySku` come VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="32c03-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="32c03-124"><a name="resize"></a>Modificare (ridimensionare) uno SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="32c03-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="32c03-125">Se si desidera tooupgrade tooa SKU del gateway SKU più potente, è possibile utilizzare hello `Resize-AzureRmVirtualNetworkGateway` cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c03-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="32c03-126">È anche possibile effettuare il downgrade di dimensioni SKU di gateway hello utilizzando questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32c03-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="32c03-127">Hello esempio PowerShell seguente viene illustrato che un gateway SKU ridimensionata tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="32c03-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="32c03-128"><a name="connectiontype"></a>Tipi di connessione</span><span class="sxs-lookup"><span data-stu-id="32c03-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="32c03-129">Nel modello di distribuzione di gestione risorse hello, ogni configurazione richiede un tipo di connessione di gateway di rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="32c03-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="32c03-130">Hello PowerShell di gestione risorse disponibili i valori del parametro `-ConnectionType` sono:</span><span class="sxs-lookup"><span data-stu-id="32c03-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="32c03-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="32c03-131">IPsec</span></span>
* <span data-ttu-id="32c03-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="32c03-132">Vnet2Vnet</span></span>
* <span data-ttu-id="32c03-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="32c03-133">ExpressRoute</span></span>
* <span data-ttu-id="32c03-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="32c03-134">VPNClient</span></span>

<span data-ttu-id="32c03-135">Nel seguente esempio di PowerShell di hello, verrà creata una connessione di S2S che richiede il tipo di connessione hello *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="32c03-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="32c03-136"><a name="vpntype"></a>Tipi di VPN</span><span class="sxs-lookup"><span data-stu-id="32c03-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="32c03-137">Quando si crea il gateway di rete virtuale hello per una configurazione di gateway VPN, è necessario specificare un tipo di VPN.</span><span class="sxs-lookup"><span data-stu-id="32c03-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="32c03-138">tipo VPN che si sceglie di Hello dipende dalla topologia di connessione hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="32c03-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="32c03-139">Ad esempio, una connessione P2S richiede un tipo di VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="32c03-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="32c03-140">Un tipo di VPN può dipendere anche da hardware hello che si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="32c03-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="32c03-141">Le configurazioni S2S richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="32c03-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="32c03-142">Alcuni dispositivi VPN supportano solo un determinato tipo di VPN.</span><span class="sxs-lookup"><span data-stu-id="32c03-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="32c03-143">Hello tipo VPN selezionato deve soddisfare tutti i requisiti di connessione hello per soluzione hello desiderato toocreate.</span><span class="sxs-lookup"><span data-stu-id="32c03-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="32c03-144">Ad esempio, se si desidera toocreate una connessione di gateway VPN S2S, un gateway VPN P2S per hello stessa rete virtuale, utilizzare il tipo VPN *tipo RouteBased* perché P2S richiede un tipo RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="32c03-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="32c03-145">È inoltre necessario che il dispositivo VPN è supportata una connessione VPN RouteBased tooverify.</span><span class="sxs-lookup"><span data-stu-id="32c03-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="32c03-146">Dopo aver creato un gateway di rete virtuale, è possibile modificare il tipo VPN hello.</span><span class="sxs-lookup"><span data-stu-id="32c03-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="32c03-147">È possibile toodelete hello gateway di rete virtuale e crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="32c03-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="32c03-148">Sono disponibili due tipi di VPN:</span><span class="sxs-lookup"><span data-stu-id="32c03-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="32c03-149">esempio di PowerShell seguente Hello specifica hello `-VpnType` come *tipo RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="32c03-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="32c03-150">Quando si crea un gateway, è necessario assicurarsi che hello - VpnType sia corretto per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="32c03-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="32c03-151"><a name="requirements"></a>Requisiti del gateway</span><span class="sxs-lookup"><span data-stu-id="32c03-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="32c03-152"><a name="gwsub"></a>Subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="32c03-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="32c03-153">Prima di creare un gateway VPN, è necessario creare una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="32c03-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="32c03-154">subnet del gateway Hello contiene indirizzi IP hello tale gateway di rete virtuale hello macchine virtuali e servizi utilizzano.</span><span class="sxs-lookup"><span data-stu-id="32c03-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="32c03-155">Quando si crea il gateway di rete virtuale, gateway di macchine virtuali sono subnet del gateway toohello distribuito e configurato con impostazioni del gateway VPN hello necessario.</span><span class="sxs-lookup"><span data-stu-id="32c03-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="32c03-156">È non necessario distribuire mai subnet del gateway toohello qualsiasi altra operazione (ad esempio, altre macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="32c03-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="32c03-157">subnet del gateway Hello devono essere denominate 'GatewaySubnet' toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="32c03-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="32c03-158">Denominazione subnet del gateway hello consente 'GatewaySubnet' Azure sapere che si è gateway di rete virtuale hello toodeploy subnet hello macchine virtuali e servizi.</span><span class="sxs-lookup"><span data-stu-id="32c03-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="32c03-159">Quando si crea una subnet del gateway hello, specificare il numero di indirizzi IP che hello subnet hello contiene.</span><span class="sxs-lookup"><span data-stu-id="32c03-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="32c03-160">gli indirizzi IP di Hello nella subnet del gateway hello sono allocati toohello macchine virtuali del gateway e il servizio gateway.</span><span class="sxs-lookup"><span data-stu-id="32c03-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="32c03-161">Alcune configurazioni richiedono più indirizzi IP di altre.</span><span class="sxs-lookup"><span data-stu-id="32c03-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="32c03-162">Esaminare le istruzioni di hello per configurazione hello toocreate desiderato e verificare che la subnet gateway hello desiderato toocreate soddisfi tali requisiti.</span><span class="sxs-lookup"><span data-stu-id="32c03-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="32c03-163">Inoltre, si consiglia di toomake che la subnet gateway contenga sufficiente IP indirizzi tooaccommodate future ulteriori configurazioni possibili.</span><span class="sxs-lookup"><span data-stu-id="32c03-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="32c03-164">Anche se è possibile creare una subnet del gateway con dimensioni pari a /29, è consigliabile crearne una con dimensioni pari a /28 o superiori, ad esempio /28, /27, /26 e così via.</span><span class="sxs-lookup"><span data-stu-id="32c03-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="32c03-165">In questo modo, se si aggiunge una funzionalità in futuro, hello non hanno tootear il gateway, quindi eliminare e ricreare hello gateway subnet tooallow per più indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="32c03-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="32c03-166">Hello Gestione risorse di PowerShell riportato di seguito una subnet del gateway denominata GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="32c03-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="32c03-167">È possibile visualizzare la notazione CIDR hello specifica un /27, che consente agli indirizzi IP sufficienti per la maggior parte delle configurazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="32c03-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="32c03-168"><a name="lng"></a>Gateway di rete locali</span><span class="sxs-lookup"><span data-stu-id="32c03-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="32c03-169">Quando si crea una configurazione di gateway VPN, il gateway di rete locale hello rappresenta spesso il percorso locale.</span><span class="sxs-lookup"><span data-stu-id="32c03-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="32c03-170">Nel modello di distribuzione classica hello, gateway di rete locale hello è tooas di cui si fa riferimento un sito locale.</span><span class="sxs-lookup"><span data-stu-id="32c03-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="32c03-171">Assegnare un nome di gateway di rete locale hello, indirizzo IP pubblico del dispositivo VPN locale di hello hello e specificare i prefissi di indirizzo hello che si trovano nel percorso locale hello.</span><span class="sxs-lookup"><span data-stu-id="32c03-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="32c03-172">Azure esamina i prefissi di indirizzo di destinazione hello il traffico di rete, consulta configurazione hello specificate per il gateway di rete locale e indirizza i pacchetti di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="32c03-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="32c03-173">È anche possibile specificare i gateway di rete locale per le configurazioni da rete virtuale a rete virtuale che usano una connessione di gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="32c03-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="32c03-174">esempio di PowerShell seguente Hello crea un nuovo gateway di rete locale:</span><span class="sxs-lookup"><span data-stu-id="32c03-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="32c03-175">Talvolta è necessario impostazioni del gateway di rete locale hello toomodify.</span><span class="sxs-lookup"><span data-stu-id="32c03-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="32c03-176">Ad esempio, quando si aggiunge o Modifica intervallo di indirizzi hello o se cambia indirizzo IP di hello del dispositivo VPN hello.</span><span class="sxs-lookup"><span data-stu-id="32c03-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="32c03-177">Per una rete virtuale classica, è possibile modificare queste impostazioni nel portale classico di hello nella pagina reti locali hello.</span><span class="sxs-lookup"><span data-stu-id="32c03-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="32c03-178">Per Resource Manager, vedere [Modificare le impostazioni del gateway di rete locale usando PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="32c03-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="32c03-179"><a name="resources"></a>API REST e cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c03-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="32c03-180">Per ulteriori risorse tecniche e requisiti di sintassi specifica per l'utilizzo di CLI di Azure, i cmdlet di PowerShell o le API REST per le configurazioni del Gateway VPN, vedere hello seguenti pagine:</span><span class="sxs-lookup"><span data-stu-id="32c03-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="32c03-181">**Classico**</span><span class="sxs-lookup"><span data-stu-id="32c03-181">**Classic**</span></span> | <span data-ttu-id="32c03-182">**Gestione risorse**</span><span class="sxs-lookup"><span data-stu-id="32c03-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="32c03-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c03-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="32c03-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c03-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="32c03-185">API REST</span><span class="sxs-lookup"><span data-stu-id="32c03-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="32c03-186">API REST</span><span class="sxs-lookup"><span data-stu-id="32c03-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="32c03-187">Non supportate</span><span class="sxs-lookup"><span data-stu-id="32c03-187">Not supported</span></span> | [<span data-ttu-id="32c03-188">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="32c03-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="32c03-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32c03-189">Next steps</span></span>

<span data-ttu-id="32c03-190">Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="32c03-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>