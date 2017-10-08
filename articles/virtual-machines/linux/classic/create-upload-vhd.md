---
title: aaaCreate e caricare un tooAzure VHD Linux | Documenti Microsoft
description: Creare e caricare un Azure disco rigido virtuale (VHD) che contiene sistema operativo Linux di hello utilizzando hello modello di distribuzione classica
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
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="132b0-103">Creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="132b0-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="132b0-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="132b0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="132b0-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="132b0-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="132b0-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="132b0-107">È anche possibile [caricare un'immagine disco personalizzata tramite Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="132b0-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="132b0-108">Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD), è possibile utilizzarlo come la propria immagine toocreate di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="132b0-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="132b0-109">Informazioni su come il sistema operativo hello tooprepare quindi è possibile usare toocreate più macchine virtuali in base che l'immagine.</span><span class="sxs-lookup"><span data-stu-id="132b0-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="132b0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="132b0-110">Prerequisites</span></span>
<span data-ttu-id="132b0-111">Questo articolo si presuppone di aver hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="132b0-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="132b0-112">**Sistema operativo Linux installato in un file con estensione vhd** -è stato installato un [distribuzione Linux approvate per Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disco virtuale tooa in formato VHD hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="132b0-113">Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="132b0-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="132b0-114">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="132b0-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="132b0-115">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="132b0-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="132b0-116">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="132b0-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="132b0-117">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="132b0-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="132b0-118">Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="132b0-119">Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="132b0-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="132b0-120">Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="132b0-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="132b0-121">È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="132b0-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="132b0-122">**Interfaccia della riga di comando di Azure** -hello installazione più recente [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello tooupload disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="132b0-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="132b0-123"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="132b0-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="132b0-124">Passaggio 1: Preparare hello immagine toobe caricato</span><span class="sxs-lookup"><span data-stu-id="132b0-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="132b0-125">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="132b0-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="132b0-126">Hello seguenti articoli illustra come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure.</span><span class="sxs-lookup"><span data-stu-id="132b0-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="132b0-127">Dopo aver completato i passaggi seguenti guide hello hello, sono disponibili qui dopo aver un file VHD che è pronto tooupload tooAzure:</span><span class="sxs-lookup"><span data-stu-id="132b0-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="132b0-128">**[Distribuzioni basate su CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-132">**[SLES e openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="132b0-134">**[Altro - Distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="132b0-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="132b0-135">contratto di servizio di piattaforma Azure Hello applica toovirtual computer hello viene utilizzato solo quando una delle hello approvate per le distribuzioni del sistema operativo Linux con i dettagli di configurazione hello come specificato nelle versioni supportate [Linux in distribuzioni Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="132b0-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="132b0-136">Tutte le distribuzioni di Linux nella raccolta di immagini di Azure hello sono avallate distribuzioni con la configurazione richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="132b0-137">Vedere anche hello  **[note sull'installazione di Linux](../create-upload-generic.md#general-linux-installation-notes)**  per suggerimenti generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="132b0-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="132b0-138"><a id="connect"></a></span><span class="sxs-lookup"><span data-stu-id="132b0-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="132b0-139">Passaggio 2: Preparare hello connessione tooAzure</span><span class="sxs-lookup"><span data-stu-id="132b0-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="132b0-140">Assicurarsi che si utilizza il modello di distribuzione classica hello Ciao CLI di Azure (`azure config mode asm`), quindi accedi tooyour account:</span><span class="sxs-lookup"><span data-stu-id="132b0-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="132b0-141"><a id="upload"></a></span><span class="sxs-lookup"><span data-stu-id="132b0-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="132b0-142">Passaggio 3: Caricare hello immagine tooAzure</span><span class="sxs-lookup"><span data-stu-id="132b0-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="132b0-143">È necessario un tooupload di account di archiviazione di file di disco rigido virtuale per.</span><span class="sxs-lookup"><span data-stu-id="132b0-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="132b0-144">È possibile usare un account di archiviazione esistente o [crearne uno nuovo](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="132b0-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="132b0-145">Usare hello Azure CLI tooupload hello immagine utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="132b0-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="132b0-146">Nell'esempio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="132b0-146">In hello previous example:</span></span>

* <span data-ttu-id="132b0-147">**BlobStorageURL** hello URL per l'account di archiviazione hello Prevedi toouse</span><span class="sxs-lookup"><span data-stu-id="132b0-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="132b0-148">**YourImagesFolder** è il contenitore di hello nell'archiviazione blob in cui si desidera toostore delle immagini</span><span class="sxs-lookup"><span data-stu-id="132b0-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="132b0-149">**VHDName** è hello etichetta visualizzata nel disco rigido virtuale di portale tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="132b0-150">**PathToVHDFile** è hello di percorso completo e il nome del file con estensione vhd hello nel computer.</span><span class="sxs-lookup"><span data-stu-id="132b0-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="132b0-151">Hello comando seguente viene illustrato un esempio completo:</span><span class="sxs-lookup"><span data-stu-id="132b0-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="132b0-152">Passaggio 4: Creare una macchina virtuale dall'immagine hello</span><span class="sxs-lookup"><span data-stu-id="132b0-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="132b0-153">Si crea una macchina virtuale utilizzando `azure vm create` in hello esattamente come una macchina virtuale di regolare.</span><span class="sxs-lookup"><span data-stu-id="132b0-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="132b0-154">Specificare nome hello assegnato l'immagine nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="132b0-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="132b0-155">Nel seguente esempio di hello, utilizziamo hello **myImage** nome immagine fornito nel passaggio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="132b0-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="132b0-156">toocreate le proprie macchine virtuali, fornire la propria username + password, indirizzo, nome DNS e nome dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="132b0-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="132b0-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="132b0-157">Next steps</span></span>
<span data-ttu-id="132b0-158">Per ulteriori informazioni, vedere [riferimento CLI di Azure per il modello di distribuzione classica Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="132b0-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
