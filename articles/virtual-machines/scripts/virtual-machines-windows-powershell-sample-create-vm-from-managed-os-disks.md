---
title: Esempio di Script di PowerShell - aaaAzure creare una macchina virtuale collegando un disco come disco del sistema operativo gestito | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare una VM collegando un disco gestito come disco del sistema operativo
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="d0602-103">Creare una macchina virtuale usando un disco del sistema operativo gestito esistente con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0602-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="d0602-104">Questo script crea una macchina virtuale collegando un disco gestito esistente come disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d0602-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="d0602-105">Usare questo script negli scenari precedenti:</span><span class="sxs-lookup"><span data-stu-id="d0602-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="d0602-106">Creare una VM da un disco del sistema operativo gestito esistente che è stato copiato da un disco gestito in una sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="d0602-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="d0602-107">Creare una VM da un disco gestito esistente che è stato creato da un file VHD specializzato</span><span class="sxs-lookup"><span data-stu-id="d0602-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="d0602-108">Creare una VM da un disco del sistema operativo gestito esistente che è stato creato da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="d0602-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d0602-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d0602-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d0602-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d0602-110">Clean up deployment</span></span> 

<span data-ttu-id="d0602-111">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="d0602-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d0602-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d0602-112">Script explanation</span></span>

<span data-ttu-id="d0602-113">Questo script utilizza i seguenti comandi gestiti tooget disco proprietà hello, collegare un disco gestito di tooa nuova macchina virtuale e creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0602-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="d0602-114">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="d0602-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d0602-115">Comando</span><span class="sxs-lookup"><span data-stu-id="d0602-115">Command</span></span> | <span data-ttu-id="d0602-116">Note</span><span class="sxs-lookup"><span data-stu-id="d0602-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d0602-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="d0602-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="d0602-118">Ottiene l'oggetto disco in base a nome hello e gruppo di risorse hello di un disco.</span><span class="sxs-lookup"><span data-stu-id="d0602-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="d0602-119">Proprietà ID di hello restituito l'oggetto disco è utilizzato tooattach hello disco tooa nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d0602-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="d0602-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d0602-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d0602-121">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="d0602-121">Creates a VM configuration.</span></span> <span data-ttu-id="d0602-122">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="d0602-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d0602-123">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0602-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d0602-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="d0602-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="d0602-125">Collega un disco gestito con proprietà Id hello del disco hello come disco del sistema operativo tooa nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d0602-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="d0602-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d0602-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d0602-127">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d0602-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d0602-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d0602-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d0602-129">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="d0602-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="d0602-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d0602-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d0602-131">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0602-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="d0602-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d0602-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d0602-133">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="d0602-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d0602-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0602-134">Next steps</span></span>

<span data-ttu-id="d0602-135">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0602-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d0602-136">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0602-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
