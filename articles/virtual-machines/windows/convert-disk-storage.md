---
title: Convertire l'archiviazione di Azure Managed Disks da Standard a Premium e viceversa | Microsoft Docs
description: Come convertire Azure Managed Disks da Standard a Premium e viceversa usando Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 9e5c73ceb0ff7d9c18c9cf7128b69e40b9796874
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="8e3f6-103">Convertire l'archiviazione di Azure Managed Disks da Standard a Premium e viceversa</span><span class="sxs-lookup"><span data-stu-id="8e3f6-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="8e3f6-104">Managed Disks offre due opzioni di archiviazione: [Premium](../../storage/storage-premium-storage.md) (basata su SSD) e [Standard](../../storage/storage-standard-storage.md) (basata su HDD).</span><span class="sxs-lookup"><span data-stu-id="8e3f6-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="8e3f6-105">È possibile passare facilmente tra le due opzioni con un tempo di inattività minimo in base alle esigenze in termini di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="8e3f6-106">Questa funzionalità non è disponibile per i dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="8e3f6-107">È possibile eseguire facilmente la [conversione a Managed Disks](convert-unmanaged-to-managed-disks.md) per passare facilmente tra le due opzioni.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="8e3f6-108">Questo articolo illustra come convertire la versione di Managed Disks da Standard a Premium e viceversa usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="8e3f6-109">Se è necessario eseguirne l'installazione o l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8e3f6-109">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8e3f6-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8e3f6-110">Before you begin</span></span>

* <span data-ttu-id="8e3f6-111">La conversione richiede un riavvio della VM, quindi pianificare la migrazione dell'archiviazione su dischi durante una finestra di manutenzione preesistente.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="8e3f6-112">Se si usano dischi non gestiti, prima di tutto eseguire la [conversione a Managed Disks](convert-unmanaged-to-managed-disks.md) per poi passare tra le due opzioni di archiviazione come indicato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="8e3f6-113">Convertire tutte le istanze di Managed Disks di una VM da Standard a Premium e viceversa</span><span class="sxs-lookup"><span data-stu-id="8e3f6-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="8e3f6-114">L'esempio seguente illustra come passare dall'archiviazione Standard all'archiviazione Premium per tutti i dischi di una VM.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="8e3f6-115">Per usare i dischi gestiti Premium, la VM deve avere [dimensioni tali](sizes.md) da supportare l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="8e3f6-116">In questo esempio si passa anche a una dimensione che supporta l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-116">This example also switches to a size that supports premium storage.</span></span>

```powershell
# Name of the resource group that contains the VM
$rgName = 'yourResourceGroup'

# Name of the your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard to premium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate the VM before changing the size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in the resource group of the VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong to the selected VM, convert to premium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="8e3f6-117">Convertire un disco gestito da Standard a Premium e viceversa</span><span class="sxs-lookup"><span data-stu-id="8e3f6-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="8e3f6-118">Per il carico di lavoro di sviluppo/test, potrebbe essere necessaria una combinazione di dischi Standard e Premium, per ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="8e3f6-119">A tale scopo, è possibile eseguire l'aggiornamento ad Archiviazione Premium solo per i dischi che richiedono prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="8e3f6-120">L'esempio seguente illustra come passare dall'archiviazione Standard all'archiviazione Premium e viceversa per un singolo disco di una VM.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="8e3f6-121">Per usare i dischi gestiti Premium, la VM deve avere [dimensioni tali](sizes.md) da supportare l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="8e3f6-122">In questo esempio si passa anche a una dimensione che supporta l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="8e3f6-122">This example also switches to a size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains the managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get the ARM resource to get name and resource group of the VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate the VM before changing the storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update the storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="8e3f6-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e3f6-123">Next steps</span></span>

<span data-ttu-id="8e3f6-124">Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="8e3f6-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

