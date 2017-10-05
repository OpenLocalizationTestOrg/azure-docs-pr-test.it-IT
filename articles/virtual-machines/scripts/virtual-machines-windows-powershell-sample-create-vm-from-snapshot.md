---
title: Esempio di script di Azure PowerShell - Creare una VM da uno snapshot | Microsoft Docs
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
ms.openlocfilehash: 63d108bbfd0f58f8a40bf1c7c8649e3a1f7ed288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="1e9c8-103">Creare una macchina virtuale da uno snapshot con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e9c8-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="1e9c8-104">Questo script crea una macchina virtuale da uno snapshot di un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1e9c8-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1e9c8-105">Sample script</span></span>

<span data-ttu-id="1e9c8-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Creare una VM da un disco del sistema operativo gestito")]</span><span class="sxs-lookup"><span data-stu-id="1e9c8-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1e9c8-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1e9c8-107">Clean up deployment</span></span> 

<span data-ttu-id="1e9c8-108">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1e9c8-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1e9c8-109">Script explanation</span></span>

<span data-ttu-id="1e9c8-110">Questo script usa i comandi seguenti per ottenere le proprietà dello snapshot, creare un disco gestito da uno snapshot e creare una VM.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-110">This script uses the following commands to get snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="1e9c8-111">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1e9c8-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1e9c8-112">Command</span></span> | <span data-ttu-id="1e9c8-113">Note</span><span class="sxs-lookup"><span data-stu-id="1e9c8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e9c8-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="1e9c8-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="1e9c8-115">Ottiene uno snapshot usando il nome dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-115">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="1e9c8-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="1e9c8-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="1e9c8-117">Crea una configurazione di disco.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-117">Creates a disk configuration.</span></span> <span data-ttu-id="1e9c8-118">Questa configurazione viene usata con il processo di creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-118">This configuration is used with the disk creation process.</span></span> |
| [<span data-ttu-id="1e9c8-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="1e9c8-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="1e9c8-120">Crea un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-120">Creates a managed disk.</span></span> |
| [<span data-ttu-id="1e9c8-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="1e9c8-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="1e9c8-122">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-122">Creates a VM configuration.</span></span> <span data-ttu-id="1e9c8-123">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="1e9c8-124">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="1e9c8-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="1e9c8-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="1e9c8-126">Collega il disco gestito come disco del sistema operativo alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1e9c8-126">Attaches the managed disk as OS disk to the virtual machine</span></span> |
| [<span data-ttu-id="1e9c8-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="1e9c8-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="1e9c8-128">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="1e9c8-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1e9c8-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="1e9c8-130">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="1e9c8-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="1e9c8-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="1e9c8-132">Consente di creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-132">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="1e9c8-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e9c8-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1e9c8-134">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="1e9c8-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e9c8-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e9c8-135">Next steps</span></span>

<span data-ttu-id="1e9c8-136">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1e9c8-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1e9c8-137">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e9c8-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>