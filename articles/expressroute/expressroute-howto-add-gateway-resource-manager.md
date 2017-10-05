---
title: 'Aggiungere un gateway di rete virtuale a una rete virtuale per ExpressRoute: PowerShell: Azure | Documentazione Microsoft'
description: "Questo articolo illustra come aggiungere un gateway di rete virtuale a una rete virtuale di Resource Manager già creata per ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="58ad9-103">Configurare un gateway di rete virtuale per ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="58ad9-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58ad9-104">Resource Manager - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="58ad9-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="58ad9-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="58ad9-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="58ad9-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="58ad9-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="58ad9-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="58ad9-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="58ad9-108">Questo articolo illustra le procedure per l'aggiunta, il ridimensionamento e la rimozione di un gateway di rete virtuale per una rete virtuale già esistente.</span><span class="sxs-lookup"><span data-stu-id="58ad9-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="58ad9-109">I passaggi di questa configurazione sono specifici per le reti virtuali create usando il modello di distribuzione di Resource Manager che viene usato in una configurazione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="58ad9-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="58ad9-110">Per altre informazioni sui gateway di rete virtuale e sulle impostazioni di configurazione dei gateway per ExpressRoute, vedere [Informazioni sui gateway di rete virtuale per ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="58ad9-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="58ad9-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="58ad9-111">Before beginning</span></span>
<span data-ttu-id="58ad9-112">Assicurarsi che sia installata la versione più recente dei cmdlet Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58ad9-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="58ad9-113">Se i cmdlet più recenti non sono stati installati, è necessario eseguire l'operazione prima di iniziare i passaggi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="58ad9-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="58ad9-114">Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58ad9-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="58ad9-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58ad9-115">Next steps</span></span>
<span data-ttu-id="58ad9-116">Dopo avere creato il gateway VNet, è possibile collegare la rete virtuale a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="58ad9-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="58ad9-117">Vedere [Collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="58ad9-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

