---
title: Modificare i prefissi di indirizzo IP gateway hello rete locale e l'indirizzo IP del Gateway VPN di hello | Azure | Portale | Documenti Microsoft
description: In questo articolo illustra la modifica di prefissi di indirizzi IP per il gateway di rete locale tramite hello portale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Modificare le impostazioni di gateway di rete locale utilizzando hello portale di Azure

In alcuni casi modificare le impostazioni di hello per il gateway di rete locale AddressPrefix o GatewayIPAddress. In questo articolo illustra come toomodify le impostazioni del gateway di rete locale. È inoltre possibile modificare queste impostazioni utilizzando un metodo diverso selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP

Quando si modificano i prefissi di indirizzi IP, hello è attenersi alla procedura dipendono se il gateway di rete locale dispone di una connessione.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Modificare l'indirizzo IP del gateway hello

Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare. Quando si modifica l'indirizzo IP pubblico hello, hello è attenersi alla procedura dipendono se il gateway di rete locale dispone di una connessione.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Passaggi successivi

È possibile verificare la connessione al gateway. Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).