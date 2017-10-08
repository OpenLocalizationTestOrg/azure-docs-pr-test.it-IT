---
title: un'immagine Linux personalizzata con Azure CLI 1.0 aaaUpload | Documenti Microsoft
description: Creare e caricare un disco rigido virtuale (VHD) di tooAzure con un'immagine Linux personalizzata con modello di distribuzione di gestione risorse di hello e hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="31946-103">Caricare e creare una VM Linux dall'immagine del disco personalizzato utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="31946-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="31946-104">Questo articolo illustra come tooupload un disco rigido virtuale (VHD) di tooAzure utilizzando il modello di distribuzione di gestione risorse di hello e creare macchine virtuali Linux da questa immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="31946-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="31946-105">Questa funzionalità consente tooinstall e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare macchine virtuali di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="31946-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="31946-106">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="31946-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="31946-107">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="31946-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="31946-108">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="31946-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="31946-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="31946-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="31946-110">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="31946-110">Quick commands</span></span>
<span data-ttu-id="31946-111">Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31946-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="31946-112">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="31946-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="31946-113">Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="31946-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="31946-114">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="31946-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="31946-115">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="31946-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="31946-116">Creare prima un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="31946-116">First, create a resource group.</span></span> <span data-ttu-id="31946-117">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUs` percorso:</span><span class="sxs-lookup"><span data-stu-id="31946-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="31946-118">Creare un toohold di account di archiviazione dei dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="31946-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="31946-119">esempio Hello crea un account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="31946-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="31946-120">Elencare le chiavi di accesso hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31946-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="31946-121">Annotare il valore di `key1`:</span><span class="sxs-lookup"><span data-stu-id="31946-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="31946-122">Creare un contenitore all'interno dell'account di archiviazione tramite la chiave di archiviazione hello ottenuto.</span><span class="sxs-lookup"><span data-stu-id="31946-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="31946-123">esempio Hello crea un contenitore denominato `myimages` utilizzando hello valore chiave di archiviazione da `key1`:</span><span class="sxs-lookup"><span data-stu-id="31946-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="31946-124">Infine, caricare il contenitore toohello disco rigido virtuale che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="31946-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="31946-125">Specificare percorso locale di hello tooyour disco rigido virtuale in `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="31946-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="31946-126">È ora possibile creare una macchina virtuale dal disco virtuale caricato [utilizzando un modello di Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="31946-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="31946-127">È inoltre possibile utilizzare hello CLI specificando disco tooyour URI di hello (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="31946-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="31946-128">esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="31946-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="31946-129">account di archiviazione di destinazione Hello è toobe hello stesso come in cui è caricato il disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="31946-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="31946-130">Inoltre necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello `azure vm create` comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="31946-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="31946-131">Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="31946-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="31946-132">Requisiti</span><span class="sxs-lookup"><span data-stu-id="31946-132">Requirements</span></span>
<span data-ttu-id="31946-133">hello toocomplete seguendo la procedura, è necessario:</span><span class="sxs-lookup"><span data-stu-id="31946-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="31946-134">**Sistema operativo Linux installato in un file con estensione vhd** -installare un [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in hello disco rigido virtuale formato.</span><span class="sxs-lookup"><span data-stu-id="31946-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="31946-135">Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="31946-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="31946-136">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="31946-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="31946-137">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="31946-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="31946-138">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="31946-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="31946-139">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="31946-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="31946-140">Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello.</span><span class="sxs-lookup"><span data-stu-id="31946-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="31946-141">Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31946-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="31946-142">Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="31946-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="31946-143">È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="31946-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="31946-144">Macchine virtuali create da un'immagine personalizzata devono risiedere in hello stesso account di archiviazione come immagine di hello stessa</span><span class="sxs-lookup"><span data-stu-id="31946-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="31946-145">Creare un toohold account e il contenitore di archiviazione creato le macchine virtuali sia l'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="31946-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="31946-146">Una volta create tutte le VM, è possibile eliminare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="31946-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="31946-147">Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="31946-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="31946-148">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="31946-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="31946-149">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="31946-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="31946-150"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="31946-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="31946-151">Preparare hello immagine toobe caricato</span><span class="sxs-lookup"><span data-stu-id="31946-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="31946-152">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="31946-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="31946-153">Hello seguenti articoli semplificato come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure:</span><span class="sxs-lookup"><span data-stu-id="31946-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="31946-154">**[Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-158">**[SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="31946-160">**[Altro - Distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="31946-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="31946-161">Vedere anche hello  **[note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes)**  per suggerimenti generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="31946-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="31946-162">Hello [contratto di servizio di piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applica tooVMs in esecuzione Linux solo quando una delle hello approvate per le distribuzioni viene utilizzata con i dettagli di configurazione hello come specificato nelle versioni supportate in [Linux in approvate per Azure Distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31946-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="31946-163">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="31946-163">Create a resource group</span></span>
<span data-ttu-id="31946-164">Gruppi di risorse in modo logico riunire toosupport di risorse di Azure hello tutte le macchine virtuali, ad esempio una rete virtuale hello e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31946-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="31946-165">Ulteriori informazioni sui [gruppi di risorse di Azure sono disponibili qui](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31946-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="31946-166">Prima di caricare l'immagine del disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="31946-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="31946-167">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUS` percorso:</span><span class="sxs-lookup"><span data-stu-id="31946-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="31946-168">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="31946-168">Create a storage account</span></span>
<span data-ttu-id="31946-169">Le VM vengono archiviate come BLOB di pagine all'interno di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31946-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="31946-170">Ulteriori informazioni sull' [archiviazione BLOB di Azure sono disponibili qui](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="31946-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="31946-171">Creare un account di archiviazione per l'immagine disco personalizzata e le VM.</span><span class="sxs-lookup"><span data-stu-id="31946-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="31946-172">Tutte le macchine virtuali che vengono creati tramite il toobe necessità di immagine disco personalizzata in hello stesso account di archiviazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="31946-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="31946-173">esempio Hello crea un account di archiviazione denominato `mystorageaccount` nel gruppo di risorse hello creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="31946-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="31946-174">Ottenere chiavi degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="31946-174">List storage account keys</span></span>
<span data-ttu-id="31946-175">Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31946-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="31946-176">Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio toocarry le operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="31946-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="31946-177">Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="31946-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="31946-178">È possibile visualizzare i tasti di scelta con hello `azure storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="31946-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="31946-179">Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="31946-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="31946-180">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="31946-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="31946-181">Prendere nota del `key1` come sarà necessario utilizzarlo toointeract con l'account di archiviazione in passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="31946-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="31946-182">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="31946-182">Create a storage container</span></span>
<span data-ttu-id="31946-183">In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione, i dischi virtuali e le immagini.</span><span class="sxs-lookup"><span data-stu-id="31946-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="31946-184">Un account di archiviazione può contenere un numero qualsiasi di contenitori.</span><span class="sxs-lookup"><span data-stu-id="31946-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="31946-185">esempio Hello crea un contenitore denominato `myimages`, che specifica la chiave di accesso hello ottenuto nel passaggio precedente hello (`key1`):</span><span class="sxs-lookup"><span data-stu-id="31946-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="31946-186">Caricare il file VHD.</span><span class="sxs-lookup"><span data-stu-id="31946-186">Upload VHD</span></span>
<span data-ttu-id="31946-187">Ora è effettivamente possibile caricare l'immagine disco personalizzata.</span><span class="sxs-lookup"><span data-stu-id="31946-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="31946-188">Come con tutti i dischi virtuali utilizzati dalle VM, l'immagine disco personalizzata viene caricata e archiviata come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="31946-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="31946-189">Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello immagine di disco personalizzata toohello percorso sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="31946-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="31946-190">Creare una VM in base a un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="31946-190">Create VM from custom image</span></span>
<span data-ttu-id="31946-191">Quando si creano le macchine virtuali dall'immagine disco personalizzata, specificare l'immagine del disco toohello hello URI.</span><span class="sxs-lookup"><span data-stu-id="31946-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="31946-192">Verificare che hello corrispondenze di account di archiviazione destinazione dove viene archiviata l'immagine disco personalizzata.</span><span class="sxs-lookup"><span data-stu-id="31946-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="31946-193">È possibile creare la macchina virtuale usando il modello di CLI di Azure o Gestione risorse JSON hello.</span><span class="sxs-lookup"><span data-stu-id="31946-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="31946-194">Creare una macchina virtuale utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="31946-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="31946-195">Specificare hello `--image-urn` parametro hello `azure vm create` immagine disco personalizzata tooyour toopoint del comando.</span><span class="sxs-lookup"><span data-stu-id="31946-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="31946-196">Verificare che `--storage-account-name` corrispondenze hello account di archiviazione dove viene archiviata l'immagine disco personalizzata.</span><span class="sxs-lookup"><span data-stu-id="31946-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="31946-197">Non si dispone toouse hello stesso contenitore come hello toostore immagine disco personalizzata nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="31946-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="31946-198">Apportare eventuali altri contenitori che toocreate hello come hello passaggi precedenti prima di caricare immagini del disco rigido personalizzato.</span><span class="sxs-lookup"><span data-stu-id="31946-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="31946-199">esempio Hello crea una macchina virtuale denominata `myVM` dall'immagine disco personalizzata:</span><span class="sxs-lookup"><span data-stu-id="31946-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="31946-200">È comunque necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello `azure vm create` comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="31946-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="31946-201">Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="31946-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="31946-202">Creare una VM utilizzando un modello JSON</span><span class="sxs-lookup"><span data-stu-id="31946-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="31946-203">Modelli di gestione risorse di Azure sono i file JavaScript Object Notation (JSON) che definiscono l'ambiente hello desiderato toobuild.</span><span class="sxs-lookup"><span data-stu-id="31946-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="31946-204">modelli di Hello sono suddivisi in toodifferent i provider di risorse, ad esempio compute o rete.</span><span class="sxs-lookup"><span data-stu-id="31946-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="31946-205">È possibile utilizzare i modelli esistenti o crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="31946-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="31946-206">Altre informazioni sull' [uso di Resource Manager e relativi modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31946-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="31946-207">All'interno di hello `Microsoft.Compute/virtualMachines` provider del modello, è un `storageProfile` nodo che contiene i dettagli di configurazione hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31946-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="31946-208">Hello due parametri principali tooedit sono hello `image` e `vhd` URI che puntano immagine disco personalizzata tooyour e il disco virtuale della nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31946-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="31946-209">esempio Hello viene illustrato un esempio di hello JSON per l'utilizzo di un'immagine del disco personalizzato:</span><span class="sxs-lookup"><span data-stu-id="31946-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="31946-210">È possibile utilizzare [questo toocreate modello esistente di una macchina virtuale da un'immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leggere le informazioni sulle [la creazione di modelli di Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="31946-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="31946-211">Dopo aver creato un modello configurato, creare le macchine virtuali utilizzando hello `azure group deployment create` comando.</span><span class="sxs-lookup"><span data-stu-id="31946-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="31946-212">Specificare l'URI del modello di JSON hello con hello `--template-uri` parametro:</span><span class="sxs-lookup"><span data-stu-id="31946-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="31946-213">Se si dispone di un file JSON archiviato localmente nel computer in uso, è possibile utilizzare hello `--template-file` parametro invece:</span><span class="sxs-lookup"><span data-stu-id="31946-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="31946-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31946-214">Next steps</span></span>
<span data-ttu-id="31946-215">Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31946-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="31946-216">È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="31946-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="31946-217">Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31946-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

