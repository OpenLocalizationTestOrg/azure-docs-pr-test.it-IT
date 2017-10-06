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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Configurare un gateway di rete virtuale per ExpressRoute usando PowerShell (versione classica)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classica: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Questo articolo viene illustrato come tramite tooadd passaggi hello, ridimensionare e rimuovere un gateway di rete virtuale (VNet) per una rete virtuale esistente. Hello passaggi di questa configurazione sono in particolare per le reti virtuali create utilizzando hello **modello di distribuzione classica** e che sarà utilizzabile in una configurazione di ExpressRoute. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Prima di iniziare
Verificare di aver installato i cmdlet di Azure PowerShell hello necessari per questa configurazione (1.0.2 o versione successiva). Se non è stato installato hello cmdlet, è necessario toodo in tal caso, prima di iniziare i passaggi di configurazione hello. Per ulteriori informazioni sull'installazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il gateway di rete virtuale hello, è possibile collegare il circuito ExpressRoute di tooan di rete virtuale. Vedere [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md).

