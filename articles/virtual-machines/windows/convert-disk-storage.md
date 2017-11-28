---
title: aaaConvert Azure gestito archiviazione dischi da toopremium standard e viceversa | Documenti Microsoft
description: Come dischi tooconvert Azure gestiti da toopremium standard e viceversa, tramite Azure PowerShell.
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
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b7355-103">Convertire Azure archiviazione dischi gestiti da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="b7355-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b7355-104">Managed Disks offre due opzioni di archiviazione: [Premium](../../storage/storage-premium-storage.md) (basata su SSD) e [Standard](../../storage/storage-standard-storage.md) (basata su HDD).</span><span class="sxs-lookup"><span data-stu-id="b7355-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="b7355-105">Consente di commutatore tooeasily tra le opzioni di hello due con tempo di inattività minimo in base alle proprie esigenze di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b7355-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="b7355-106">Questa funzionalità non è disponibile per i dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="b7355-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="b7355-107">Ma è possibile facilmente [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily commutatore tra le opzioni di hello due.</span><span class="sxs-lookup"><span data-stu-id="b7355-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="b7355-108">Questo articolo illustra come tooconvert dischi gestiti da toopremium standard e, viceversa, tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7355-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="b7355-109">Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b7355-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7355-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b7355-110">Before you begin</span></span>

* <span data-ttu-id="b7355-111">la conversione di Hello richiede un riavvio della macchina virtuale hello, pertanto, pianificare la migrazione di hello dello spazio di archiviazione dischi durante una finestra di manutenzione preesistente.</span><span class="sxs-lookup"><span data-stu-id="b7355-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="b7355-112">Se si utilizza innanzitutto i dischi non gestiti, [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch questo articolo tra le opzioni di archiviazione hello due.</span><span class="sxs-lookup"><span data-stu-id="b7355-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b7355-113">Converti tutti hello gestiti dischi di una macchina virtuale da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="b7355-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b7355-114">Nell'esempio seguente di hello, ecco come tooswitch tutti hello dischi di una macchina virtuale dall'archiviazione toopremium standard.</span><span class="sxs-lookup"><span data-stu-id="b7355-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="b7355-115">dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="b7355-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b7355-116">Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="b7355-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b7355-117">Convertire un disco gestito da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="b7355-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b7355-118">Il carico di lavoro di sviluppo/test, è consigliabile toohave combinazione di dischi standard e premium tooreduce i costi.</span><span class="sxs-lookup"><span data-stu-id="b7355-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="b7355-119">È possibile ottenere questo risultato con l'aggiornamento di archiviazione toopremium, solo i dischi di hello che richiedono prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="b7355-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="b7355-120">Nell'esempio seguente di hello, ecco come tooswitch un singolo disco di una macchina virtuale dall'archiviazione toopremium standard e viceversa.</span><span class="sxs-lookup"><span data-stu-id="b7355-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="b7355-121">dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="b7355-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b7355-122">Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="b7355-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="b7355-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7355-123">Next steps</span></span>

<span data-ttu-id="b7355-124">Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b7355-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

