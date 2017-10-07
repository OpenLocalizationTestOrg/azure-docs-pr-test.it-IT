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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Convertire Azure archiviazione dischi gestiti da toopremium standard e viceversa

Managed Disks offre due opzioni di archiviazione: [Premium](../../storage/storage-premium-storage.md) (basata su SSD) e [Standard](../../storage/storage-standard-storage.md) (basata su HDD). Consente di commutatore tooeasily tra le opzioni di hello due con tempo di inattività minimo in base alle proprie esigenze di prestazioni. Questa funzionalità non è disponibile per i dischi non gestiti. Ma è possibile facilmente [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily commutatore tra le opzioni di hello due.

Questo articolo illustra come tooconvert dischi gestiti da toopremium standard e, viceversa, tramite Azure PowerShell. Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Prima di iniziare

* la conversione di Hello richiede un riavvio della macchina virtuale hello, pertanto, pianificare la migrazione di hello dello spazio di archiviazione dischi durante una finestra di manutenzione preesistente. 
* Se si utilizza innanzitutto i dischi non gestiti, [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch questo articolo tra le opzioni di archiviazione hello due. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converti tutti hello gestiti dischi di una macchina virtuale da toopremium standard e viceversa

Nell'esempio seguente di hello, ecco come tooswitch tutti hello dischi di una macchina virtuale dall'archiviazione toopremium standard. dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium. Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Convertire un disco gestito da toopremium standard e viceversa

Il carico di lavoro di sviluppo/test, è consigliabile toohave combinazione di dischi standard e premium tooreduce i costi. È possibile ottenere questo risultato con l'aggiornamento di archiviazione toopremium, solo i dischi di hello che richiedono prestazioni migliori. Nell'esempio seguente di hello, ecco come tooswitch un singolo disco di una macchina virtuale dall'archiviazione toopremium standard e viceversa. dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium. Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.

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

## <a name="next-steps"></a>Passaggi successivi

Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).

