---
title: gateway di rete virtuale ExpressRoute aaaAbout | Documenti Microsoft
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
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="a19db-103">Informazioni sui gateway di rete virtuale per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a19db-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="a19db-104">Viene utilizzato un gateway di rete virtuale toosend il traffico tra reti virtuali di Azure e i percorsi locali.</span><span class="sxs-lookup"><span data-stu-id="a19db-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="a19db-105">Quando si configura una connessione ExpressRoute, è necessario creare e configurare un gateway di rete virtuale e la connessione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a19db-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="a19db-106">Quando si crea un gateway di rete virtuale, si devono specificare alcune impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a19db-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="a19db-107">Una delle impostazioni necessarie hello specifica se verrà utilizzato per il traffico di ExpressRoute o Site-to-Site VPN gateway hello.</span><span class="sxs-lookup"><span data-stu-id="a19db-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="a19db-108">Nel modello di distribuzione di gestione risorse hello, impostazione hello è '-il tipo di gateway '.</span><span class="sxs-lookup"><span data-stu-id="a19db-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="a19db-109">Quando il traffico di rete viene inviato su una connessione privata, si utilizza il tipo di gateway hello 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="a19db-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="a19db-110">Questo è un gateway ExpressRoute di tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="a19db-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="a19db-111">Quando il traffico di rete viene inviato in forma crittografato tra hello rete Internet pubblica, si utilizza il tipo di gateway hello 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="a19db-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="a19db-112">Si tratta di un gateway VPN di tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="a19db-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="a19db-113">Le connessioni da sito a sito, da punto a sito e da rete virtuale a rete virtuale usano tutte un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="a19db-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="a19db-114">Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo di gateway.</span><span class="sxs-lookup"><span data-stu-id="a19db-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="a19db-115">Ad esempio, è possibile configurare un gateway di rete virtuale che usa -GatewayType Vpn e una che usa -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a19db-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="a19db-116">In questo articolo è incentrato sul gateway di rete virtuale hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a19db-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="a19db-117"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="a19db-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="a19db-118">Se si desidera tooupgrade tooa il gateway più potente gateway SKU, nella maggior parte dei casi è possibile utilizzare hello cmdlet di PowerShell 'Ridimensionamento AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="a19db-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="a19db-119">Questa tecnica funziona per gli aggiornamenti tooStandard e SKU ad alte prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a19db-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="a19db-120">Tuttavia, tooupgrade toohello UltraPerformance SKU, sarà necessario gateway hello toorecreate.</span><span class="sxs-lookup"><span data-stu-id="a19db-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="a19db-121"><a name="aggthroughput"></a>Velocità effettiva aggregata stimata per SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="a19db-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="a19db-122">Hello nella tabella seguente mostra i tipi di gateway hello e velocità effettiva aggregata di hello stimato.</span><span class="sxs-lookup"><span data-stu-id="a19db-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="a19db-123">Questa tabella si applica hello tooboth Gestione risorse e i modelli di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="a19db-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a19db-124">Velocità effettiva dell'applicazione dipende da vari fattori, ad esempio la latenza end-to-end di hello, e il numero di hello del traffico flussi hello aperto dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a19db-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="a19db-125">numeri di Hello hello tabella rappresentano hello limite massimo utilizzabile da un'applicazione hello theorectically raggiungono in un ambiente ideale.</span><span class="sxs-lookup"><span data-stu-id="a19db-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="a19db-126"><a name="resources"></a>API REST e cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="a19db-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="a19db-127">Per i requisiti di sintassi specifici quando si utilizzano le API REST e i cmdlet di PowerShell per le configurazioni di gateway di rete virtuale e risorse tecniche aggiuntive, vedere hello seguenti pagine:</span><span class="sxs-lookup"><span data-stu-id="a19db-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="a19db-128">**Classico**</span><span class="sxs-lookup"><span data-stu-id="a19db-128">**Classic**</span></span> | <span data-ttu-id="a19db-129">**Gestione risorse**</span><span class="sxs-lookup"><span data-stu-id="a19db-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="a19db-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a19db-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="a19db-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a19db-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="a19db-132">API REST</span><span class="sxs-lookup"><span data-stu-id="a19db-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="a19db-133">API REST</span><span class="sxs-lookup"><span data-stu-id="a19db-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="a19db-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a19db-134">Next steps</span></span>
<span data-ttu-id="a19db-135">Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Panoramica tecnica relativa a ExpressRoute](expressroute-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="a19db-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

