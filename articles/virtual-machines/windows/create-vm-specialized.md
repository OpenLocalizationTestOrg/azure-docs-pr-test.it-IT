---
title: Creare una macchina virtuale Windows da un disco rigido virtuale specializzato in Azure | Microsoft Docs
description: Creare una nuova macchina virtuale Windows collegando un disco gestito specializzato come disco del sistema operativo usando il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="61e97-103">Creare una macchina virtuale Windows da un disco specializzato</span><span class="sxs-lookup"><span data-stu-id="61e97-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="61e97-104">Creare una nuova macchina virtuale collegando un disco gestito specializzato come disco del sistema operativo con Powershell.</span><span class="sxs-lookup"><span data-stu-id="61e97-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="61e97-105">Un disco specializzato è una copia del disco rigido virtuale proveniente da una macchina virtuale esistente che gestisce gli account utente, le applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="61e97-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="61e97-106">Quando si usa un disco rigido virtuale specializzato per creare una nuova VM, la nuova VM mantiene il nome computer della VM originale.</span><span class="sxs-lookup"><span data-stu-id="61e97-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="61e97-107">Vengono mantenute anche altre informazioni specifiche del computer e, in alcuni casi, queste informazioni duplicate possono causare problemi.</span><span class="sxs-lookup"><span data-stu-id="61e97-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="61e97-108">Quando si copia una VM, tenere presente quali tipi di informazioni specifiche del computer vengono usate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="61e97-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="61e97-109">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="61e97-109">You have two options:</span></span>
* [<span data-ttu-id="61e97-110">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="61e97-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="61e97-111">Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="61e97-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="61e97-112">Questo argomento illustra come usare i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="61e97-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="61e97-113">Se è presente una distribuzione legacy che richiede l'uso di un account di archiviazione, vedere [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="61e97-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="61e97-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="61e97-114">Before you begin</span></span>
<span data-ttu-id="61e97-115">Se si usa PowerShell, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="61e97-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="61e97-116">Per altre informazioni, vedere [Azure PowerShell Versioning](/powershell/azure/overview) (Controllo delle versioni di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="61e97-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="61e97-117">Opzione 1: Caricare un disco rigido virtuale specializzato</span><span class="sxs-lookup"><span data-stu-id="61e97-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="61e97-118">È possibile caricare il disco rigido virtuale da una VM specializzata creata con uno strumento di virtualizzazione locale, ad esempio Hyper-V, o da una VM esportata da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="61e97-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="61e97-119">Preparare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="61e97-119">Prepare the VM</span></span>
<span data-ttu-id="61e97-120">Se si intende usare il disco rigido virtuale così come è per creare una nuova macchina virtuale, assicurare il completamento delle operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="61e97-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="61e97-121">[Preparare un disco rigido virtuale (VHD) di Windows per il caricamento in Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61e97-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="61e97-122">**Non** generalizzare la macchina Virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="61e97-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="61e97-123">Rimuovere tutti gli strumenti di virtualizzazione guest e gli agenti installati nella macchina virtuale, ad esempio gli strumenti VMware.</span><span class="sxs-lookup"><span data-stu-id="61e97-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="61e97-124">Assicurarsi che la macchina virtuale sia configurata per eseguire il pull dell'indirizzo IP e delle impostazioni DNS tramite DHCP.</span><span class="sxs-lookup"><span data-stu-id="61e97-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="61e97-125">In questo modo il server ottiene un indirizzo IP all'interno della rete virtuale all'avvio.</span><span class="sxs-lookup"><span data-stu-id="61e97-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="61e97-126">Ottenere l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="61e97-126">Get the storage account</span></span>
<span data-ttu-id="61e97-127">Per archiviare il disco rigido virtuale caricato, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="61e97-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="61e97-128">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="61e97-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="61e97-129">Per mostrare gli account di archiviazione disponibili, digitare:</span><span class="sxs-lookup"><span data-stu-id="61e97-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="61e97-130">Per usare un account di archiviazione esistente, passare alla sezione [Caricare il disco rigido virtuale](#upload-the-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="61e97-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="61e97-131">Per creare un account di archiviazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="61e97-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="61e97-132">È necessario il nome del gruppo di risorse in cui deve essere creato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="61e97-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="61e97-133">Per trovare tutti i gruppi di risorse inclusi nella sottoscrizione digitare:</span><span class="sxs-lookup"><span data-stu-id="61e97-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="61e97-134">Per creare un gruppo di risorse denominato *MyResourceGroup* nell'area *Stati Uniti occidentali*, digitare:</span><span class="sxs-lookup"><span data-stu-id="61e97-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="61e97-135">Creare un account di archiviazione denominato *mystorageaccount* in questo gruppo di risorse con il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="61e97-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="61e97-136">Caricare il disco rigido virtuale nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="61e97-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="61e97-137">Usare il cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) per caricare il disco rigido virtuale in un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="61e97-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="61e97-138">In questo esempio, il file *myVHD.vhd* viene caricato da `"C:\Users\Public\Documents\Virtual hard disks\"` a un account di archiviazione denominato *mystorageaccount* nel gruppo di risorse *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="61e97-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="61e97-139">Il file viene archiviato nel contenitore denominato *mycontainer* e il nuovo nome del file sarà *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="61e97-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="61e97-140">Se l'operazione riesce, si ottiene una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="61e97-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="61e97-141">L'esecuzione del comando potrebbe richiedere del tempo, a seconda della connessione di rete e delle dimensioni del file VHD.</span><span class="sxs-lookup"><span data-stu-id="61e97-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="61e97-142">Creare un disco gestito dal disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="61e97-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="61e97-143">Creare un disco gestito dal disco rigido virtuale specializzato nell'account di archiviazione usando [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="61e97-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="61e97-144">Questo esempio usa **myOSDisk1** come nome del disco, inserisce il disco nella risorsa di archiviazione *StandardLRS* e usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* come URI per il disco rigido virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="61e97-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="61e97-145">Creare un nuovo gruppo di risorse per la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="61e97-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="61e97-146">Creare il nuovo disco del sistema operativo dal disco rigido virtuale caricato.</span><span class="sxs-lookup"><span data-stu-id="61e97-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="61e97-147">Opzione 2: Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="61e97-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="61e97-148">È possibile creare una copia di una VM che usa dischi gestiti acquisendo uno snapshot della VM, quindi usando tale snapshot per creare un nuovo disco gestito e una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="61e97-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="61e97-149">Acquisire uno snapshot del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="61e97-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="61e97-150">È possibile acquisire uno snapshot di un'intera VM (tutti i dischi inclusi) o solo di un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="61e97-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="61e97-151">I passaggi seguenti illustrano come acquisire uno snapshot solo del disco del sistema operativo della VM usando il cmdlet [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot).</span><span class="sxs-lookup"><span data-stu-id="61e97-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="61e97-152">Impostare alcuni parametri.</span><span class="sxs-lookup"><span data-stu-id="61e97-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="61e97-153">Ottenere l'oggetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="61e97-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="61e97-154">Ottenere il nome del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="61e97-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="61e97-155">Creare la configurazione dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="61e97-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="61e97-156">Ottenere lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="61e97-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="61e97-157">Se si prevede di usare lo snapshot per creare una macchina virtuale a prestazioni elevate, usare il parametro `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="61e97-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="61e97-158">Il parametro crea lo snapshot in modo tale che venga archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="61e97-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="61e97-159">I dischi gestiti Premium sono più costosi di quelli Standard.</span><span class="sxs-lookup"><span data-stu-id="61e97-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="61e97-160">Assicurarsi quindi che l'opzione Premium sia realmente necessaria prima di usare il parametro.</span><span class="sxs-lookup"><span data-stu-id="61e97-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="61e97-161">Creare un nuovo disco dallo snapshot</span><span class="sxs-lookup"><span data-stu-id="61e97-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="61e97-162">Creare un disco gestito dallo snapshot usando [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="61e97-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="61e97-163">Questo esempio usa *myOSDisk* come nome del disco.</span><span class="sxs-lookup"><span data-stu-id="61e97-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="61e97-164">Creare un nuovo gruppo di risorse per la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="61e97-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="61e97-165">Impostare il nome del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="61e97-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="61e97-166">Creare il disco gestito.</span><span class="sxs-lookup"><span data-stu-id="61e97-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="61e97-167">Creare la nuova VM</span><span class="sxs-lookup"><span data-stu-id="61e97-167">Create the new VM</span></span> 

<span data-ttu-id="61e97-168">Creare le risorse di rete e le altre risorse da usare nella nuova VM.</span><span class="sxs-lookup"><span data-stu-id="61e97-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="61e97-169">Creare la subNet e la vNet</span><span class="sxs-lookup"><span data-stu-id="61e97-169">Create the subNet and vNet</span></span>

<span data-ttu-id="61e97-170">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61e97-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="61e97-171">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="61e97-171">Create the subNet.</span></span> <span data-ttu-id="61e97-172">In questo esempio viene creata una subnet denominata **mySubNet** nel gruppo di risorse **myDestinationResourceGroup** e il prefisso dell'indirizzo della subnet viene impostato su **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="61e97-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="61e97-173">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="61e97-173">Create the vNet.</span></span> <span data-ttu-id="61e97-174">In questo esempio il nome della rete virtuale è **myVnetName**, la posizione specificata è **Stati Uniti occidentali** e il prefisso dell'indirizzo per la rete virtuale è **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="61e97-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="61e97-175">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="61e97-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="61e97-176">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="61e97-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="61e97-177">Poiché il disco rigido virtuale per la nuova macchina virtuale è stato creato da una VM specializzata esistente, è possibile usare un account della macchina virtuale di origine per RDP.</span><span class="sxs-lookup"><span data-stu-id="61e97-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="61e97-178">In questo esempio il nome NSG impostato è **myNsg**, mentre il nome della regola RDP è **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="61e97-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="61e97-179">Per altre informazioni sugli endpoint e sulle regole NSG, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61e97-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="61e97-180">Creare un indirizzo IP pubblico e NIC</span><span class="sxs-lookup"><span data-stu-id="61e97-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="61e97-181">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="61e97-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="61e97-182">Creare l'IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="61e97-182">Create the public IP.</span></span> <span data-ttu-id="61e97-183">In questo esempio, il nome dell'indirizzo IP pubblico è **myIP**.</span><span class="sxs-lookup"><span data-stu-id="61e97-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="61e97-184">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="61e97-184">Create the NIC.</span></span> <span data-ttu-id="61e97-185">In questo esempio, il nome specificato della scheda NIC è **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="61e97-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="61e97-186">Impostare il nome e le dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="61e97-186">Set the VM name and size</span></span>

<span data-ttu-id="61e97-187">Questo esempio imposta il nome della macchina virtuale su *myVM* e le dimensioni su *Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="61e97-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="61e97-188">Aggiungere la scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="61e97-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="61e97-189">Aggiungere il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="61e97-189">Add the OS disk</span></span> 

<span data-ttu-id="61e97-190">Aggiungere il disco del sistema operativo alla configurazione usando [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="61e97-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="61e97-191">In questo esempio le dimensioni del disco vengono impostate su *128 GB* e viene collegato il disco gestito come disco del sistema operativo *Windows*.</span><span class="sxs-lookup"><span data-stu-id="61e97-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="61e97-192">Completare la VM</span><span class="sxs-lookup"><span data-stu-id="61e97-192">Complete the VM</span></span> 

<span data-ttu-id="61e97-193">Creare la macchina virtuale usando le configurazioni [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm) appena create.</span><span class="sxs-lookup"><span data-stu-id="61e97-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="61e97-194">Se il comando ha esito positivo, viene visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="61e97-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="61e97-195">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="61e97-195">Verify that the VM was created</span></span>
<span data-ttu-id="61e97-196">La VM appena creata verrà visualizzata nel [portale di Azure](https://portal.azure.com) in **Sfoglia** > **Macchine virtuali** oppure usando i comandi di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="61e97-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="61e97-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61e97-197">Next steps</span></span>
<span data-ttu-id="61e97-198">Per accedere alla nuova macchina virtuale, passare alla VM nel [portale](https://portal.azure.com), fare clic su **Connetti**e aprire il file RDP di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="61e97-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="61e97-199">Usare le credenziali dell'account della macchina virtuale originale per accedere alla nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="61e97-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="61e97-200">Per altre informazioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="61e97-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

