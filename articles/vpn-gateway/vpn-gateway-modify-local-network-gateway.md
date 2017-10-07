---
title: Modificare i prefissi di indirizzo IP gateway hello rete locale e l'indirizzo IP del Gateway VPN di hello | Azure | PowerShell | Documenti Microsoft
description: Questo articolo illustra in modo dettagliato come modificare i prefissi degli indirizzi IP per il gateway di rete locale usando PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modificare le impostazioni del gateway di rete locale usando PowerShell

In alcuni casi modificare le impostazioni di hello per il gateway di rete locale AddressPrefix o GatewayIPAddress. In questo articolo illustra come toomodify le impostazioni del gateway di rete locale. È inoltre possibile modificare queste impostazioni utilizzando un metodo diverso selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Prima di iniziare

Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.

## <a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Modificare l'indirizzo IP del gateway hello

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Passaggi successivi

È possibile verificare la connessione al gateway. Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).