---
title: esempio di script di PowerShell aaaAzure - instradare il traffico attraverso un dispositivo di rete virtuale | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Instradare il traffico attraverso un'appliance virtuale di rete di tipo firewall.
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Instradare il traffico attraverso un'appliance virtuale di rete

Questo script di esempio crea una rete virtuale con subnet front-end e back-end. Viene inoltre creata una macchina virtuale con IP inoltro del traffico tra due subnet hello tooroute abilitato. Dopo l'esecuzione di script hello è possibile distribuire il software di rete, ad esempio un'applicazione di firewall, toohello macchina virtuale.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete. Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Consente di creare una rete virtuale e una subnet front-end di Azure. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Consente di creare le subnet back-end e di rete perimetrale. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Consente di creare un'interfaccia di rete virtuale e attiva l'inoltro IP. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Consente di creare un gruppo di sicurezza di rete. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crea regole del gruppo che consentono le porte HTTP e HTTPS in ingresso toohello macchina virtuale. |
| [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| Associa hello NSGs e toosubnets nelle tabelle di route. |
| [New-AzureRmRouteTable](/powershell/module/azurerm.network/new-azurermroutetable)| Consente di creare una tabella di route per tutte le route. |
| [New-AzureRMRouteConfig](/powershell/module/azurerm.network/new-azurermrouteconfig)| Crea route tooroute il traffico tra subnet e hello Internet tramite hello macchina virtuale. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Crea una macchina virtuale e collega tooit NIC hello. Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
