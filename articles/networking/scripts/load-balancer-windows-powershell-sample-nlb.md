---
title: "Esempio di Script di PowerShell - tooVMs traffico bilanciamento di carico per la disponibilità elevata aaaAzure | Documenti Microsoft"
description: "Esempio di Script di PowerShell Azure - tooVMs traffico bilanciamento di carico per la disponibilità elevata"
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
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Caricare tooVMs di bilanciare il traffico per la disponibilità elevata

In questo esempio di script crea tutti gli elementi necessari toorun diverse macchine virtuali di Windows configurati a disponibilità elevata e carico bilanciato di configurazione. Tre macchine virtuali, tooan aggiunti a un Set di disponibilità di Azure, sarà necessario dopo l'esecuzione dello script, hello e accessibile tramite un servizio di bilanciamento del carico di Azure.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crea una configurazione di subnet. Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Consente di creare una rete virtuale e una subnet di Azure. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Crea un servizio di bilanciamento del carico di Azure. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Crea un probe di bilanciamento del carico. Un probe di bilanciamento del carico è toomonitor usato ogni macchina virtuale nel set di bilanciamento carico di hello. Se qualsiasi macchina virtuale non è accessibile, il traffico non è indirizzato toohello macchina virtuale. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Crea una regola del bilanciamento del carico. In questo esempio viene creata una regola per la porta 80. Come il traffico HTTP arriva al servizio di bilanciamento del carico hello, è indirizzato tooport 80 una delle macchine virtuali di hello nel set di bilanciamento carico di hello. |
| [New-AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Crea una regola Network Address Translation (NAT) di bilanciamento del carico.  Le regole NAT mapping di una porta della porta di tooa del bilanciamento del carico hello in una macchina virtuale. In questo esempio, viene creata una regola NAT per il traffico SSH tooeach macchina virtuale nel set di bilanciamento carico di hello.  |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Crea un gruppo di sicurezza di rete (gruppo), ovvero un limite di sicurezza tra le macchine virtuali internet e hello hello. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crea un tooallow regola NSG il traffico in ingresso. In questo esempio, la porta 22 è aperta al traffico SSH. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea una scheda di rete virtuale e la collega toohello di rete virtuale, subnet e gruppo. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Consente di creare un set di disponibilità. Set di disponibilità la distribuzione di macchine virtuali hello tra risorse fisiche in modo che se si verifica l'errore, non è stato eseguito alcun set intero di hello assicurare la disponibilità dell'applicazione. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crea una configurazione di VM. Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative. configurazione di Hello viene utilizzato durante la creazione della macchina virtuale. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
