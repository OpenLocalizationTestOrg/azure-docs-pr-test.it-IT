---
title: SKU del gateway di rete virtuale di Azure legacy| Microsoft Docs
description: SKU del gateway di rete virtuale precedenti.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="b5f47-103">Utilizzo degli SKU del gateway di rete virtuale (SKU di versione precedente)</span><span class="sxs-lookup"><span data-stu-id="b5f47-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="b5f47-104">Questo articolo contiene informazioni sugli SKU del gateway di rete virtuale (versione precedente).</span><span class="sxs-lookup"><span data-stu-id="b5f47-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="b5f47-105">Gli SKU di versione precedente continuano a funzionare in entrambi i modelli di distribuzione per i gateway VPN che sono già stati creati.</span><span class="sxs-lookup"><span data-stu-id="b5f47-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="b5f47-106">I gateway VPN classici continuano a usare gli SKU di versione precedente, sia per i gateway esistenti sia per i nuovi gateway.</span><span class="sxs-lookup"><span data-stu-id="b5f47-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="b5f47-107">Quando si creano nuovi gateway VPN di Resource Manager, usare i nuovi SKU del gateway.</span><span class="sxs-lookup"><span data-stu-id="b5f47-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="b5f47-108">Per informazioni sui nuovi SKU, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="b5f47-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="b5f47-109"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="b5f47-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="b5f47-110"><a name="agg"></a>Velocità effettiva aggregata stimata per SKU</span><span class="sxs-lookup"><span data-stu-id="b5f47-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="b5f47-111"><a name="config"></a>Configurazioni supportate per tipo di VPN e SKU</span><span class="sxs-lookup"><span data-stu-id="b5f47-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="b5f47-112"><a name="resize"></a>Ridimensionare un gateway (modificare uno SKU del gateway)</span><span class="sxs-lookup"><span data-stu-id="b5f47-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="b5f47-113">È possibile ridimensionare uno SKU del gateway solo all'interno della stessa famiglia di SKU.</span><span class="sxs-lookup"><span data-stu-id="b5f47-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="b5f47-114">Se si ha uno SKU Standard, ad esempio, è possibile ridimensionarlo in uno SKU HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="b5f47-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="b5f47-115">Non è possibile invece ridimensionare gateway VPN tra gli SKU di versione precedente e le nuove famiglie di SKU.</span><span class="sxs-lookup"><span data-stu-id="b5f47-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="b5f47-116">Non è possibile, ad esempio, passare da uno SKU Standard a uno SKU VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="b5f47-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="b5f47-117">Per ridimensionare uno SKU del gateway per il modello di distribuzione classica, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b5f47-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="b5f47-118">Per ridimensionare uno SKU del gateway per il modello di distribuzione di Resource Manager, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b5f47-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="b5f47-119"><a name="migrate"></a>Eseguire la migrazione ai nuovi SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="b5f47-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="b5f47-120">Se si sta usando il modello di distribuzione di Resource Manager, è possibile eseguire la migrazione ai nuovi SKU del gateway.</span><span class="sxs-lookup"><span data-stu-id="b5f47-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="b5f47-121">Se si sta usando il modello di distribuzione classica, non è possibile eseguire la migrazione ai nuovi SKU ed è necessario invece continuare a usare gli SKU di versione precedente.</span><span class="sxs-lookup"><span data-stu-id="b5f47-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b5f47-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5f47-122">Next steps</span></span>

<span data-ttu-id="b5f47-123">Per altre informazioni sui nuovi SKU del gateway, vedere [SKU del gateway](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="b5f47-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="b5f47-124">Per altre informazioni sulle impostazioni di configurazione, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b5f47-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>