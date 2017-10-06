---
title: Configurare un gateway di rete virtuale per ExpressRoute con PowerShell:versione classica:Azure | Documentazione Microsoft
description: Configurare un gateway VNet per una rete virtuale con modello di distribuzione classico usando PowerShell per una configurazione ExpressRoute.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="1e678-103">Configurare un gateway di rete virtuale per ExpressRoute usando PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="1e678-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e678-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e678-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="1e678-105">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e678-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="1e678-106">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1e678-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="1e678-107">Questo articolo viene illustrato come tramite tooadd passaggi hello, ridimensionare e rimuovere un gateway di rete virtuale (VNet) per una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="1e678-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="1e678-108">Hello passaggi di questa configurazione sono in particolare per le reti virtuali create utilizzando hello **modello di distribuzione classica** e che sarà utilizzabile in una configurazione di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1e678-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="1e678-109">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="1e678-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="1e678-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="1e678-110">Before beginning</span></span>
<span data-ttu-id="1e678-111">Verificare di aver installato i cmdlet di Azure PowerShell hello necessari per questa configurazione (1.0.2 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="1e678-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="1e678-112">Se non è stato installato hello cmdlet, è necessario toodo in tal caso, prima di iniziare i passaggi di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e678-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="1e678-113">Per ulteriori informazioni sull'installazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1e678-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1e678-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e678-114">Next steps</span></span>
<span data-ttu-id="1e678-115">Dopo aver creato il gateway di rete virtuale hello, è possibile collegare il circuito ExpressRoute di tooan di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1e678-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="1e678-116">Vedere [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1e678-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

