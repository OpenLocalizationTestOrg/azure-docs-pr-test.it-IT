---
title: 'Aggiungere un tooa di gateway di rete virtuale tra reti virtuali per ExpressRoute: PowerShell: Azure | Documenti Microsoft'
description: "In questo articolo viene illustrata l'aggiunta di un tooan di gateway di rete virtuale già creata VNet Gestione risorse per ExpressRoute."
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
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="d2248-103">Configurare un gateway di rete virtuale per ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2248-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2248-104">Resource Manager - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d2248-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="d2248-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2248-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="d2248-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2248-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="d2248-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d2248-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="d2248-108">Questo articolo illustra hello passaggi tooadd, ridimensionare e rimuovere un gateway di rete virtuale (VNet) per una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="d2248-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="d2248-109">passaggi di Hello per questa configurazione sono in particolare per le reti virtuali creati con modello di distribuzione di gestione risorse hello che verrà utilizzato in una configurazione di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d2248-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="d2248-110">Per altre informazioni sui gateway di rete virtuale e sulle impostazioni di configurazione dei gateway per ExpressRoute, vedere [Informazioni sui gateway di rete virtuale per ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="d2248-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="d2248-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d2248-111">Before beginning</span></span>
<span data-ttu-id="d2248-112">Verificare di aver installato il cmdlet PowerShell di Azure più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="d2248-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d2248-113">Se non è stato installato il cmdlet più recenti di hello, è necessario toodo in tal caso, prima di iniziare i passaggi di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="d2248-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="d2248-114">Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2248-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d2248-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2248-115">Next steps</span></span>
<span data-ttu-id="d2248-116">Dopo aver creato il gateway di rete virtuale hello, è possibile collegare il circuito ExpressRoute di tooan di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d2248-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="d2248-117">Vedere [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d2248-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

