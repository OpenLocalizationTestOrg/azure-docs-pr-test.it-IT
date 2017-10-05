---
title: Creazione di un'immagine di macchina virtuale in locale per Azure Marketplace | Microsoft Docs
description: Comprendere ed eseguire i passaggi per creare un'immagine di VM in locale e distribuire in Azure Marketplace per l'acquisto da parte di altri utenti.
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
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="83843-103">Sviluppare l'immagine di una macchina virtuale in locale per Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="83843-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="83843-104">Si consiglia di sviluppare i dischi rigidi virtuali (VHD, Virtual Hard Disk) di Azure direttamente nel cloud utilizzando Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="83843-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="83843-105">Tuttavia, se necessario, è possibile scaricare un VHD e svilupparlo utilizzando l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="83843-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="83843-106">Per lo sviluppo locale, è necessario scaricare il VHD del sistema operativo della macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="83843-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="83843-107">Questi passaggi avverrebbero come parte del passaggio 3.3 precedente.</span><span class="sxs-lookup"><span data-stu-id="83843-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="83843-108">Scaricare un'immagine di VHD </span><span class="sxs-lookup"><span data-stu-id="83843-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="83843-109">Individuare l'URL BLOB</span><span class="sxs-lookup"><span data-stu-id="83843-109">Locate a blob URL</span></span>
<span data-ttu-id="83843-110">Per scaricare il VHD, individuare innanzitutto l'URL BLOB per il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="83843-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="83843-111">Individuare l'URL BLOB dal nuovo [portale di Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="83843-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="83843-112">Passare a **Sfoglia** > **VM** e selezionare la VM distribuita.</span><span class="sxs-lookup"><span data-stu-id="83843-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="83843-113">In **Configura** selezionare il riquadro **Dischi**, che apre il pannello Dischi.</span><span class="sxs-lookup"><span data-stu-id="83843-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="83843-115">Selezionare il **disco del sistema operativo**. Verrà aperto un altro pannello che visualizza le proprietà del disco, compresa la posizione del VHD.</span><span class="sxs-lookup"><span data-stu-id="83843-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="83843-116">Copiare questo URL blob.</span><span class="sxs-lookup"><span data-stu-id="83843-116">Copy this blob URL.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="83843-118">A questo punto, eliminare la macchina virtuale distribuita senza eliminare i dischi di backup.</span><span class="sxs-lookup"><span data-stu-id="83843-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="83843-119">È inoltre possibile arrestare la macchina virtuale, anziché eliminarla.</span><span class="sxs-lookup"><span data-stu-id="83843-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="83843-120">Non scaricare il VHD del sistema operativo quando la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83843-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="83843-122">Scaricare il VHD</span><span class="sxs-lookup"><span data-stu-id="83843-122">Download a VHD</span></span>
<span data-ttu-id="83843-123">Quando si conosce l'URL BLOB, è possibile scaricare il VHD utilizzando il [portale di Azure](http://manage.windowsazure.com/) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83843-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="83843-124">Al momento della creazione della guida, la funzionalità per scaricare un VHD non è ancora presente nel nuovo portale di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="83843-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="83843-125">**Scaricare il VHD del sistema operativo tramite il [portale di Azure](http://manage.windowsazure.com/)** corrente</span><span class="sxs-lookup"><span data-stu-id="83843-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="83843-126">Accedere al portale di Azure, se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="83843-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="83843-127">Fare clic sulla scheda **Archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="83843-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="83843-128">Selezionare l'account di archiviazione in cui è archiviato il VHD.</span><span class="sxs-lookup"><span data-stu-id="83843-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="83843-130">Questo visualizza le proprietà dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83843-130">This displays storage account properties.</span></span> <span data-ttu-id="83843-131">Selezionare la scheda **Contenitori** .</span><span class="sxs-lookup"><span data-stu-id="83843-131">Select the **Containers** tab.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="83843-133">Selezionare il contenitore in cui è archiviato il VHD.</span><span class="sxs-lookup"><span data-stu-id="83843-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="83843-134">Per impostazione predefinita, quando creato dal portale, il VHD viene archiviato in un contenitore di VHD.</span><span class="sxs-lookup"><span data-stu-id="83843-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="83843-136">Selezionare il VHD del sistema operativo corretto confrontando l'URL con quello salvato.</span><span class="sxs-lookup"><span data-stu-id="83843-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="83843-137">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="83843-137">Click **Download**.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="83843-139">Scaricare il VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="83843-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="83843-140">Oltre al portale di Azure, è possibile usare il cmdlet [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) per scaricare il VHD del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="83843-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="83843-141">Ad esempio, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="83843-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="83843-142">**Save-AzureVhd** dispone inoltre dell'opzione **NumberOfThreads**, che può essere usata per aumentare il parallelismo per un uso ottimale della larghezza di banda disponibile per il download.</span><span class="sxs-lookup"><span data-stu-id="83843-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="83843-143">Caricare VHD in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83843-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="83843-144">Se i VHD sono stati preparati in locale, è necessario caricarli in un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="83843-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="83843-145">Questo passaggio avviene dopo la creazione del VHD locale, ma prima di ottenere una certificazione per l'immagine della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="83843-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="83843-146">Creare un account di archiviazione e un contenitore</span><span class="sxs-lookup"><span data-stu-id="83843-146">Create a storage account and container</span></span>
<span data-ttu-id="83843-147">Si consiglia di caricare i VHD in un account di archiviazione in un'area negli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="83843-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="83843-148">Tutti i VHD per un unico codice SKU devono essere posizionati in un singolo contenitore all'interno di un singolo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83843-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="83843-149">Per creare un account di archiviazione è possibile utilizzare il [portale di Microsoft Azure](https://portal.azure.com/), PowerShell o lo strumento da riga di comando per Linux.</span><span class="sxs-lookup"><span data-stu-id="83843-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="83843-150">**Creare un account di archiviazione dal portale di Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="83843-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="83843-151">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="83843-151">Click **New**.</span></span>
2. <span data-ttu-id="83843-152">Selezionare **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="83843-152">Select **Storage**.</span></span>
3. <span data-ttu-id="83843-153">Immettere il nome dell’account di archiviazione e quindi selezionare il percorso.</span><span class="sxs-lookup"><span data-stu-id="83843-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="83843-155">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="83843-155">Click **Create**.</span></span>
5. <span data-ttu-id="83843-156">Il pannello dell'account di archiviazione creato deve essere aperto.</span><span class="sxs-lookup"><span data-stu-id="83843-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="83843-157">In caso contrario, selezionare **Sfoglia** > **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="83843-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="83843-158">Nel pannello Account di archiviazione selezionare l'account di archiviazione creato.</span><span class="sxs-lookup"><span data-stu-id="83843-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="83843-159">Selezionare **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="83843-159">Select **Containers**.</span></span>
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="83843-161">Nel pannello Contenitori selezionare **Aggiungi**e quindi immettere un nome e le autorizzazioni per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="83843-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="83843-162">Selezionare **Privato** per le autorizzazioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="83843-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="83843-163">Si consiglia di creare un contenitore per ogni SKU che si intende pubblicare.</span><span class="sxs-lookup"><span data-stu-id="83843-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="83843-165">Creare un account di archiviazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="83843-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="83843-166">Usando PowerShell, creare un account di archiviazione con il cmdlet [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) .</span><span class="sxs-lookup"><span data-stu-id="83843-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="83843-167">Sarà quindi possibile creare un contenitore in tale account di archiviazione usando il cmdlet [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) .</span><span class="sxs-lookup"><span data-stu-id="83843-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="83843-168">Tali comandi presuppongono che il contesto dell’account di archiviazione corrente sia già stato impostato in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83843-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="83843-169">Per ulteriori dettagli sulla configurazione di PowerShell fare riferimento a [Configurazione di Azure PowerShell](marketplace-publishing-powershell-setup.md) .</span><span class="sxs-lookup"><span data-stu-id="83843-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="83843-170">Creare un account di archiviazione con lo strumento da riga di comando per Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="83843-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="83843-171">Dallo [strumento da riga di comando per Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)creare un account di archiviazione come segue.</span><span class="sxs-lookup"><span data-stu-id="83843-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="83843-172">Creare un contenitore come segue.</span><span class="sxs-lookup"><span data-stu-id="83843-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="83843-173">Caricare il VHD</span><span class="sxs-lookup"><span data-stu-id="83843-173">Upload a VHD</span></span>
<span data-ttu-id="83843-174">Dopo aver creato l'account di archiviazione e il contenitore, è possibile caricare i VHD preparati.</span><span class="sxs-lookup"><span data-stu-id="83843-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="83843-175">È possibile usare PowerShell, lo strumento da riga di comando per Linux o altri strumenti di gestione di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83843-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="83843-176">Caricare un VHD tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="83843-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="83843-177">Usare il cmdlet [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="83843-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="83843-178">Caricare un VHD utilizzando lo strumento da riga di comando per Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="83843-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="83843-179">Con lo [strumento da riga di comando per Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), usare il comando indicato di seguito: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="83843-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="83843-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="83843-180">See also</span></span>
* [<span data-ttu-id="83843-181">Creazione di un'immagine di macchina virtuale per Marketplace</span><span class="sxs-lookup"><span data-stu-id="83843-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="83843-182">Configurazione di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="83843-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

