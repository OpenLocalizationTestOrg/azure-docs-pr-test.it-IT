---
title: Informazioni sui gateway di rete virtuale per ExpressRoute | Microsoft Docs
description: Informazioni sui gateway di rete virtuale per ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="9b5b3-103">Informazioni sui gateway di rete virtuale per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9b5b3-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="9b5b3-104">Il gateway di rete virtuale viene usato per inviare il traffico di rete tra le reti virtuali di Azure e i percorsi locali.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="9b5b3-105">Quando si configura una connessione ExpressRoute, è necessario creare e configurare un gateway di rete virtuale e la connessione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="9b5b3-106">Quando si crea un gateway di rete virtuale, si devono specificare alcune impostazioni.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="9b5b3-107">Una delle impostazioni necessarie indica se il gateway verrà usato per il traffico VPN sito a sito o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="9b5b3-108">Nel modello di distribuzione di Gestione risorse, l'impostazione è "-GatewayType".</span><span class="sxs-lookup"><span data-stu-id="9b5b3-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="9b5b3-109">Quando il traffico di rete viene inviato con una connessione privata, si usa il tipo di gateway ExpressRoute,</span><span class="sxs-lookup"><span data-stu-id="9b5b3-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="9b5b3-110">detto appunto gateway ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="9b5b3-111">Quando il traffico di rete viene inviato crittografato attraverso una rete Internet pubblica, si usa il gateway di tipo 'VPN',</span><span class="sxs-lookup"><span data-stu-id="9b5b3-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="9b5b3-112">detto appunto gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="9b5b3-113">Le connessioni da sito a sito, da punto a sito e da rete virtuale a rete virtuale usano tutte un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="9b5b3-114">Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo di gateway.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="9b5b3-115">Ad esempio, è possibile configurare un gateway di rete virtuale che usa -GatewayType Vpn e una che usa -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="9b5b3-116">L'articolo è incentrato sul gateway di rete virtuale per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="9b5b3-117"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="9b5b3-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="9b5b3-118">Se si vuole aggiornare il gateway a uno SKU più potente, nella maggior parte dei casi è possibile usare il cmdlet PowerShell 'Resize-AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="9b5b3-119">Questa tecnica funziona per gli aggiornamenti agli SKU Standard e HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="9b5b3-120">Tuttavia, per eseguire l'aggiornamento per allo SKU UltraPerformance sarà necessario ricreare il gateway.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="9b5b3-121"><a name="aggthroughput"></a>Velocità effettiva aggregata stimata per SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="9b5b3-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="9b5b3-122">La tabella seguente illustra i tipi di gateway e la velocità effettiva aggregata stimata.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="9b5b3-123">La tabella è valida per entrambi i modelli di distribuzione classica e di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="9b5b3-124">Le velocità effettiva dell'applicazione dipende da vari fattori, ad esempio la latenza end-to-end e il numero di flussi di traffico avviati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="9b5b3-125">I numeri nella tabella rappresentano il limite massimo che l'applicazione può ottenere in teoria in un ambiente ideale.</span><span class="sxs-lookup"><span data-stu-id="9b5b3-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="9b5b3-126"><a name="resources"></a>API REST e cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b5b3-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="9b5b3-127">Per altre risorse tecniche e requisiti di sintassi specifici quando si usano le API REST e i cmdlet PowerShell per le configurazioni di gateway di rete virtuale, vedere le pagine seguenti:</span><span class="sxs-lookup"><span data-stu-id="9b5b3-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="9b5b3-128">**Classico**</span><span class="sxs-lookup"><span data-stu-id="9b5b3-128">**Classic**</span></span> | <span data-ttu-id="9b5b3-129">**Gestione risorse**</span><span class="sxs-lookup"><span data-stu-id="9b5b3-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="9b5b3-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b5b3-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="9b5b3-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b5b3-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="9b5b3-132">API REST</span><span class="sxs-lookup"><span data-stu-id="9b5b3-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="9b5b3-133">API REST</span><span class="sxs-lookup"><span data-stu-id="9b5b3-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="9b5b3-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b5b3-134">Next steps</span></span>
<span data-ttu-id="9b5b3-135">Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Panoramica tecnica relativa a ExpressRoute](expressroute-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="9b5b3-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

