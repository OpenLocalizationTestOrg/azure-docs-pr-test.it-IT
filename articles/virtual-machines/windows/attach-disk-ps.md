---
title: aaaAttach un tooa disco dati macchina virtuale di Windows in Azure tramite PowerShell | Documenti Microsoft
description: Funzionamento dei dischi dati nuovi o esistenti tooattach tooa macchina virtuale di Windows con PowerShell con modello di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="96c2a-103">Collegare un tooa disco dati macchina virtuale di Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="96c2a-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="96c2a-104">Questo articolo illustra come tooattach sia nuovi che esistenti dischi tooa macchina virtuale di Windows con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96c2a-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="96c2a-105">Se la macchina virtuale usa dischi gestiti, è possibile collegare dischi dati gestiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="96c2a-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="96c2a-106">È inoltre possibile collegare i dischi di dati non gestiti tooa macchina virtuale che utilizza dischi non gestiti in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="96c2a-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="96c2a-107">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="96c2a-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="96c2a-108">dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="96c2a-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="96c2a-109">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96c2a-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="96c2a-110">toouse archiviazione Premium, è necessario uno spazio di archiviazione Premium abilitato dimensioni della macchina virtuale come macchina virtuale serie DS o GS-series hello.</span><span class="sxs-lookup"><span data-stu-id="96c2a-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="96c2a-111">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="96c2a-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="96c2a-112">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="96c2a-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="96c2a-113">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96c2a-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96c2a-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="96c2a-114">Before you begin</span></span>
<span data-ttu-id="96c2a-115">Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="96c2a-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="96c2a-116">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="96c2a-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="96c2a-117">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96c2a-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="96c2a-118">Aggiungere una macchina virtuale di tooa disco dati vuoto</span><span class="sxs-lookup"><span data-stu-id="96c2a-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="96c2a-119">Questo esempio mostra come tooadd dati vuoti di un disco di macchina virtuale esistente tooan.</span><span class="sxs-lookup"><span data-stu-id="96c2a-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="96c2a-120">Uso di Managed Disks</span><span class="sxs-lookup"><span data-stu-id="96c2a-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="96c2a-121">Uso di dischi non gestiti in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="96c2a-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="96c2a-122">Inizializzare il disco hello</span><span class="sxs-lookup"><span data-stu-id="96c2a-122">Initialize hello disk</span></span>

<span data-ttu-id="96c2a-123">Dopo aver aggiunto un disco vuoto, è necessario tooinitialize è.</span><span class="sxs-lookup"><span data-stu-id="96c2a-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="96c2a-124">disco hello tooinitialize, è possibile accedere in Gestione disco macchina virtuale e l'utilizzo di tooa.</span><span class="sxs-lookup"><span data-stu-id="96c2a-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="96c2a-125">Se è abilitato gestione remota Windows e un certificato su hello VM quando è stato creato, è possibile utilizzare disco hello tooinitialize di PowerShell remoto.</span><span class="sxs-lookup"><span data-stu-id="96c2a-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="96c2a-126">È anche possibile usare un'estensione di script personalizzata:</span><span class="sxs-lookup"><span data-stu-id="96c2a-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="96c2a-127">file di script Hello può contenere elementi come i dischi di hello tooinitialize questo codice:</span><span class="sxs-lookup"><span data-stu-id="96c2a-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="96c2a-128">Collegare un tooa di disco dati macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="96c2a-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="96c2a-129">È anche possibile collegare un disco rigido virtuale esistente come macchina virtuale tooa disco dati gestiti.</span><span class="sxs-lookup"><span data-stu-id="96c2a-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="96c2a-130">Uso di Managed Disks</span><span class="sxs-lookup"><span data-stu-id="96c2a-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="96c2a-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96c2a-131">Next steps</span></span>

<span data-ttu-id="96c2a-132">Creare uno [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="96c2a-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
