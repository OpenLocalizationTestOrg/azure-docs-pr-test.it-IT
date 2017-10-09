---
title: copia una VM Linux personalizzato con l'interfaccia CLI di Azure 2.0 o aaaUpload | Documenti Microsoft
description: Caricare o copiare una macchina virtuale personalizzata con modello di distribuzione di gestione risorse di hello e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="0d216-103">Creare una VM Linux da disco personalizzata con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d216-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="0d216-104">In questo articolo illustra come tooupload un personalizzato disco rigido virtuale (VHD) o copiare un un disco rigido virtuale esistente in Azure e creare nuove macchine virtuali Linux (VM) da disco personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="0d216-105">È possibile installare e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare una nuova macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d216-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="0d216-106">Se si desidera toocreate più macchine virtuali dal disco personalizzato, si deve creare un'immagine dal disco rigido virtuale o macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d216-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="0d216-107">Per ulteriori informazioni, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="0d216-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="0d216-108">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="0d216-108">You have two options:</span></span>
* [<span data-ttu-id="0d216-109">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="0d216-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="0d216-110">Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="0d216-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="0d216-111">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="0d216-111">Quick commands</span></span>

<span data-ttu-id="0d216-112">Quando si crea una nuova macchina virtuale utilizzando [creare vm az](/cli/azure/vm#create) da un disco specializzato o personalizzato è **allegare** disco hello (-disco del sistema operativo collegare) anziché specificare un'immagine personalizzata o marketplace (-immagine).</span><span class="sxs-lookup"><span data-stu-id="0d216-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="0d216-113">esempio Hello crea una macchina virtuale denominata *myVM* utilizzando hello gestito disco denominato *myManagedDisk* creato dal disco rigido virtuale personalizzato:</span><span class="sxs-lookup"><span data-stu-id="0d216-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="0d216-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="0d216-114">Requirements</span></span>
<span data-ttu-id="0d216-115">hello toocomplete seguendo la procedura, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0d216-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="0d216-116">Una macchina virtuale Linux che è stata preparata per l'uso in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d216-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="0d216-117">Hello [Prepare hello VM](#prepare-the-vm) sezione di questo articolo descrive come toofind distro le informazioni specifiche sull'installazione di hello agente Linux Azure (waagent) che è necessario per hello VM toowork correttamente in Azure e si toobe in grado di tooconnect tooit tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="0d216-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="0d216-118">il file VHD Hello da un oggetto esistente [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in formato VHD hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="0d216-119">Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="0d216-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="0d216-120">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d216-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="0d216-121">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="0d216-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="0d216-122">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d216-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0d216-123">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d216-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="0d216-124">Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="0d216-125">Se necessario, è possibile convertire VHDX dischi tooVHD con [qemu img convertire](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d216-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="0d216-126">Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="0d216-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="0d216-127">È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0d216-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="0d216-128">Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0d216-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0d216-129">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="0d216-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0d216-130">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="0d216-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="0d216-131"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="0d216-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="0d216-132">Preparare hello VM</span><span class="sxs-lookup"><span data-stu-id="0d216-132">Prepare hello VM</span></span>

<span data-ttu-id="0d216-133">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="0d216-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="0d216-134">Hello seguenti articoli semplificato come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure:</span><span class="sxs-lookup"><span data-stu-id="0d216-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="0d216-135">Distribuzioni basate su CentOS</span><span class="sxs-lookup"><span data-stu-id="0d216-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="0d216-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="0d216-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="0d216-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-139">SLES e openSUSE</span><span class="sxs-lookup"><span data-stu-id="0d216-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0d216-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0d216-141">Altro - Distribuzioni non approvate</span><span class="sxs-lookup"><span data-stu-id="0d216-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="0d216-142">Vedere anche hello [note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per suggerimenti generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="0d216-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="0d216-143">Hello [contratto di servizio di piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applica tooVMs in esecuzione Linux solo quando una delle hello approvate per le distribuzioni viene utilizzata con i dettagli di configurazione hello come specificato nelle versioni supportate in [Linux in approvate per Azure Distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d216-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="0d216-144">Opzione 1: caricare un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="0d216-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="0d216-145">È possibile caricare un disco rigido virtuale personalizzato in esecuzione in un computer locale o che è stato esportato da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="0d216-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="0d216-146">disco rigido virtuale hello toouse toocreate una nuova macchina virtuale di Azure, è necessario un archivio di tooa tooupload hello VHD account e creare un disco gestito da hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d216-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="0d216-147">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0d216-147">Create a resource group</span></span>

<span data-ttu-id="0d216-148">Prima di caricare il disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0d216-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="0d216-149">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso: [Panoramica di dischi gestiti di Azure](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0d216-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="0d216-150">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0d216-150">Create a storage account</span></span>

<span data-ttu-id="0d216-151">Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="0d216-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="0d216-152">esempio Hello crea un account di archiviazione denominato *mystorageaccount* nel gruppo di risorse hello creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="0d216-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="0d216-153">Ottenere chiavi degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0d216-153">List storage account keys</span></span>
<span data-ttu-id="0d216-154">Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0d216-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="0d216-155">Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio l'esecuzione di operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="0d216-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="0d216-156">Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0d216-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="0d216-157">Visualizzare le chiavi di accesso hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="0d216-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="0d216-158">Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="0d216-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="0d216-159">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0d216-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="0d216-160">Prendere nota del **key1** come sarà necessario utilizzarlo toointeract con l'account di archiviazione in passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="0d216-161">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0d216-161">Create a storage container</span></span>
<span data-ttu-id="0d216-162">In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione dei dischi.</span><span class="sxs-lookup"><span data-stu-id="0d216-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="0d216-163">Un account di archiviazione può contenere un numero qualsiasi di contenitori.</span><span class="sxs-lookup"><span data-stu-id="0d216-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="0d216-164">Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="0d216-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="0d216-165">esempio Hello crea un contenitore denominato *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="0d216-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="0d216-166">Caricare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="0d216-166">Upload hello VHD</span></span>
<span data-ttu-id="0d216-167">Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="0d216-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="0d216-168">Caricare e archiviare il disco personalizzato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="0d216-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="0d216-169">Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello disco con percorsi toohello personalizzato nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="0d216-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="0d216-170">Caricamento hello disco rigido virtuale potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="0d216-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="0d216-171">Creare un disco gestito</span><span class="sxs-lookup"><span data-stu-id="0d216-171">Create a managed disk</span></span>


<span data-ttu-id="0d216-172">Creare un disco gestito da hello VHD utilizzando [disco az creare](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="0d216-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="0d216-173">esempio Hello crea un disco gestito denominato *myManagedDisk* caricato dal disco rigido virtuale hello tooyour denominato account di archiviazione e contenitore:</span><span class="sxs-lookup"><span data-stu-id="0d216-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="0d216-174">Opzione 2: copiare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="0d216-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="0d216-175">È inoltre possibile creare hello personalizzato macchina virtuale in Azure e quindi copia disco hello del sistema operativo e di collegarlo tooa nuova VM toocreate un'altra copia.</span><span class="sxs-lookup"><span data-stu-id="0d216-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="0d216-176">L'operazione è corretta per il test, ma se si desidera toouse una macchina virtuale di Azure esistente come modello hello per più nuove macchine virtuali, è effettivamente necessario creare un **immagine** invece.</span><span class="sxs-lookup"><span data-stu-id="0d216-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="0d216-177">Per ulteriori informazioni sulla creazione di un'immagine da una macchina virtuale di Azure esistente, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="0d216-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="0d216-178">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="0d216-178">Create a snapshot</span></span>

<span data-ttu-id="0d216-179">Questo esempio crea uno snapshot di una macchina virtuale denominata *myVM* nel gruppo di risorse *myResourceGroup* e uno snapshot denominato *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="0d216-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="0d216-180">Disco gestito hello creare</span><span class="sxs-lookup"><span data-stu-id="0d216-180">Create hello managed disk</span></span>

<span data-ttu-id="0d216-181">Creare un nuovo disco gestito da snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="0d216-182">Ottenere l'ID di hello dello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="0d216-183">In questo esempio è denominato snapshot hello *osDiskSnapshot* ed è in hello *myResourceGroup* gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0d216-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="0d216-184">Disco gestito hello creato.</span><span class="sxs-lookup"><span data-stu-id="0d216-184">Create hello managed disk.</span></span> <span data-ttu-id="0d216-185">In questo esempio, si creerà un disco gestito denominato *myManagedDisk* dallo snapshot che ha una dimensione di 128 GB nell'archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="0d216-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="0d216-186">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="0d216-186">Create hello VM</span></span>

<span data-ttu-id="0d216-187">A questo punto, creare la macchina virtuale con [creare vm az](/cli/azure/vm#create) e collegamento (-disco del sistema operativo collegare) hello gestiti disco come disco di hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0d216-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="0d216-188">esempio Hello crea una macchina virtuale denominata *myNewVM* utilizzando hello gestito disco creato dal disco rigido virtuale caricato:</span><span class="sxs-lookup"><span data-stu-id="0d216-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="0d216-189">Dovrebbe essere in grado di tooSSH in hello VM utilizzando le credenziali di hello dalla macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="0d216-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d216-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d216-190">Next steps</span></span>
<span data-ttu-id="0d216-191">Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d216-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0d216-192">È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0d216-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="0d216-193">Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d216-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

