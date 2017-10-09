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
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="08e13-103">Aumento hello dimensioni di un disco dati collegato tooa macchina virtuale di Windows</span><span class="sxs-lookup"><span data-stu-id="08e13-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="08e13-104">Se è necessario dimensioni hello tooincrease della macchina virtuale tooyour di hello dati disco collegato, è possibile aumentare la dimensione di hello utilizzando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08e13-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="08e13-105">Dopo aver aumentato dimensioni hello del disco dati hello nelle impostazioni di hello macchina virtuale di Azure, è necessario anche tooallocate hello nuovo spazio su disco all'interno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="08e13-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="08e13-106">Utilizzare Powershell tooincrease hello dimensioni di un disco dati gestiti</span><span class="sxs-lookup"><span data-stu-id="08e13-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="08e13-107">dimensioni di hello tooincrease di un disco dati gestiti, hello di utilizzare i cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="08e13-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="08e13-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="08e13-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="08e13-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="08e13-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="08e13-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="08e13-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="08e13-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="08e13-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="08e13-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="08e13-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="08e13-113">Hello lo script seguente assiste l'utente tramite il recupero di informazioni di VM hello, selezionare il disco di dati hello e specificando nuove dimensioni hello.</span><span class="sxs-lookup"><span data-stu-id="08e13-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="08e13-114">Utilizzare PowerShell tooincrease hello dimensioni di un disco dati non gestiti</span><span class="sxs-lookup"><span data-stu-id="08e13-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="08e13-115">dimensione di hello tooincrease dei dischi di dati non gestiti in un account di archiviazione, hello di utilizzare i cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="08e13-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="08e13-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="08e13-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="08e13-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="08e13-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="08e13-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="08e13-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="08e13-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="08e13-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="08e13-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="08e13-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="08e13-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="08e13-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="08e13-122">Hello script riportato di seguito consentono di recupero di informazioni di account hello macchina virtuale e archiviazione, selezionare il disco di dati hello e specificando nuove dimensioni hello.</span><span class="sxs-lookup"><span data-stu-id="08e13-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="08e13-123">Allocare spazio su disco non allocato hello</span><span class="sxs-lookup"><span data-stu-id="08e13-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="08e13-124">Dopo avere apportato unità hello più grande, è necessario tooallocate hello nuovo spazio non allocato all'interno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="08e13-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="08e13-125">spazio di hello tooallocate, è possibile connettere utilizzare VM toohello Gestione disco (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="08e13-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="08e13-126">In alternativa, se è abilitato gestione remota Windows e un certificato su hello VM quando è stato creato, è possibile utilizzare un disco di hello tooinitialize PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="08e13-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="08e13-127">È anche possibile usare un'estensione di script personalizzata:</span><span class="sxs-lookup"><span data-stu-id="08e13-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="08e13-128">file di script Hello può contenere un risultato simile a questo codice tooincrease hello unità allocazione toohello massimo hello dischi con dimensioni:</span><span class="sxs-lookup"><span data-stu-id="08e13-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="08e13-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08e13-129">Next Steps</span></span>
- [<span data-ttu-id="08e13-130">Altre informazioni su dischi e dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="08e13-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
