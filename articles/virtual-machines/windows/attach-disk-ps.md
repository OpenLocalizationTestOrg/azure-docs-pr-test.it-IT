---
title: Collegare un disco dati a una macchina virtuale Windows in Azure con PowerShell | Documentazione Microsoft
description: Come collegare un disco dati nuovo o esistente a una macchina virtuale Windows con PowerShell tramite il modello di distribuzione di Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="0eb4d-103">Collegare un disco dati a una macchina virtuale Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0eb4d-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="0eb4d-104">Questo articolo illustra come collegare dischi nuovi o esistenti a una macchina virtuale Windows tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="0eb4d-105">Se la macchina virtuale usa dischi gestiti, è possibile collegare dischi dati gestiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="0eb4d-106">È anche possibile collegare dischi dati non gestiti in una macchina virtuale che usa dischi non gestiti in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="0eb4d-107">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0eb4d-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="0eb4d-108">La dimensione della macchina virtuale controlla il numero di dischi dati che è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="0eb4d-109">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0eb4d-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="0eb4d-110">Per usare l'Archiviazione Premium, è necessario usare una macchina virtuale abilitata per l'Archiviazione Premium di dimensioni simili a una macchina virtuale della serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="0eb4d-111">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="0eb4d-112">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="0eb4d-113">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0eb4d-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0eb4d-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0eb4d-114">Before you begin</span></span>
<span data-ttu-id="0eb4d-115">Se si usa PowerShell, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="0eb4d-116">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="0eb4d-117">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0eb4d-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="0eb4d-118">Aggiungere un disco dati vuoto a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0eb4d-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="0eb4d-119">Questo esempio illustra come aggiungere un disco dati vuoto a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="0eb4d-120">Uso di Managed Disks</span><span class="sxs-lookup"><span data-stu-id="0eb4d-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="0eb4d-121">Uso di dischi non gestiti in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0eb4d-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="0eb4d-122">Inizializzare il disco</span><span class="sxs-lookup"><span data-stu-id="0eb4d-122">Initialize the disk</span></span>

<span data-ttu-id="0eb4d-123">Dopo aver aggiunto un disco vuoto, è necessario inizializzarlo.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="0eb4d-124">Per inizializzare il disco, è possibile accedere alla macchina virtuale e usare la gestione del disco.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="0eb4d-125">Se è stata abilitata l'installazione di WinRM e di un certificato durante la creazione della macchina virtuale, è possibile usare PowerShell remoto per inizializzare il disco.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="0eb4d-126">È anche possibile usare un'estensione di script personalizzata:</span><span class="sxs-lookup"><span data-stu-id="0eb4d-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="0eb4d-127">Il file di script può contenere codice analogo al seguente per inizializzare i dischi:</span><span class="sxs-lookup"><span data-stu-id="0eb4d-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="0eb4d-128">Collegare un disco dati esistente a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0eb4d-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="0eb4d-129">È anche possibile collegare un disco rigido virtuale esistente come disco dati gestito a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0eb4d-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="0eb4d-130">Uso di Managed Disks</span><span class="sxs-lookup"><span data-stu-id="0eb4d-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="0eb4d-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0eb4d-131">Next steps</span></span>

<span data-ttu-id="0eb4d-132">Creare uno [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="0eb4d-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
