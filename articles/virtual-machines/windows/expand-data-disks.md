---
title: aaaExpand un disco dati collegato tooa macchina virtuale Windows in Azure | Documenti Microsoft
description: Espandere hello dimensioni di un disco dati collegato tooa macchina virtuale di Windows con PowerShell.
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a>Aumento hello dimensioni di un disco dati collegato tooa macchina virtuale di Windows

Se è necessario dimensioni hello tooincrease della macchina virtuale tooyour di hello dati disco collegato, è possibile aumentare la dimensione di hello utilizzando PowerShell. Dopo aver aumentato dimensioni hello del disco dati hello nelle impostazioni di hello macchina virtuale di Azure, è necessario anche tooallocate hello nuovo spazio su disco all'interno di hello macchina virtuale.


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a>Utilizzare Powershell tooincrease hello dimensioni di un disco dati gestiti

dimensioni di hello tooincrease di un disco dati gestiti, hello di utilizzare i cmdlet di PowerShell seguente:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [Update-AzureRmDisk](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Hello lo script seguente assiste l'utente tramite il recupero di informazioni di VM hello, selezionare il disco di dati hello e specificando nuove dimensioni hello.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a>Utilizzare PowerShell tooincrease hello dimensioni di un disco dati non gestiti

dimensione di hello tooincrease dei dischi di dati non gestiti in un account di archiviazione, hello di utilizzare i cmdlet di PowerShell seguente:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Hello script riportato di seguito consentono di recupero di informazioni di account hello macchina virtuale e archiviazione, selezionare il disco di dati hello e specificando nuove dimensioni hello.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a>Allocare spazio su disco non allocato hello

Dopo avere apportato unità hello più grande, è necessario tooallocate hello nuovo spazio non allocato all'interno di hello macchina virtuale. spazio di hello tooallocate, è possibile connettere utilizzare VM toohello Gestione disco (diskmgmt.msc). In alternativa, se è abilitato gestione remota Windows e un certificato su hello VM quando è stato creato, è possibile utilizzare un disco di hello tooinitialize PowerShell remoto. È anche possibile usare un'estensione di script personalizzata:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

file di script Hello può contenere un risultato simile a questo codice tooincrease hello unità allocazione toohello massimo hello dischi con dimensioni:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni su dischi e dischi rigidi virtuali](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
