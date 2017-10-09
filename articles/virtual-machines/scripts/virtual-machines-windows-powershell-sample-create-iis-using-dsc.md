---
title: aaaAzure Script di PowerShell di esempio - IIS con DSC | Documenti Microsoft
description: Esempio di script di Azure PowerShell - IIS con DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a>Creare una VM IIS con PowerShell

Questo script crea una macchina virtuale di Azure che esegue Windows Server 2016 e quindi utilizza hello estensione DSC della macchina virtuale Azure tooinstall IIS. Dopo l'esecuzione di script hello, è possibile accedere il sito Web IIS predefinito hello in indirizzo IP pubblico hello della macchina virtuale hello.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello dopo la distribuzione di comandi toocreate hello. Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crea una configurazione di subnet. Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Crea una rete virtuale. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Crea un indirizzo IP pubblico. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crea una configurazione di regola del gruppo di sicurezza di rete. Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Crea un gruppo di sicurezza di rete. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | Ottiene informazioni sulla subnet. Queste informazioni vengono usate durante la creazione di un'interfaccia di rete. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea un'interfaccia di rete. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crea una configurazione di VM. Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative. configurazione di Hello viene utilizzato durante la creazione della macchina virtuale. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Creare una macchina virtuale. |
| [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) | Aggiungere una macchina virtuale VM estensione toohello. In questo esempio, un'estensione personalizzata hello è tooinstall utilizzato IIS. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
