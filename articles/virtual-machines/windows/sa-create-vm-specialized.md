---
title: Creare una macchina virtuale da un disco specializzato in Azure | Documentazione Microsoft
description: Creare una nuova macchina virtuale collegando un disco non gestito specializzato nel modello di distribuzione Resource Manager.
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
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="11dda-103">Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="11dda-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="11dda-104">Creare una nuova macchina virtuale collegando un disco non gestito specializzato come disco del sistema operativo con Powershell.</span><span class="sxs-lookup"><span data-stu-id="11dda-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="11dda-105">Un disco specializzato è una copia del disco rigido virtuale proveniente da una macchina virtuale esistente che gestisce gli account utente, le applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="11dda-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="11dda-106">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="11dda-106">You have two options:</span></span>
* [<span data-ttu-id="11dda-107">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="11dda-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="11dda-108">Copiare il disco rigido virtuale di una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="11dda-108">Copy the VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="11dda-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="11dda-109">Before you begin</span></span>
<span data-ttu-id="11dda-110">Se si usa PowerShell, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="11dda-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="11dda-111">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="11dda-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="11dda-112">Per altre informazioni, vedere [Azure PowerShell Versioning](/powershell/azure/overview) (Controllo delle versioni di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="11dda-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="11dda-113">Opzione 1: Caricare un disco rigido virtuale specializzato</span><span class="sxs-lookup"><span data-stu-id="11dda-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="11dda-114">È possibile caricare il disco rigido virtuale da una VM specializzata creata con uno strumento di virtualizzazione locale, ad esempio Hyper-V, o da una VM esportata da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="11dda-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="11dda-115">Preparare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="11dda-115">Prepare the VM</span></span>
<span data-ttu-id="11dda-116">È possibile caricare un disco rigido virtuale specializzato creato usando una VM locale o un disco rigido virtuale esportato da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="11dda-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="11dda-117">Un disco rigido virtuale specializzato gestisce gli account utente, le applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="11dda-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="11dda-118">Se si intende usare il disco rigido virtuale così come è per creare una nuova macchina virtuale, assicurare il completamento delle operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="11dda-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="11dda-119">[Preparare un disco rigido virtuale (VHD) di Windows per il caricamento in Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11dda-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="11dda-120">**Non** generalizzare la macchina Virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="11dda-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="11dda-121">Rimuovere tutti gli strumenti di virtualizzazione guest e gli agenti installati nella macchina virtuale, ad esempio gli strumenti VMware.</span><span class="sxs-lookup"><span data-stu-id="11dda-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="11dda-122">Assicurarsi che la macchina virtuale sia configurata per eseguire il pull dell'indirizzo IP e delle impostazioni DNS tramite DHCP.</span><span class="sxs-lookup"><span data-stu-id="11dda-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="11dda-123">In questo modo il server ottiene un indirizzo IP all'interno della rete virtuale all'avvio.</span><span class="sxs-lookup"><span data-stu-id="11dda-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="11dda-124">Ottenere l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="11dda-124">Get the storage account</span></span>
<span data-ttu-id="11dda-125">Per archiviare l'immagine della VM caricata, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="11dda-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="11dda-126">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="11dda-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="11dda-127">Per mostrare gli account di archiviazione disponibili, digitare:</span><span class="sxs-lookup"><span data-stu-id="11dda-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="11dda-128">Se si vuole usare un account di archiviazione esistente, passare alla sezione [Caricare l'immagine della VM](#upload-the-vm-vhd-to-your-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="11dda-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="11dda-129">Per creare un account di archiviazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="11dda-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="11dda-130">È necessario il nome del gruppo di risorse in cui deve essere creato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="11dda-131">Per trovare tutti i gruppi di risorse inclusi nella sottoscrizione digitare:</span><span class="sxs-lookup"><span data-stu-id="11dda-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="11dda-132">Per creare un gruppo di risorse denominato **MyResourceGroup** nell'area **Stati Uniti occidentali**, digitare:</span><span class="sxs-lookup"><span data-stu-id="11dda-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="11dda-133">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse con il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="11dda-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="11dda-134">Caricare il disco rigido virtuale nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="11dda-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="11dda-135">Usare il cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) per caricare l'immagine in un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="11dda-136">In questo esempio, il file **myVHD.vhd** viene caricato da `"C:\Users\Public\Documents\Virtual hard disks\"` a un account di archiviazione denominato **mystorageaccount** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="11dda-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="11dda-137">Il file viene inserito nel contenitore denominato **mycontainer** e il nuovo nome del file sarà **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="11dda-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="11dda-138">Se l'operazione riesce, si ottiene una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="11dda-138">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="11dda-139">L'esecuzione del comando potrebbe richiedere del tempo, a seconda della connessione di rete e delle dimensioni del file VHD.</span><span class="sxs-lookup"><span data-stu-id="11dda-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="11dda-140">Opzione 2: Copiare il disco rigido virtuale da una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="11dda-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="11dda-141">È possibile copiare un disco rigido virtuale in un altro account di archiviazione da usare quando si crea una nuova VM duplicata.</span><span class="sxs-lookup"><span data-stu-id="11dda-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="11dda-142">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="11dda-142">Before you begin</span></span>
<span data-ttu-id="11dda-143">Verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="11dda-143">Make sure that you:</span></span>

* <span data-ttu-id="11dda-144">Disporre delle informazioni sugli **account di archiviazione di origine e destinazione**.</span><span class="sxs-lookup"><span data-stu-id="11dda-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="11dda-145">Per la VM di origine è necessario disporre dei nomi degli account di archiviazione e dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="11dda-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="11dda-146">In genere il nome del contenitore sarà **vhds**.</span><span class="sxs-lookup"><span data-stu-id="11dda-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="11dda-147">È inoltre necessario disporre di un account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="11dda-148">Se non si dispone già di un account di archiviazione, è possibile crearne uno usando il portale (**Servizi** > Account di archiviazione > Aggiungi) oppure mediante il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="11dda-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="11dda-149">Avere scaricato e installato lo [strumento AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="11dda-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="11dda-150">Deallocare la VM</span><span class="sxs-lookup"><span data-stu-id="11dda-150">Deallocate the VM</span></span>
<span data-ttu-id="11dda-151">Deallocare la VM, operazione che consente di liberare il disco rigido virtuale da copiare.</span><span class="sxs-lookup"><span data-stu-id="11dda-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="11dda-152">**Portale**: fare clic su  **Macchine virtuali** > **myVM** > Stop (Termina)</span><span class="sxs-lookup"><span data-stu-id="11dda-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="11dda-153">**PowerShell**: usare [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) per arrestare (deallocare) la VM denominata **myVM** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="11dda-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="11dda-154">Nel portale di Azure lo **stato** della VM passa da **Arrestato** ad **Arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="11dda-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="11dda-155">Ottenere gli URL dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="11dda-155">Get the storage account URLs</span></span>
<span data-ttu-id="11dda-156">Sono necessari gli URL degli account di archiviazione di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="11dda-157">Gli URL hanno l'aspetto seguente: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="11dda-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="11dda-158">Se si conosce già il nome degli account di archiviazione e dei contenitori, per creare l'URL è sufficiente sostituire le informazioni tra parentesi.</span><span class="sxs-lookup"><span data-stu-id="11dda-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="11dda-159">Per ottenere l'URL è possibile usare il portale di Azure o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="11dda-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="11dda-160">**Portale**: fare clic su **>** per **Altri servizi** > **Account di archiviazione** > *account di archiviazione* > **BLOB**. Il file VHD di origine si trova probabilmente nel contenitore **vhds**.</span><span class="sxs-lookup"><span data-stu-id="11dda-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="11dda-161">Fare clic su **Proprietà** per il contenitore e copiare il testo con l'etichetta **URL**.</span><span class="sxs-lookup"><span data-stu-id="11dda-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="11dda-162">Sono necessari gli URL di entrambi i contenitori di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="11dda-163">**PowerShell**: usare [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) per ottenere le informazioni dalla VM denominata **myVM** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="11dda-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="11dda-164">Nei risultati esaminare la sezione **Storage profile** (Profilo archiviazione) per l'**URI VHD**.</span><span class="sxs-lookup"><span data-stu-id="11dda-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="11dda-165">La prima parte dell'URI è l'URL del contenitore, mentre l'ultima parte è il nome del disco rigido virtuale del sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="11dda-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="11dda-166">Ottenere le chiavi di accesso alle risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="11dda-166">Get the storage access keys</span></span>
<span data-ttu-id="11dda-167">Trovare le chiavi di accesso per gli account di archiviazione di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="11dda-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="11dda-168">Per altre informazioni sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="11dda-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="11dda-169">**Portale**: fare clic su **Altri servizi** > **Account di archiviazione** > *account di archiviazione* > **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="11dda-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="11dda-170">Copiare la chiave denominata **key1**.</span><span class="sxs-lookup"><span data-stu-id="11dda-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="11dda-171">**PowerShell**: usare [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) per ottenere la chiave di archiviazione per l'account di archiviazione **mystorageaccount** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="11dda-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="11dda-172">Copiare la chiave denominata **key1**.</span><span class="sxs-lookup"><span data-stu-id="11dda-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="11dda-173">Copiare il file VHD</span><span class="sxs-lookup"><span data-stu-id="11dda-173">Copy the VHD</span></span>
<span data-ttu-id="11dda-174">È possibile copiare file da un account di archiviazione a un altro usando AzCopy.</span><span class="sxs-lookup"><span data-stu-id="11dda-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="11dda-175">Se il container di destinazione specificato non esiste, tale contenitore verrà creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="11dda-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="11dda-176">Per usare AzCopy, aprire un prompt dei comandi sul computer locale e passare alla cartella in cui è installato tale strumento.</span><span class="sxs-lookup"><span data-stu-id="11dda-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="11dda-177">Il percorso sarà simile a *C:\Programmi (x86)\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="11dda-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="11dda-178">Per copiare tutti i file all'interno di un contenitore, è possibile usare l'opzione **/S**.</span><span class="sxs-lookup"><span data-stu-id="11dda-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="11dda-179">Può essere usata per copiare il disco rigido virtuale del sistema operativo e tutti i dischi dati che si trovano nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="11dda-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="11dda-180">Questo esempio mostra come copiare tutti i file che si trovano nel contenitore **mysourcecontainer** dell'account di archiviazione **mysourcestorageaccount** nel contenitore **mydestinationcontainer** dell'account di archiviazione **mydestinationstorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="11dda-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="11dda-181">Sostituire i nomi degli account di archiviazione e dei contenitori con nomi a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="11dda-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="11dda-182">Sostituire `<sourceStorageAccountKey1>` e `<destinationStorageAccountKey1>` con chiavi a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="11dda-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="11dda-183">Se si vuole copiare solo uno specifico file VHD in un contenitore con più file, è anche possibile specificare il nome del file usando l'opzione /Pattern.</span><span class="sxs-lookup"><span data-stu-id="11dda-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="11dda-184">In questo esempio verrà copiato solo il file denominato **myFileName.vhd**.</span><span class="sxs-lookup"><span data-stu-id="11dda-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="11dda-185">Al termine verrà visualizzato un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="11dda-185">When it is finished, you will get a message that looks something like:</span></span>

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

### <a name="troubleshooting"></a><span data-ttu-id="11dda-186">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="11dda-186">Troubleshooting</span></span>
* <span data-ttu-id="11dda-187">Quando si usa AZCopy, se viene visualizzato l'errore "Il server non è stato in grado di autenticare la richiesta", assicurarsi che il valore dell'intestazione di autorizzazione sia formato correttamente, inclusa la firma.</span><span class="sxs-lookup"><span data-stu-id="11dda-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="11dda-188">Se si sta usando la chiave 2 o la chiave di archiviazione secondaria, provare a usare la chiave 1 o la chiave di archiviazione primaria.</span><span class="sxs-lookup"><span data-stu-id="11dda-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="11dda-189">Creare la nuova VM</span><span class="sxs-lookup"><span data-stu-id="11dda-189">Create the new VM</span></span> 

<span data-ttu-id="11dda-190">È necessario creare le risorse di rete e le altre risorse da usare nella nuova VM.</span><span class="sxs-lookup"><span data-stu-id="11dda-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="11dda-191">Creare la subNet e la vNet</span><span class="sxs-lookup"><span data-stu-id="11dda-191">Create the subNet and vNet</span></span>

<span data-ttu-id="11dda-192">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11dda-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="11dda-193">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="11dda-193">Create the subNet.</span></span> <span data-ttu-id="11dda-194">In questo esempio viene creata una subnet denominata **mySubNet** nel gruppo di risorse **myResourceGroup** e il prefisso dell'indirizzo della subnet viene impostato su **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="11dda-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="11dda-195">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="11dda-195">Create the vNet.</span></span> <span data-ttu-id="11dda-196">In questo esempio il nome della rete virtuale è **myVnetName**, la posizione specificata è **Stati Uniti occidentali** e il prefisso dell'indirizzo per la rete virtuale è **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="11dda-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="11dda-197">Creare un indirizzo IP pubblico e NIC</span><span class="sxs-lookup"><span data-stu-id="11dda-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="11dda-198">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="11dda-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="11dda-199">Creare l'IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="11dda-199">Create the public IP.</span></span> <span data-ttu-id="11dda-200">In questo esempio, il nome dell'indirizzo IP pubblico è **myIP**.</span><span class="sxs-lookup"><span data-stu-id="11dda-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="11dda-201">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="11dda-201">Create the NIC.</span></span> <span data-ttu-id="11dda-202">In questo esempio, il nome specificato della scheda NIC è **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="11dda-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="11dda-203">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="11dda-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="11dda-204">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="11dda-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="11dda-205">Poiché il disco rigido virtuale per la nuova macchina virtuale è stato creato da una VM specializzata esistente, dopo l'avvenuta creazione della macchina virtuale è possibile usare un account esistente dalla VM di origine che aveva l'autorizzazione di accedere tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="11dda-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="11dda-206">In questo esempio il nome NSG impostato è **myNsg**, mentre il nome della regola RDP è **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="11dda-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="11dda-207">Per altre informazioni sugli endpoint e sulle regole NSG, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11dda-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="11dda-208">Impostare il nome e le dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="11dda-208">Set the VM name and size</span></span>

<span data-ttu-id="11dda-209">In questo esempio il nome della macchina virtuale viene impostato su "myVM" e le dimensioni su "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="11dda-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="11dda-210">Aggiungere la scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="11dda-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="11dda-211">Configurare il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="11dda-211">Configure the OS disk</span></span>

1. <span data-ttu-id="11dda-212">Impostare l'URI per il disco rigido virtuale caricato o copiato.</span><span class="sxs-lookup"><span data-stu-id="11dda-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="11dda-213">In questo esempio, il file del disco rigido virtuale denominato **myOsDisk.vhd** viene mantenuto in un account di archiviazione denominato **myStorageAccount** all'interno di un contenitore denominato **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="11dda-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="11dda-214">Aggiungere il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="11dda-214">Add the OS disk.</span></span> <span data-ttu-id="11dda-215">In questo esempio, quando viene creato il disco del sistema operativo, il termine "osDisk" viene collegato al nome della macchina virtuale per creare il nome del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="11dda-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="11dda-216">Questo esempio specifica anche che il disco rigido virtuale basato su Windows deve essere collegato alla macchina virtuale come disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="11dda-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="11dda-217">Facoltativo: se si dispone di dischi dati da associare alla macchina virtuale, aggiungere i dischi dati tramite gli URL dei dischi rigidi virtuali di dati e il numero di unità logica (LUN) appropriato.</span><span class="sxs-lookup"><span data-stu-id="11dda-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="11dda-218">Quando si usa un account di archiviazione, gli URL dei dischi dati e del sistema operativo sono simili al seguente: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="11dda-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="11dda-219">Per trovarlo nel portale, passare al contenitore di archiviazione di destinazione, fare clic sul disco rigido virtuale del sistema operativo o dei dati copiato e quindi copiare il contenuto dell'URL.</span><span class="sxs-lookup"><span data-stu-id="11dda-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="11dda-220">Completare la VM</span><span class="sxs-lookup"><span data-stu-id="11dda-220">Complete the VM</span></span> 

<span data-ttu-id="11dda-221">Creare la macchina virtuale usando le configurazioni appena create.</span><span class="sxs-lookup"><span data-stu-id="11dda-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="11dda-222">Se il comando ha esito positivo, viene visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="11dda-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="11dda-223">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="11dda-223">Verify that the VM was created</span></span>
<span data-ttu-id="11dda-224">La VM appena creata verrà visualizzata nel [portale di Azure](https://portal.azure.com) in **Sfoglia** > **Macchine virtuali** oppure usando i comandi di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="11dda-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="11dda-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11dda-225">Next steps</span></span>
<span data-ttu-id="11dda-226">Per accedere alla nuova macchina virtuale, passare alla VM nel [portale](https://portal.azure.com), fare clic su **Connetti**e aprire il file RDP di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="11dda-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="11dda-227">Usare le credenziali dell'account della macchina virtuale originale per accedere alla nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11dda-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="11dda-228">Per altre informazioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="11dda-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

