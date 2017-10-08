---
title: gateway di rete virtuale di Azure aaaLegacy SKU | Documenti Microsoft
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
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="2e3e8-103">Utilizzo degli SKU del gateway di rete virtuale (SKU di versione precedente)</span><span class="sxs-lookup"><span data-stu-id="2e3e8-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="2e3e8-104">Questo articolo contiene informazioni su hello legacy (precedente) gateway di rete virtuale SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="2e3e8-105">legacy Hello SKU continuerà a funzionare in entrambi i modelli di distribuzione per i gateway VPN che sono già stati creati.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="2e3e8-106">Gateway VPN classico continuare toouse hello SKU legacy, sia per il gateway esistente e per nuovi gateway.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="2e3e8-107">Quando si crea nuovo Gestione risorse VPN gateway, è possibile usare gateway di nuovo hello SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="2e3e8-108">Per informazioni su hello nuovo SKU, vedere [sul Gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="2e3e8-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="2e3e8-109"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="2e3e8-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="2e3e8-110"><a name="agg"></a>Velocità effettiva aggregata stimata per SKU</span><span class="sxs-lookup"><span data-stu-id="2e3e8-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="2e3e8-111"><a name="config"></a>Configurazioni supportate per tipo di VPN e SKU</span><span class="sxs-lookup"><span data-stu-id="2e3e8-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="2e3e8-112"><a name="resize"></a>Ridimensionare un gateway (modificare uno SKU del gateway)</span><span class="sxs-lookup"><span data-stu-id="2e3e8-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="2e3e8-113">È possibile ridimensionare un SKU di gateway all'interno di hello stessa famiglia SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="2e3e8-114">Se si dispone di una SKU Standard, ad esempio, è possibile ridimensionare tooa HighPerformance SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="2e3e8-115">Non è possibile ridimensionare la VPN gateway tra hello SKU precedente e hello nuove famiglie SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="2e3e8-116">Ad esempio, è non è possibile passare da un tooa SKU Standard VpnGw2 SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="2e3e8-117">tooresize un SKU di gateway per hello classico modello di distribuzione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e3e8-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="2e3e8-118">un gateway SKU per il modello di distribuzione di gestione delle risorse, hello tooresize utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e3e8-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="2e3e8-119"><a name="migrate"></a>Eseguire la migrazione toohello nuovo gateway SKU</span><span class="sxs-lookup"><span data-stu-id="2e3e8-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="2e3e8-120">Se si lavora con modello di distribuzione di gestione risorse di hello, è possibile migrare toohello nuovo gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="2e3e8-121">Se si sta usando il modello di distribuzione classica hello, è possibile eseguire la migrazione toohello nuovo SKU e deve proseguire toouse hello SKU legacy.</span><span class="sxs-lookup"><span data-stu-id="2e3e8-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2e3e8-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e3e8-122">Next steps</span></span>

<span data-ttu-id="2e3e8-123">Per ulteriori informazioni su hello nuovo SKU di Gateway, vedere [SKU di Gateway](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="2e3e8-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="2e3e8-124">Per altre informazioni sulle impostazioni di configurazione, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2e3e8-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>