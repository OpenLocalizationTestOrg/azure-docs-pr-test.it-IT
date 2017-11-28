---
title: una macchina virtuale Windows da un VHD in Azure specializzato aaaCreate | Documenti Microsoft
description: Creare una nuova macchina virtuale Windows collegando un disco specializzato gestito come disco del sistema operativo hello utilizzo nel modello di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="67b95-103">Creare una macchina virtuale Windows da un disco specializzato</span><span class="sxs-lookup"><span data-stu-id="67b95-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="67b95-104">Creare una nuova macchina virtuale collegando un disco specializzato gestito come disco del sistema operativo hello tramite Powershell.</span><span class="sxs-lookup"><span data-stu-id="67b95-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="67b95-105">Un disco specializzato è una copia del disco rigido virtuale (VHD) da una macchina virtuale esistente che gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="67b95-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="67b95-106">Quando si utilizza un toocreate VHD specializzata di una nuova macchina virtuale, hello nuova macchina virtuale mantiene il nome del computer hello hello macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="67b95-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="67b95-107">Vengono mantenute anche altre informazioni specifiche del computer e, in alcuni casi, queste informazioni duplicate possono causare problemi.</span><span class="sxs-lookup"><span data-stu-id="67b95-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="67b95-108">Quando si copia una VM, tenere presente quali tipi di informazioni specifiche del computer vengono usate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="67b95-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="67b95-109">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="67b95-109">You have two options:</span></span>
* [<span data-ttu-id="67b95-110">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="67b95-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="67b95-111">Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="67b95-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="67b95-112">Questo argomento viene illustrato come toouse dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="67b95-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="67b95-113">Se è presente una distribuzione legacy che richiede l'uso di un account di archiviazione, vedere [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="67b95-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="67b95-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="67b95-114">Before you begin</span></span>
<span data-ttu-id="67b95-115">Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="67b95-116">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67b95-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="67b95-117">Opzione 1: Caricare un disco rigido virtuale specializzato</span><span class="sxs-lookup"><span data-stu-id="67b95-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="67b95-118">È possibile caricare hello che disco rigido virtuale da una VM specializzata creato con uno strumento di virtualizzazione locale, come Hyper-V, o una macchina virtuale esportata da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="67b95-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="67b95-119">Preparare hello VM</span><span class="sxs-lookup"><span data-stu-id="67b95-119">Prepare hello VM</span></span>
<span data-ttu-id="67b95-120">Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata.</span><span class="sxs-lookup"><span data-stu-id="67b95-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="67b95-121">[Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67b95-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="67b95-122">**Non** generalizzare hello macchina virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="67b95-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="67b95-123">Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware).</span><span class="sxs-lookup"><span data-stu-id="67b95-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="67b95-124">Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP.</span><span class="sxs-lookup"><span data-stu-id="67b95-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="67b95-125">Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio.</span><span class="sxs-lookup"><span data-stu-id="67b95-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="67b95-126">Ottenere l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="67b95-126">Get hello storage account</span></span>
<span data-ttu-id="67b95-127">È necessario uno spazio di archiviazione account in Azure toostore hello caricato disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="67b95-128">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="67b95-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="67b95-129">account di archiviazione disponibili hello tooshow, digitare:</span><span class="sxs-lookup"><span data-stu-id="67b95-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="67b95-130">Se si desidera toouse un account di archiviazione esistente, procedere toohello [hello caricamento VHD](#upload-the-vhd-to-your-storage-account) sezione.</span><span class="sxs-lookup"><span data-stu-id="67b95-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="67b95-131">Se è necessario un account di archiviazione toocreate, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="67b95-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="67b95-132">È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="67b95-133">toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:</span><span class="sxs-lookup"><span data-stu-id="67b95-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="67b95-134">un gruppo di risorse denominato toocreate *myResourceGroup* in hello *Stati Uniti occidentali* area, digitare:</span><span class="sxs-lookup"><span data-stu-id="67b95-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="67b95-135">Creare un account di archiviazione denominato *mystorageaccount* in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="67b95-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="67b95-136">Caricare l'account di archiviazione tooyour hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="67b95-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="67b95-137">Hello utilizzare [Aggiungi AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) contenitore cmdlet tooupload hello VHD tooa nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67b95-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="67b95-138">In questo esempio caricamenti hello file *myVHD.vhd* da `"C:\Users\Public\Documents\Virtual hard disks\"` tooa account di archiviazione denominato *mystorageaccount* in hello *myResourceGroup* gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="67b95-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="67b95-139">file Hello viene archiviato nel contenitore hello denominato *mycontainer* e sarà il nuovo nome di file hello *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="67b95-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="67b95-140">Se ha esito positivo, si otterrà una risposta simile toothis simile:</span><span class="sxs-lookup"><span data-stu-id="67b95-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="67b95-141">La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete</span><span class="sxs-lookup"><span data-stu-id="67b95-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="67b95-142">Creare un disco gestito da hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="67b95-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="67b95-143">Creare un disco gestito da hello specializzato di disco rigido virtuale in cui l'account di archiviazione utilizzando [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="67b95-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="67b95-144">Questo esempio viene utilizzato **myOSDisk1** per il nome del disco hello, inserisce hello disco *StandardLRS* archiviazione e utilizza *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* come hello URI per l'origine hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="67b95-145">Creare un nuovo gruppo di risorse per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="67b95-146">Creare nuovo disco del sistema operativo hello da hello caricato disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="67b95-147">Opzione 2: Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="67b95-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="67b95-148">È possibile creare una copia di una macchina virtuale che utilizza dischi gestiti da creare uno snapshot di hello VM, quindi utilizza tale toocreate snapshot un nuovo gestito disco e una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="67b95-149">Creare uno snapshot del disco del sistema operativo hello</span><span class="sxs-lookup"><span data-stu-id="67b95-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="67b95-150">È possibile acquisire uno snapshot di un'intera VM (tutti i dischi inclusi) o solo di un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="67b95-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="67b95-151">Hello passaggi seguenti viene illustrato come tootake uno snapshot di appena hello del sistema operativo disco di macchina virtuale utilizzando hello [New AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="67b95-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="67b95-152">Impostare alcuni parametri.</span><span class="sxs-lookup"><span data-stu-id="67b95-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="67b95-153">Ottenere l'oggetto macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="67b95-154">Ottenere il nome del disco hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="67b95-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="67b95-155">Creare hello snapshot configurazione.</span><span class="sxs-lookup"><span data-stu-id="67b95-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="67b95-156">Creare snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="67b95-157">Se si prevede di toouse hello snapshot toocreate una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="67b95-158">il parametro Hello Crea snapshot hello in modo che viene archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="67b95-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="67b95-159">I dischi gestiti Premium sono più costosi di quelli Standard.</span><span class="sxs-lookup"><span data-stu-id="67b95-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="67b95-160">Pertanto è necessario assicurarsi che occorre Premium prima di utilizzare il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="67b95-161">Creare un nuovo disco da snapshot hello</span><span class="sxs-lookup"><span data-stu-id="67b95-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="67b95-162">Creare un disco gestito da hello snapshot utilizzando [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="67b95-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="67b95-163">Questo esempio viene utilizzato *myOSDisk* per il nome del disco hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="67b95-164">Creare un nuovo gruppo di risorse per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="67b95-165">Impostare il nome del disco hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="67b95-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="67b95-166">Disco gestito hello creato.</span><span class="sxs-lookup"><span data-stu-id="67b95-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="67b95-167">Creare hello nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="67b95-167">Create hello new VM</span></span> 

<span data-ttu-id="67b95-168">Creare una rete e altri toobe risorse macchina virtuale utilizzato da hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="67b95-169">Creare reti virtuali e la subNet hello</span><span class="sxs-lookup"><span data-stu-id="67b95-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="67b95-170">Creare reti virtuali hello e la subNet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67b95-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="67b95-171">Creare subNet hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-171">Create hello subNet.</span></span> <span data-ttu-id="67b95-172">Questo esempio viene creata una subnet denominata **mySubNet**, nel gruppo di risorse hello **myDestinationResourceGroup**, e set hello prefisso di indirizzo di subnet troppo**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="67b95-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="67b95-173">Creare una rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-173">Create hello vNet.</span></span> <span data-ttu-id="67b95-174">In questo esempio imposta hello toobe nome di rete virtuale **myVnetName**, hello percorso troppo**Stati Uniti occidentali**, e hello prefisso dell'indirizzo per la rete virtuale hello troppo**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="67b95-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="67b95-175">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="67b95-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="67b95-176">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="67b95-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="67b95-177">Poiché hello VHD per hello nuova macchina virtuale è stato creato da una macchina virtuale specializzata esistente, è possibile utilizzare un account dalla macchina virtuale di origine hello per RDP.</span><span class="sxs-lookup"><span data-stu-id="67b95-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="67b95-178">In questo esempio imposta hello Nome gruppo troppo**myNsg** e hello RDP troppo nome regola**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="67b95-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="67b95-179">Per ulteriori informazioni sugli endpoint e le regole di gruppo, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67b95-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="67b95-180">Creare un indirizzo IP pubblico e NIC</span><span class="sxs-lookup"><span data-stu-id="67b95-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="67b95-181">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="67b95-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="67b95-182">Creare l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-182">Create hello public IP.</span></span> <span data-ttu-id="67b95-183">In questo esempio, nome dell'indirizzo IP pubblico hello è troppo**myIP**.</span><span class="sxs-lookup"><span data-stu-id="67b95-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="67b95-184">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-184">Create hello NIC.</span></span> <span data-ttu-id="67b95-185">In questo esempio, il nome di interfaccia di rete hello è impostato troppo**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="67b95-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="67b95-186">Nome della macchina virtuale hello e le dimensioni</span><span class="sxs-lookup"><span data-stu-id="67b95-186">Set hello VM name and size</span></span>

<span data-ttu-id="67b95-187">In questo esempio imposta hello nome della macchina virtuale troppo*myVM* e hello VM dimensioni troppo*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="67b95-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="67b95-188">Aggiungere hello NIC</span><span class="sxs-lookup"><span data-stu-id="67b95-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="67b95-189">Aggiungere il disco del sistema operativo hello</span><span class="sxs-lookup"><span data-stu-id="67b95-189">Add hello OS disk</span></span> 

<span data-ttu-id="67b95-190">Aggiungere hello del sistema operativo disco toohello configurazione tramite [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="67b95-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="67b95-191">In questo esempio imposta dimensioni hello del disco hello troppo*128 GB* e collega disco gestito di hello come un *Windows* disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="67b95-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="67b95-192">Completare hello VM</span><span class="sxs-lookup"><span data-stu-id="67b95-192">Complete hello VM</span></span> 

<span data-ttu-id="67b95-193">Creare hello VM utilizzando [New AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurazioni che abbiamo appena creato.</span><span class="sxs-lookup"><span data-stu-id="67b95-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="67b95-194">Se il comando ha esito positivo, viene visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="67b95-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="67b95-195">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="67b95-195">Verify that hello VM was created</span></span>
<span data-ttu-id="67b95-196">È consigliabile vedere hello appena creato VM in hello [portale di Azure](https://portal.azure.com), in **Sfoglia** > **macchine virtuali**, oppure utilizzando hello seguente PowerShell comandi:</span><span class="sxs-lookup"><span data-stu-id="67b95-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="67b95-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67b95-197">Next steps</span></span>
<span data-ttu-id="67b95-198">toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello.</span><span class="sxs-lookup"><span data-stu-id="67b95-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="67b95-199">Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67b95-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="67b95-200">Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="67b95-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

