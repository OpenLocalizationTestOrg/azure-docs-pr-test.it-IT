---
title: Creazione e caricamento di un VHD Linux in Azure | Documentazione Microsoft
description: Creare e caricare un disco rigido virtuale di Azure (VHD) contenente il sistema operativo Linux con il modello di distribuzione classica
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 23c30c954875598ce3e01db137b0ef8cda9779f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="c1cf6-103">Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="c1cf6-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="c1cf6-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c1cf6-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c1cf6-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c1cf6-107">È anche possibile [caricare un'immagine disco personalizzata tramite Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c1cf6-108">Questo articolo illustra come creare e caricare un disco rigido virtuale (VHD) in modo da usarlo come immagine per la creazione di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="c1cf6-109">L'articolo fornisce istruzioni su come preparare il sistema operativo in modo da usarlo per la creazione di più macchine virtuali basate sull'immagine specificata.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="c1cf6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c1cf6-110">Prerequisites</span></span>
<span data-ttu-id="c1cf6-111">In questo articolo si presuppone che l'utente disponga degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="c1cf6-112">**Sistema operativo Linux installato in un file .vhd**: è stata installata una [distribuzione di Linux approvata da Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (oppure consultare le [informazioni sulle distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) in un disco virtuale in formato VHD.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="c1cf6-113">Sono disponibili vari strumenti per la creazione di una VM e un file VHD:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="c1cf6-114">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione a usare il disco rigido virtuale come formato di immagine.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="c1cf6-115">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="c1cf6-116">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c1cf6-117">Il formato VHDX più recente non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="c1cf6-118">Quando si crea una VM, specificare VHD come formato.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="c1cf6-119">Se necessario, è possibile convertire i dischi VHDX nel formato VHD usando [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o il cmdlet [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="c1cf6-120">Inoltre, Azure non supporta il caricamento di VHD dinamici, pertanto è necessario convertire tali dischi in VHD statici prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="c1cf6-121">Per convertire dischi dinamici durante il processo di caricamento in Azure, sono disponibili strumenti come [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) .</span><span class="sxs-lookup"><span data-stu-id="c1cf6-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="c1cf6-122">**Interfaccia della riga di comando di Azure** : installare l' [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) più recente per caricare il VHD.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="c1cf6-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="c1cf6-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="c1cf6-124">Passaggio 1: preparare l'immagine da caricare</span><span class="sxs-lookup"><span data-stu-id="c1cf6-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="c1cf6-125">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="c1cf6-126">Gli articoli seguenti forniscono le istruzioni per preparare le diverse distribuzioni Linux supportate in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="c1cf6-127">Dopo aver eseguito le procedure nelle guide seguenti, tornare qui quando è disponibile un file VHD pronto per essere caricato in Azure:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="c1cf6-128">**[Distribuzioni basate su CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-132">**[SLES e openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="c1cf6-134">**[Altro - Distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="c1cf6-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="c1cf6-135">Il contratto di servizio della piattaforma Azure si applica alle macchine virtuali che eseguono il sistema operativo Linux solo quando una distribuzione approvata viene usata con i dettagli di configurazione specificati in "Versioni supportate" in [Linux in Azure - Distribuzioni supportate](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c1cf6-136">Tutte le distribuzioni di Linux disponibili nella raccolta immagini di Azure sono distribuzioni approvate con la configurazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="c1cf6-137">Vedere anche le **[Note generali sull'installazione di Linux](../create-upload-generic.md#general-linux-installation-notes)** per suggerimenti più generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="c1cf6-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="c1cf6-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="c1cf6-139">Passaggio 2: preparare la connessione ad Azure</span><span class="sxs-lookup"><span data-stu-id="c1cf6-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="c1cf6-140">Assicurarsi di usare l'interfaccia della riga di comando di Azure nel modello di distribuzione classica (`azure config mode asm`), quindi accedere al proprio account:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="c1cf6-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="c1cf6-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="c1cf6-142">Passaggio 3: caricare l'immagine in Azure</span><span class="sxs-lookup"><span data-stu-id="c1cf6-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="c1cf6-143">È necessario un account di archiviazione in cui caricare il file VHD.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="c1cf6-144">È possibile usare un account di archiviazione esistente o [crearne uno nuovo](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="c1cf6-145">Usare l'interfaccia della riga di comando di Azure per caricare l'immagine tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="c1cf6-146">Nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-146">In the previous example:</span></span>

* <span data-ttu-id="c1cf6-147">**BlobStorageURL** è l'URL dell'account di archiviazione che si prevede di usare.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="c1cf6-148">**YourImagesFolder** è il contenitore all'interno dell'archiviazione BLOB in cui si vogliono archiviare le immagini.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="c1cf6-149">**VHDName** è l'etichetta che identifica il disco rigido virtuale visualizzata nel portale.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="c1cf6-150">**PathToVHDFile** è il percorso completo e il nome del file con estensione .vhd della macchina.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="c1cf6-151">Il comando seguente illustra un esempio completo:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="c1cf6-152">Passaggio 4: Creare una VM dall'immagine</span><span class="sxs-lookup"><span data-stu-id="c1cf6-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="c1cf6-153">Creare una VM usando `azure vm create` come per una normale VM.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="c1cf6-154">Specificare il nome assegnato all'immagine nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="c1cf6-155">Nell'esempio seguente viene usato il nome dell'immagine **myImage** assegnato nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="c1cf6-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="c1cf6-156">Per creare le proprie VM, fornire nome utente e password, posizione, nome DNS e nome dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="c1cf6-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1cf6-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1cf6-157">Next steps</span></span>
<span data-ttu-id="c1cf6-158">Per altri dettagli, vedere [Riferimento all'interfaccia della riga di comando di Azure per il modello di distribuzione classica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c1cf6-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
