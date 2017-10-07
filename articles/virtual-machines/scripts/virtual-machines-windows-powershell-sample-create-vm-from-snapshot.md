---
title: Esempio di Script di PowerShell - aaaAzure creare una macchina virtuale da uno snapshot | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare una VM da uno snapshot
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="5c6f7-103">Creare una macchina virtuale da uno snapshot con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c6f7-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="5c6f7-104">Questo script crea una macchina virtuale da uno snapshot di un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c6f7-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5c6f7-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5c6f7-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5c6f7-106">Clean up deployment</span></span> 

<span data-ttu-id="5c6f7-107">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5c6f7-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5c6f7-108">Script explanation</span></span>

<span data-ttu-id="5c6f7-109">Questo script utilizza hello seguenti comandi, le proprietà dello snapshot tooget, creare un disco gestito da snapshot e creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="5c6f7-110">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5c6f7-111">Comando</span><span class="sxs-lookup"><span data-stu-id="5c6f7-111">Command</span></span> | <span data-ttu-id="5c6f7-112">Note</span><span class="sxs-lookup"><span data-stu-id="5c6f7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c6f7-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="5c6f7-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="5c6f7-114">Ottiene uno snapshot usando il nome dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="5c6f7-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="5c6f7-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="5c6f7-116">Crea una configurazione di disco.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-116">Creates a disk configuration.</span></span> <span data-ttu-id="5c6f7-117">Questa configurazione viene utilizzata con processo di creazione del disco hello.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="5c6f7-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="5c6f7-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="5c6f7-119">Crea un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="5c6f7-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5c6f7-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5c6f7-121">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-121">Creates a VM configuration.</span></span> <span data-ttu-id="5c6f7-122">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5c6f7-123">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5c6f7-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="5c6f7-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="5c6f7-125">Collega disco gestito hello come macchina virtuale di toohello disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="5c6f7-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="5c6f7-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5c6f7-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5c6f7-127">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5c6f7-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5c6f7-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5c6f7-129">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="5c6f7-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5c6f7-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5c6f7-131">Consente di creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="5c6f7-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5c6f7-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5c6f7-133">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="5c6f7-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c6f7-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c6f7-134">Next steps</span></span>

<span data-ttu-id="5c6f7-135">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c6f7-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c6f7-136">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c6f7-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
