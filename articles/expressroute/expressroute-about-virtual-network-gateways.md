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
# <a name="about-virtual-network-gateways-for-expressroute"></a>Informazioni sui gateway di rete virtuale per ExpressRoute
Viene utilizzato un gateway di rete virtuale toosend il traffico tra reti virtuali di Azure e i percorsi locali. Quando si configura una connessione ExpressRoute, è necessario creare e configurare un gateway di rete virtuale e la connessione corrispondente.

Quando si crea un gateway di rete virtuale, si devono specificare alcune impostazioni. Una delle impostazioni necessarie hello specifica se verrà utilizzato per il traffico di ExpressRoute o Site-to-Site VPN gateway hello. Nel modello di distribuzione di gestione risorse hello, impostazione hello è '-il tipo di gateway '.

Quando il traffico di rete viene inviato su una connessione privata, si utilizza il tipo di gateway hello 'ExpressRoute'. Questo è un gateway ExpressRoute di tooas cui viene fatto riferimento. Quando il traffico di rete viene inviato in forma crittografato tra hello rete Internet pubblica, si utilizza il tipo di gateway hello 'Vpn'. Si tratta di un gateway VPN di tooas cui viene fatto riferimento. Le connessioni da sito a sito, da punto a sito e da rete virtuale a rete virtuale usano tutte un gateway VPN.

Ogni rete virtuale può avere un solo gateway di rete virtuale per tipo di gateway. Ad esempio, è possibile configurare un gateway di rete virtuale che usa -GatewayType Vpn e una che usa -GatewayType ExpressRoute. In questo articolo è incentrato sul gateway di rete virtuale hello ExpressRoute.

## <a name="gwsku"></a>SKU del gateway
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Se si desidera tooupgrade tooa il gateway più potente gateway SKU, nella maggior parte dei casi è possibile utilizzare hello cmdlet di PowerShell 'Ridimensionamento AzureRmVirtualNetworkGateway'. Questa tecnica funziona per gli aggiornamenti tooStandard e SKU ad alte prestazioni. Tuttavia, tooupgrade toohello UltraPerformance SKU, sarà necessario gateway hello toorecreate.

### <a name="aggthroughput"></a>Velocità effettiva aggregata stimata per SKU del gateway
Hello nella tabella seguente mostra i tipi di gateway hello e velocità effettiva aggregata di hello stimato. Questa tabella si applica hello tooboth Gestione risorse e i modelli di distribuzione classica.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Velocità effettiva dell'applicazione dipende da vari fattori, ad esempio la latenza end-to-end di hello, e il numero di hello del traffico flussi hello aperto dall'applicazione. numeri di Hello hello tabella rappresentano hello limite massimo utilizzabile da un'applicazione hello theorectically raggiungono in un ambiente ideale. 
> 
>

## <a name="resources"></a>API REST e cmdlet PowerShell
Per i requisiti di sintassi specifici quando si utilizzano le API REST e i cmdlet di PowerShell per le configurazioni di gateway di rete virtuale e risorse tecniche aggiuntive, vedere hello seguenti pagine:

| **Classico** | **Gestione risorse** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [API REST](https://msdn.microsoft.com/library/jj154113.aspx) |[API REST](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulle configurazioni delle connessioni disponibili, vedere [Panoramica tecnica relativa a ExpressRoute](expressroute-introduction.md) . 

