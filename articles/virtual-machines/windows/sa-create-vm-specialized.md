---
title: aaaCreate macchina virtuale da un disco specializzato in Azure | Documenti Microsoft
description: Creare una nuova macchina virtuale collegando un disco specializzato non gestito, nel modello di distribuzione di gestione risorse di hello.
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="26683-103">Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="26683-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="26683-104">Creare una nuova macchina virtuale collegando un disco specializzato non gestito come disco del sistema operativo hello tramite Powershell.</span><span class="sxs-lookup"><span data-stu-id="26683-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="26683-105">Un disco specializzato è una copia del disco rigido virtuale da una macchina virtuale esistente che gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="26683-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="26683-106">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="26683-106">You have two options:</span></span>
* [<span data-ttu-id="26683-107">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="26683-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="26683-108">Copiare hello VHD di una macchina virtuale di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="26683-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="26683-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="26683-109">Before you begin</span></span>
<span data-ttu-id="26683-110">Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="26683-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="26683-111">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="26683-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="26683-112">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26683-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="26683-113">Opzione 1: Caricare un disco rigido virtuale specializzato</span><span class="sxs-lookup"><span data-stu-id="26683-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="26683-114">È possibile caricare hello che disco rigido virtuale da una VM specializzata creato con uno strumento di virtualizzazione locale, come Hyper-V, o una macchina virtuale esportata da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="26683-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="26683-115">Preparare hello VM</span><span class="sxs-lookup"><span data-stu-id="26683-115">Prepare hello VM</span></span>
<span data-ttu-id="26683-116">È possibile caricare un disco rigido virtuale specializzato creato usando una VM locale o un disco rigido virtuale esportato da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="26683-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="26683-117">Un disco rigido virtuale specializzato gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="26683-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="26683-118">Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata.</span><span class="sxs-lookup"><span data-stu-id="26683-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="26683-119">[Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26683-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="26683-120">**Non** generalizzare hello macchina virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="26683-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="26683-121">Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware).</span><span class="sxs-lookup"><span data-stu-id="26683-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="26683-122">Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP.</span><span class="sxs-lookup"><span data-stu-id="26683-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="26683-123">Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio.</span><span class="sxs-lookup"><span data-stu-id="26683-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="26683-124">Ottenere l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="26683-124">Get hello storage account</span></span>
<span data-ttu-id="26683-125">È necessario un account di archiviazione nell'immagine di macchina virtuale di Azure toostore hello caricato.</span><span class="sxs-lookup"><span data-stu-id="26683-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="26683-126">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="26683-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="26683-127">account di archiviazione disponibili hello tooshow, digitare:</span><span class="sxs-lookup"><span data-stu-id="26683-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="26683-128">Se si desidera toouse un account di archiviazione esistente, procedere toohello [immagine di macchina virtuale di caricamento hello](#upload-the-vm-vhd-to-your-storage-account) sezione.</span><span class="sxs-lookup"><span data-stu-id="26683-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="26683-129">Se è necessario un account di archiviazione toocreate, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="26683-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="26683-130">È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="26683-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="26683-131">toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:</span><span class="sxs-lookup"><span data-stu-id="26683-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="26683-132">un gruppo di risorse denominato toocreate **myResourceGroup** in hello **Stati Uniti occidentali** area, digitare:</span><span class="sxs-lookup"><span data-stu-id="26683-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="26683-133">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="26683-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="26683-134">Caricare l'account di archiviazione tooyour hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="26683-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="26683-135">Hello utilizzare [Aggiungi AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello tooa il contenitore di immagini nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="26683-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="26683-136">In questo esempio caricamenti hello file **myVHD.vhd** da `"C:\Users\Public\Documents\Virtual hard disks\"` tooa account di archiviazione denominato **mystorageaccount** in hello **myResourceGroup** gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="26683-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="26683-137">sarà inseriti file Hello contenitore hello denominato **mycontainer** e sarà il nuovo nome di file hello **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="26683-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="26683-138">Se ha esito positivo, si otterrà una risposta simile toothis simile:</span><span class="sxs-lookup"><span data-stu-id="26683-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="26683-139">La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete.</span><span class="sxs-lookup"><span data-stu-id="26683-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="26683-140">Opzione 2: Copiare hello disco rigido virtuale da una macchina virtuale di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="26683-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="26683-141">È possibile copiare un account toouse di disco rigido virtuale tooanother archiviazione durante la creazione di una macchina virtuale nuova, duplicata.</span><span class="sxs-lookup"><span data-stu-id="26683-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="26683-142">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="26683-142">Before you begin</span></span>
<span data-ttu-id="26683-143">Verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="26683-143">Make sure that you:</span></span>

* <span data-ttu-id="26683-144">Informazioni hello **gli account di archiviazione di origine e destinazione**.</span><span class="sxs-lookup"><span data-stu-id="26683-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="26683-145">Per la macchina virtuale di origine hello, è necessario toohave hello archiviazione nomi account e contenitore.</span><span class="sxs-lookup"><span data-stu-id="26683-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="26683-146">In genere, si sarà il nome di contenitore hello **dischi rigidi virtuali**.</span><span class="sxs-lookup"><span data-stu-id="26683-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="26683-147">È inoltre necessario toohave un account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="26683-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="26683-148">Se non hai già uno, è possibile crearne uno usando portale hello (**più servizi** > gli account di archiviazione > Aggiungi) o tramite hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="26683-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="26683-149">Aver scaricato e installato hello [strumento AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="26683-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="26683-150">Deallocare hello VM</span><span class="sxs-lookup"><span data-stu-id="26683-150">Deallocate hello VM</span></span>
<span data-ttu-id="26683-151">Dealloca hello VM, che consente di liberare hello toobe di disco rigido virtuale copiato.</span><span class="sxs-lookup"><span data-stu-id="26683-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="26683-152">**Portale**: fare clic su  **Macchine virtuali** > **myVM** &gt; Stop (Termina)</span><span class="sxs-lookup"><span data-stu-id="26683-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="26683-153">**PowerShell**: utilizzare [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocazione) hello macchina virtuale denominata **myVM** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="26683-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="26683-154">Hello **stato** per Ciao VM hello Azure portal cambia da **arrestato** troppo**arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="26683-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="26683-155">Ottenere l'URL di account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="26683-155">Get hello storage account URLs</span></span>
<span data-ttu-id="26683-156">È necessario hello gli URL di account di archiviazione di origine e destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="26683-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="26683-157">Hello URL simile a: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="26683-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="26683-158">Se si conosce già nome account e il contenitore di archiviazione hello, è possibile solo sostituire informazioni hello tra hello tra parentesi quadre toocreate l'URL.</span><span class="sxs-lookup"><span data-stu-id="26683-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="26683-159">È possibile utilizzare hello portale di Azure o Azure Powershell tooget hello URL:</span><span class="sxs-lookup"><span data-stu-id="26683-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="26683-160">**Portale**: fare clic su hello  **>**  per **più servizi** > **gli account di archiviazione**  >   *account di archiviazione* > **BLOB** e il file VHD di origine è probabilmente in hello **dischi rigidi virtuali** contenitore.</span><span class="sxs-lookup"><span data-stu-id="26683-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="26683-161">Fare clic su **proprietà** per il contenitore di hello e copiare il testo hello etichetta **URL**.</span><span class="sxs-lookup"><span data-stu-id="26683-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="26683-162">È necessario che gli URL di hello di contenitori di origine e di destinazione sia hello.</span><span class="sxs-lookup"><span data-stu-id="26683-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="26683-163">**PowerShell**: utilizzare [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) informazioni hello tooget per macchina virtuale denominata **myVM** nel gruppo di risorse hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="26683-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="26683-164">Nei risultati di hello, Cerca in hello **profilo di archiviazione** sezione per hello **Vhd Uri**.</span><span class="sxs-lookup"><span data-stu-id="26683-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="26683-165">prima parte di Hello di hello Uri hello URL toohello ed ultima parte hello hello Nome disco rigido virtuale del sistema operativo per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26683-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="26683-166">Ottiene le chiavi di accesso di hello archiviazione</span><span class="sxs-lookup"><span data-stu-id="26683-166">Get hello storage access keys</span></span>
<span data-ttu-id="26683-167">Trova le chiavi di accesso hello per hello gli account di archiviazione di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="26683-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="26683-168">Per altre informazioni sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="26683-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="26683-169">**Portale**: fare clic su **Altri servizi** > **Account di archiviazione** > *account di archiviazione* > **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="26683-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="26683-170">Tasto di copia hello etichettata come **key1**.</span><span class="sxs-lookup"><span data-stu-id="26683-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="26683-171">**PowerShell**: utilizzare [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello archiviazione chiave hello account di archiviazione **mystorageaccount** nel gruppo di risorse hello  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="26683-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="26683-172">Chiave di hello copia con l'etichetta **key1**.</span><span class="sxs-lookup"><span data-stu-id="26683-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="26683-173">Copiare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="26683-173">Copy hello VHD</span></span>
<span data-ttu-id="26683-174">È possibile copiare file da un account di archiviazione a un altro usando AzCopy.</span><span class="sxs-lookup"><span data-stu-id="26683-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="26683-175">Per il contenitore di destinazione hello, se il contenitore di hello specificato non esiste, si verrà creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="26683-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="26683-176">toouse AzCopy, aprire un prompt dei comandi nel computer locale e passare toohello cartella in cui è installato AzCopy.</span><span class="sxs-lookup"><span data-stu-id="26683-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="26683-177">Sarà simile troppo*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="26683-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="26683-178">toocopy tutti hello file all'interno di un contenitore, utilizzare hello **/S** passare.</span><span class="sxs-lookup"><span data-stu-id="26683-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="26683-179">Può essere utilizzato toocopy hello disco rigido virtuale del sistema operativo e tutti i dischi di dati hello se sono presenti in hello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="26683-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="26683-180">Questo esempio viene illustrato come toocopy hello tutti i file nel contenitore hello **mysourcecontainer** nell'account di archiviazione **mysourcestorageaccount** toohello contenitore **mydestinationcontainer**  in hello **mydestinationstorageaccount** account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="26683-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="26683-181">Sostituire i nomi di hello di account di archiviazione hello e di contenitori con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="26683-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="26683-182">Sostituire `<sourceStorageAccountKey1>` e `<destinationStorageAccountKey1>` con chiavi a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="26683-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="26683-183">Se si vuole solo toocopy uno specifico VHD in un contenitore con più file, è possibile specificare anche il nome di file hello opzione /Pattern hello.</span><span class="sxs-lookup"><span data-stu-id="26683-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="26683-184">In questo esempio, solo hello file denominato **myFileName.vhd** verranno copiati.</span><span class="sxs-lookup"><span data-stu-id="26683-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="26683-185">Al termine verrà visualizzato un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="26683-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="26683-186">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="26683-186">Troubleshooting</span></span>
* <span data-ttu-id="26683-187">Quando si utilizza AZCopy, se viene visualizzato l'errore hello "Richiesta hello tooauthenticate Server non riuscita", verificare che il valore di hello dell'intestazione di autorizzazione hello è del formato corretto, inclusa la firma hello.</span><span class="sxs-lookup"><span data-stu-id="26683-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="26683-188">Se si utilizza 2 di chiave o una chiave di archiviazione secondaria hello, provare a usare la chiave di archiviazione primario o al 1 ° hello.</span><span class="sxs-lookup"><span data-stu-id="26683-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="26683-189">Creare hello nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="26683-189">Create hello new VM</span></span> 

<span data-ttu-id="26683-190">È necessario toocreate rete e altri toobe risorse macchina virtuale utilizzato da hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26683-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="26683-191">Creare reti virtuali e la subNet hello</span><span class="sxs-lookup"><span data-stu-id="26683-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="26683-192">Creare reti virtuali hello e la subNet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26683-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="26683-193">Creare subNet hello.</span><span class="sxs-lookup"><span data-stu-id="26683-193">Create hello subNet.</span></span> <span data-ttu-id="26683-194">Questo esempio viene creata una subnet denominata **mySubNet**, nel gruppo di risorse hello **myResourceGroup**, e set hello prefisso di indirizzo di subnet troppo**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="26683-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="26683-195">Creare una rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="26683-195">Create hello vNet.</span></span> <span data-ttu-id="26683-196">In questo esempio imposta hello toobe nome di rete virtuale **myVnetName**, hello percorso troppo**Stati Uniti occidentali**, e hello prefisso dell'indirizzo per la rete virtuale hello troppo**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="26683-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="26683-197">Creare un indirizzo IP pubblico e NIC</span><span class="sxs-lookup"><span data-stu-id="26683-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="26683-198">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="26683-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="26683-199">Creare l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="26683-199">Create hello public IP.</span></span> <span data-ttu-id="26683-200">In questo esempio, nome dell'indirizzo IP pubblico hello è troppo**myIP**.</span><span class="sxs-lookup"><span data-stu-id="26683-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="26683-201">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="26683-201">Create hello NIC.</span></span> <span data-ttu-id="26683-202">In questo esempio, il nome di interfaccia di rete hello è impostato troppo**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="26683-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="26683-203">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="26683-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="26683-204">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="26683-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="26683-205">Poiché hello disco rigido virtuale per la nuova macchina virtuale è stato creato da un oggetto esistente hello specializzato macchina virtuale, dopo aver creato hello VM, è possibile utilizzare un account esistente dalla macchina virtuale di origine hello che aveva toolog autorizzazione sull'utilizzo di RDP.</span><span class="sxs-lookup"><span data-stu-id="26683-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="26683-206">In questo esempio imposta hello Nome gruppo troppo**myNsg** e hello RDP troppo nome regola**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="26683-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="26683-207">Per ulteriori informazioni sugli endpoint e le regole di gruppo, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26683-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="26683-208">Nome della macchina virtuale hello e le dimensioni</span><span class="sxs-lookup"><span data-stu-id="26683-208">Set hello VM name and size</span></span>

<span data-ttu-id="26683-209">In questo esempio imposta hello nome della macchina virtuale troppo "myVM" e hello VM dimensione troppo "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="26683-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="26683-210">Aggiungere hello NIC</span><span class="sxs-lookup"><span data-stu-id="26683-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="26683-211">Configurare un disco del sistema operativo hello</span><span class="sxs-lookup"><span data-stu-id="26683-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="26683-212">Impostare hello URI per hello disco rigido virtuale che è stato caricato o copiato.</span><span class="sxs-lookup"><span data-stu-id="26683-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="26683-213">In questo esempio, i file di disco rigido virtuale denominato hello **myOsDisk.vhd** vengono mantenuti in un account di archiviazione denominato **myStorageAccount** in un contenitore denominato **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="26683-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="26683-214">Aggiungere il disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="26683-214">Add hello OS disk.</span></span> <span data-ttu-id="26683-215">In questo esempio, quando viene creata hello disco del sistema operativo, hello termine "osDisk" è appened toohello nome toocreate hello del sistema operativo disco nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26683-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="26683-216">In questo esempio specifica inoltre che il disco rigido virtuale basato su Windows deve essere collegato toohello macchina virtuale come disco di hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="26683-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="26683-217">Facoltativo: Se si dispone di dischi dati che toobe necessità collegato toohello VM, aggiungere dischi dati hello utilizzando gli URL dei dischi rigidi virtuali dati hello e hello i numero di unità logica (Lun) appropriati.</span><span class="sxs-lookup"><span data-stu-id="26683-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="26683-218">Quando si utilizza un account di archiviazione, dati hello e gli URL del disco del sistema operativo simile al seguente: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="26683-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="26683-219">È possibile trovare nel portale di hello visualizzando contenitore di archiviazione di destinazione toohello, facendo clic su sistema operativo hello o disco rigido virtuale che è stato copiato, dati e quindi copiando il contenuto di hello dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="26683-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="26683-220">Completare hello VM</span><span class="sxs-lookup"><span data-stu-id="26683-220">Complete hello VM</span></span> 

<span data-ttu-id="26683-221">Creare hello VM utilizzando le configurazioni di hello che abbiamo appena creato.</span><span class="sxs-lookup"><span data-stu-id="26683-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="26683-222">Se il comando ha esito positivo, viene visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="26683-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="26683-223">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="26683-223">Verify that hello VM was created</span></span>
<span data-ttu-id="26683-224">È consigliabile vedere hello appena creato VM in hello [portale di Azure](https://portal.azure.com), in **Sfoglia** > **macchine virtuali**, oppure utilizzando hello seguente PowerShell comandi:</span><span class="sxs-lookup"><span data-stu-id="26683-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="26683-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26683-225">Next steps</span></span>
<span data-ttu-id="26683-226">toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello.</span><span class="sxs-lookup"><span data-stu-id="26683-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="26683-227">Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26683-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="26683-228">Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="26683-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

