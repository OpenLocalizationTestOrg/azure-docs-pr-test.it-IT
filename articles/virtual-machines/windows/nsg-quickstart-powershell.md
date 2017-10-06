---
title: aaaOpen porte tooa VM con Azure PowerShell | Documenti Microsoft
description: "Informazioni su come tooopen una porta / creare una macchina virtuale Windows di tooyour endpoint tramite la modalità di distribuzione di gestione risorse di Azure hello e PowerShell di Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Come tooopen tooa di porte e gli endpoint di macchina virtuale in Azure tramite PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandi rapidi
Gruppo di sicurezza di rete toocreate e delle regole ACL è necessario [più recente di Azure PowerShell installata hello](/powershell/azureps-cmdlets-docs). È anche possibile [eseguire questi passaggi tramite il portale di Azure hello](nsg-quickstart-portal.md).

Accedi tooyour account di Azure:

```powershell
Login-AzureRmAccount
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Creare una regola con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow *tcp* il traffico sulla porta *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

Successivamente, creare il gruppo di sicurezza di rete con [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e assegnare hello HTTP regola appena creata come indicato di seguito. esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Ora si assegnare la subnet tooa il gruppo di sicurezza di rete. esempio Hello assegna una rete virtuale esistente denominata *myVnet* toohello variabile *$vnet* con [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Associare il gruppo di sicurezza di rete alla subnet con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). esempio Hello associa subnet hello denominata *mySubnet* con il gruppo di sicurezza di rete:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Infine, aggiornare la rete virtuale con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) affinché l'effetto di tootake modifiche:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Altre informazioni sui gruppi di sicurezza di rete
Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale. Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse. Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#manage-internal-traffic).

Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer. bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico. Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).

## <a name="next-steps"></a>Passaggi successivi
In questo esempio è stato creato il traffico HTTP tooallow una semplice regola. È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:

* [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)
* [Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico](../../load-balancer/load-balancer-arm.md)

