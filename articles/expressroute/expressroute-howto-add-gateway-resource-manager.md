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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Configurare un gateway di rete virtuale per ExpressRoute usando PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager - Portale di Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classica: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Questo articolo illustra hello passaggi tooadd, ridimensionare e rimuovere un gateway di rete virtuale (VNet) per una rete virtuale esistente. passaggi di Hello per questa configurazione sono in particolare per le reti virtuali creati con modello di distribuzione di gestione risorse hello che verrà utilizzato in una configurazione di ExpressRoute. Per altre informazioni sui gateway di rete virtuale e sulle impostazioni di configurazione dei gateway per ExpressRoute, vedere [Informazioni sui gateway di rete virtuale per ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Prima di iniziare
Verificare di aver installato il cmdlet PowerShell di Azure più recenti di hello. Se non è stato installato il cmdlet più recenti di hello, è necessario toodo in tal caso, prima di iniziare i passaggi di configurazione hello. Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il gateway di rete virtuale hello, è possibile collegare il circuito ExpressRoute di tooan di rete virtuale. Vedere [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md).

