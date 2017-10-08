---
title: Script di PowerShell di esempio - aaaAzure creare una macchina virtuale Windows | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare una VM Windows
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 81f04ed88a968cb7ac540b0b4b874dcf230a8e1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="e2d4e-103">Creare una macchina virtuale completamente configurata con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2d4e-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="e2d4e-104">Questo script crea una macchina virtuale di Azure che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="e2d4e-105">Dopo l'esecuzione di script hello, è possibile accedere a macchina virtuale hello il protocollo RDP.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-105">After running hello script, you can access hello virtual machine over RDP.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e2d4e-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e2d4e-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e2d4e-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e2d4e-107">Clean up deployment</span></span> 

<span data-ttu-id="e2d4e-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e2d4e-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e2d4e-109">Script explanation</span></span>

<span data-ttu-id="e2d4e-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e2d4e-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e2d4e-112">Comando</span><span class="sxs-lookup"><span data-stu-id="e2d4e-112">Command</span></span> | <span data-ttu-id="e2d4e-113">Note</span><span class="sxs-lookup"><span data-stu-id="e2d4e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e2d4e-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2d4e-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e2d4e-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e2d4e-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e2d4e-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e2d4e-117">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-117">Creates a subnet configuration.</span></span> <span data-ttu-id="e2d4e-118">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="e2d4e-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e2d4e-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="e2d4e-120">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="e2d4e-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e2d4e-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e2d4e-122">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e2d4e-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e2d4e-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="e2d4e-124">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e2d4e-125">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="e2d4e-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e2d4e-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="e2d4e-127">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="e2d4e-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e2d4e-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e2d4e-129">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-129">Gets subnet information.</span></span> <span data-ttu-id="e2d4e-130">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="e2d4e-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e2d4e-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e2d4e-132">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="e2d4e-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e2d4e-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e2d4e-134">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-134">Creates a VM configuration.</span></span> <span data-ttu-id="e2d4e-135">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e2d4e-136">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e2d4e-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e2d4e-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e2d4e-138">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="e2d4e-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2d4e-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e2d4e-140">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="e2d4e-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e2d4e-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2d4e-141">Next steps</span></span>

<span data-ttu-id="e2d4e-142">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2d4e-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e2d4e-143">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2d4e-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
