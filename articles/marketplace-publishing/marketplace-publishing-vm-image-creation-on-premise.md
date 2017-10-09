---
title: un'immagine di macchina virtuale locale per hello Azure Marketplace aaaCreating | Documenti Microsoft
description: Comprendere ed eseguire i passaggi di hello toocreate un'immagine di macchina virtuale locale e distribuire toohello Azure Marketplace per altri toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="caf61-103">Sviluppare un'immagine di macchina virtuale locale per hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="caf61-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="caf61-104">Si consiglia di sviluppare Azure dischi rigidi virtuali (VHD) direttamente nel cloud hello tramite Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="caf61-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="caf61-105">Tuttavia, se necessario, è possibile toodownload un disco rigido virtuale e sviluppo tramite l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="caf61-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="caf61-106">Per lo sviluppo locale, è necessario scaricare il sistema operativo hello VHD di hello creato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="caf61-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="caf61-107">Questi passaggi avverrebbero come parte del passaggio 3.3 precedente.</span><span class="sxs-lookup"><span data-stu-id="caf61-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="caf61-108">Scaricare un'immagine di VHD </span><span class="sxs-lookup"><span data-stu-id="caf61-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="caf61-109">Individuare l'URL BLOB</span><span class="sxs-lookup"><span data-stu-id="caf61-109">Locate a blob URL</span></span>
<span data-ttu-id="caf61-110">In hello toodownload ordine VHD, individuare innanzitutto URL blob hello per disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="caf61-111">Individuare nuovi URL blob hello da hello [portale Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="caf61-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="caf61-112">Andare troppo**Sfoglia** > **macchine virtuali**, e quindi seleziona hello distribuito macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="caf61-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="caf61-113">In **configura**selezionare hello **dischi** riquadro, che apre il pannello dischi hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="caf61-115">Seleziona hello **disco del sistema operativo**, che viene aperto un altro pannello contenente le proprietà di disco, inclusi il percorso di VHD hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="caf61-116">Copiare questo URL blob.</span><span class="sxs-lookup"><span data-stu-id="caf61-116">Copy this blob URL.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="caf61-118">A questo punto, eliminare hello distribuito una macchina virtuale senza eliminare i dischi di hello sottostante.</span><span class="sxs-lookup"><span data-stu-id="caf61-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="caf61-119">È anche possibile arrestare hello VM anziché eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="caf61-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="caf61-120">Non scaricare il disco rigido virtuale del sistema operativo hello quando hello macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="caf61-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="caf61-122">Scaricare il VHD</span><span class="sxs-lookup"><span data-stu-id="caf61-122">Download a VHD</span></span>
<span data-ttu-id="caf61-123">Dopo avere stabilito hello blob URL, è possibile scaricare hello VHD utilizzando hello [portale di Azure](http://manage.windowsazure.com/) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="caf61-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="caf61-124">Al momento di hello della creazione di questa Guida, toodownload funzionalità hello un disco rigido virtuale non è ancora presente nel nuovo portale di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="caf61-125">**Scaricare hello sistema operativo tramite hello corrente [portale di Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="caf61-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="caf61-126">Se non è già, accedere toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="caf61-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="caf61-127">Fare clic su hello **archiviazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="caf61-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="caf61-128">Selezionare l'account di archiviazione hello all'interno delle quali hello disco rigido virtuale è archiviato.</span><span class="sxs-lookup"><span data-stu-id="caf61-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="caf61-130">Questo visualizza le proprietà dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="caf61-130">This displays storage account properties.</span></span> <span data-ttu-id="caf61-131">Seleziona hello **contenitori** scheda.</span><span class="sxs-lookup"><span data-stu-id="caf61-131">Select hello **Containers** tab.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="caf61-133">Selezionare il contenitore di hello in cui hello disco rigido virtuale è archiviato.</span><span class="sxs-lookup"><span data-stu-id="caf61-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="caf61-134">Per impostazione predefinita, quando creato dal portale di hello, hello VHD è archiviato in un contenitore di dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="caf61-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="caf61-136">Selezionare hello del sistema operativo corretto VHD confrontando hello URL toohello uno che è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="caf61-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="caf61-137">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="caf61-137">Click **Download**.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="caf61-139">Scaricare il VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="caf61-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="caf61-140">Inoltre toousing hello portale di Azure, è possibile usare hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="caf61-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="caf61-141">Ad esempio, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="caf61-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="caf61-142">**Save-AzureVhd** dispone anche di un **NumberOfThreads** opzione che può essere utilizzato tooincrease parallelismo toomake hello miglior utilizzo della larghezza di banda disponibile per il download di hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="caf61-143">Caricare dischi rigidi virtuali tooan account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="caf61-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="caf61-144">Se sono preparati i dischi rigidi virtuali locale, è necessario tooupload in uno spazio di archiviazione di account in Azure.</span><span class="sxs-lookup"><span data-stu-id="caf61-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="caf61-145">Questo passaggio avviene dopo la creazione del VHD locale, ma prima di ottenere una certificazione per l'immagine della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="caf61-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="caf61-146">Creare un account di archiviazione e un contenitore</span><span class="sxs-lookup"><span data-stu-id="caf61-146">Create a storage account and container</span></span>
<span data-ttu-id="caf61-147">È consigliabile che i dischi rigidi virtuali da caricare in un account di archiviazione in un'area in Italia hello.</span><span class="sxs-lookup"><span data-stu-id="caf61-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="caf61-148">Tutti i VHD per un unico codice SKU devono essere posizionati in un singolo contenitore all'interno di un singolo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="caf61-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="caf61-149">toocreate un account di archiviazione, è possibile utilizzare hello [portale Microsoft Azure](https://portal.azure.com/), PowerShell o lo strumento da riga di comando di hello Linux.</span><span class="sxs-lookup"><span data-stu-id="caf61-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="caf61-150">**Creare un account di archiviazione dal portale di Microsoft Azure hello**</span><span class="sxs-lookup"><span data-stu-id="caf61-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="caf61-151">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="caf61-151">Click **New**.</span></span>
2. <span data-ttu-id="caf61-152">Selezionare **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="caf61-152">Select **Storage**.</span></span>
3. <span data-ttu-id="caf61-153">Immettere nome account di archiviazione hello e quindi selezionare un percorso.</span><span class="sxs-lookup"><span data-stu-id="caf61-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="caf61-155">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="caf61-155">Click **Create**.</span></span>
5. <span data-ttu-id="caf61-156">Pannello Hello hello creato l'account di archiviazione deve essere aperta.</span><span class="sxs-lookup"><span data-stu-id="caf61-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="caf61-157">In caso contrario, selezionare **Sfoglia** > **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="caf61-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="caf61-158">Nell'archiviazione hello account pannello, selezionare l'account di archiviazione hello creato.</span><span class="sxs-lookup"><span data-stu-id="caf61-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="caf61-159">Selezionare **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="caf61-159">Select **Containers**.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="caf61-161">Nel Pannello di contenitori hello, selezionare **Aggiungi**, quindi immettere un nome e hello contenitore le autorizzazioni contenitore.</span><span class="sxs-lookup"><span data-stu-id="caf61-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="caf61-162">Selezionare **Privato** per le autorizzazioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="caf61-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="caf61-163">È consigliabile creare un contenitore per ogni SKU che si intende toopublish.</span><span class="sxs-lookup"><span data-stu-id="caf61-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="caf61-165">Creare un account di archiviazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="caf61-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="caf61-166">Utilizzo di PowerShell, creare un account di archiviazione tramite hello [New AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="caf61-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="caf61-167">È possibile creare un contenitore all'interno di tale account di archiviazione tramite hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="caf61-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="caf61-168">Tali comandi presuppongono che contesto tale account di archiviazione corrente hello è già stata impostata in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="caf61-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="caf61-169">Fare riferimento troppo[configurare Azure PowerShell](marketplace-publishing-powershell-setup.md) per ulteriori informazioni sull'installazione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="caf61-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="caf61-170">Creare un account di archiviazione usando lo strumento da riga di comando hello per Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="caf61-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="caf61-171">Dallo [strumento da riga di comando per Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)creare un account di archiviazione come segue.</span><span class="sxs-lookup"><span data-stu-id="caf61-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="caf61-172">Creare un contenitore come segue.</span><span class="sxs-lookup"><span data-stu-id="caf61-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="caf61-173">Caricare il VHD</span><span class="sxs-lookup"><span data-stu-id="caf61-173">Upload a VHD</span></span>
<span data-ttu-id="caf61-174">Una volta creati account di archiviazione di hello e contenitore, è possibile caricare i dischi rigidi virtuali preparati.</span><span class="sxs-lookup"><span data-stu-id="caf61-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="caf61-175">È possibile utilizzare PowerShell, lo strumento da riga di comando di hello Linux o altri strumenti di gestione di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="caf61-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="caf61-176">Caricare un VHD tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="caf61-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="caf61-177">Hello utilizzare [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="caf61-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="caf61-178">Caricare un disco rigido virtuale tramite lo strumento da riga di comando hello per Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="caf61-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="caf61-179">Con hello [lo strumento da riga di comando di Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilizzare la seguente hello: immagine di macchina virtuale di azure creare <image name> -percorso <Location of hello data center> - sistema operativo Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="caf61-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="caf61-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="caf61-180">See also</span></span>
* [<span data-ttu-id="caf61-181">Creazione di un'immagine di macchina virtuale per hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="caf61-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="caf61-182">Configurazione di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="caf61-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

