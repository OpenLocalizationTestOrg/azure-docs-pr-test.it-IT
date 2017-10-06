---
title: "bilanciamento del carico aaaAzure Script di PowerShell di esempio - più siti Web con Azure PowerShell | Documenti Microsoft"
description: "Esempio di Script di PowerShell Azure - più siti Web toohello il bilanciamento del carico stessa macchina virtuale"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Eseguire il bilanciamento del carico per più siti Web

Questo esempio di script crea una rete virtuale con due macchine virtuali che fanno parte di un set di disponibilità. Un servizio di bilanciamento del carico indirizza il traffico di due macchine virtuali toohello due indirizzi IP. Dopo l'esecuzione dello script hello, è possibile distribuire toohello software tramite server web le macchine virtuali e ospitare più siti web, ciascuno con il proprio indirizzo IP.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, la rete virtuale, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Crea una set di disponibilità di Azure tooprovide la disponibilità elevata. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crea una configurazione di subnet. Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Crea una rete virtuale. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Crea un indirizzo IP pubblico. |
| [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | Crea una configurazione IP front-end per un servizio di bilanciamento del carico. |
| [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | Crea una configurazione del pool di indirizzi back-end per un servizio di bilanciamento del carico. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Consente di creare un probe di bilanciamento del carico di rete. Un probe di bilanciamento carico di rete viene utilizzato toomonitor ogni macchina virtuale nel set di bilanciamento carico di rete hello. Se qualsiasi macchina virtuale non è accessibile, il traffico non è indirizzato toohello macchina virtuale. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Consente di creare una regola di bilanciamento del carico di rete. In questo esempio viene creata una regola per la porta 80. Come il traffico HTTP riceve hello bilanciamento carico di rete, è indirizzato tooport 80 una delle macchine virtuali di hello nel set di bilanciamento carico di rete hello. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) | Crea un servizio di bilanciamento del carico. |
| [New-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | Definisce le funzionalità avanzate per un'interfaccia di rete virtuale. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea un'interfaccia di rete. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crea una configurazione di VM. Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative. configurazione di Hello viene utilizzato durante la creazione della macchina virtuale. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Creare una macchina virtuale. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
