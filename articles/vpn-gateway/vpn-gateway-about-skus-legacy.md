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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Utilizzo degli SKU del gateway di rete virtuale (SKU di versione precedente)

Questo articolo contiene informazioni su hello legacy (precedente) gateway di rete virtuale SKU. legacy Hello SKU continuerà a funzionare in entrambi i modelli di distribuzione per i gateway VPN che sono già stati creati. Gateway VPN classico continuare toouse hello SKU legacy, sia per il gateway esistente e per nuovi gateway. Quando si crea nuovo Gestione risorse VPN gateway, è possibile usare gateway di nuovo hello SKU. Per informazioni su hello nuovo SKU, vedere [sul Gateway VPN](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>SKU del gateway

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Velocità effettiva aggregata stimata per SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Configurazioni supportate per tipo di VPN e SKU

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Ridimensionare un gateway (modificare uno SKU del gateway)

È possibile ridimensionare un SKU di gateway all'interno di hello stessa famiglia SKU. Se si dispone di una SKU Standard, ad esempio, è possibile ridimensionare tooa HighPerformance SKU. Non è possibile ridimensionare la VPN gateway tra hello SKU precedente e hello nuove famiglie SKU. Ad esempio, è non è possibile passare da un tooa SKU Standard VpnGw2 SKU. 

tooresize un SKU di gateway per hello classico modello di distribuzione, utilizzare hello comando seguente:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

un gateway SKU per il modello di distribuzione di gestione delle risorse, hello tooresize utilizzare hello comando seguente:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Eseguire la migrazione toohello nuovo gateway SKU

Se si lavora con modello di distribuzione di gestione risorse di hello, è possibile migrare toohello nuovo gateway SKU. Se si sta usando il modello di distribuzione classica hello, è possibile eseguire la migrazione toohello nuovo SKU e deve proseguire toouse hello SKU legacy.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello nuovo SKU di Gateway, vedere [SKU di Gateway](vpn-gateway-about-vpngateways.md#gwsku).

Per altre informazioni sulle impostazioni di configurazione, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).