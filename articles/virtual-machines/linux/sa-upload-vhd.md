---
title: un disco Linux personalizzato con Azure CLI 2.0 aaaUpload | Documenti Microsoft
description: Creare e caricare un disco rigido virtuale (VHD) di tooAzure con modello di distribuzione di gestione risorse di hello e hello Azure CLI 2.0
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="62047-103">Caricare e creare una VM Linux da disco personalizzato con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="62047-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="62047-104">In questo articolo viene illustrato come tooupload account tooan un disco rigido virtuale (VHD) di archiviazione di Azure con hello 2.0 CLI di Azure e creare le macchine virtuali Linux dal disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="62047-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="62047-105">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62047-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="62047-106">Questa funzionalità consente tooinstall e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare macchine virtuali di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="62047-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="62047-107">Questo argomento viene utilizzato l'account di archiviazione per hello finali dischi rigidi virtuali, ma è inoltre possibile eseguire questi passaggi tramite [dischi gestiti](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="62047-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="62047-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="62047-108">Quick commands</span></span>
<span data-ttu-id="62047-109">Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="62047-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="62047-110">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="62047-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="62047-111">Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="62047-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="62047-112">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="62047-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="62047-113">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="62047-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="62047-114">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="62047-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="62047-115">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUs` percorso:</span><span class="sxs-lookup"><span data-stu-id="62047-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="62047-116">Creare un toohold di account di archiviazione dei dischi virtuali con [creare account di archiviazione az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="62047-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="62047-117">esempio Hello crea un account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="62047-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="62047-118">Elencare le chiavi di accesso hello per l'account di archiviazione con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="62047-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="62047-119">Annotare il valore di `key1`:</span><span class="sxs-lookup"><span data-stu-id="62047-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="62047-120">Creare un contenitore all'interno dell'account di archiviazione tramite la chiave di archiviazione hello ottenuto con [creare il contenitore di archiviazione az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="62047-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="62047-121">esempio Hello crea un contenitore denominato `mydisks` utilizzando hello valore chiave di archiviazione da `key1`:</span><span class="sxs-lookup"><span data-stu-id="62047-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="62047-122">Infine, caricare il contenitore di toohello disco rigido virtuale è stato creato con [caricamento blob di archiviazione az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="62047-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="62047-123">Specificare percorso locale di hello tooyour disco rigido virtuale in `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="62047-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="62047-124">Specificare hello URI tooyour disco (`--image`) con [creare vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="62047-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="62047-125">esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="62047-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="62047-126">account di archiviazione di destinazione Hello è toobe hello stesso come in cui è caricato il disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="62047-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="62047-127">Inoltre necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello **creare vm az** comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="62047-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="62047-128">Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="62047-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="62047-129">Requisiti</span><span class="sxs-lookup"><span data-stu-id="62047-129">Requirements</span></span>
<span data-ttu-id="62047-130">hello toocomplete seguendo la procedura, è necessario:</span><span class="sxs-lookup"><span data-stu-id="62047-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="62047-131">**Sistema operativo Linux installato in un file con estensione vhd** -installare un [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in hello disco rigido virtuale formato.</span><span class="sxs-lookup"><span data-stu-id="62047-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="62047-132">Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="62047-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="62047-133">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="62047-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="62047-134">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="62047-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="62047-135">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="62047-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="62047-136">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="62047-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="62047-137">Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello.</span><span class="sxs-lookup"><span data-stu-id="62047-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="62047-138">Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62047-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="62047-139">Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="62047-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="62047-140">È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="62047-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="62047-141">Macchine virtuali create dal disco personalizzato devono risiedere in hello stesso account di archiviazione come disco hello</span><span class="sxs-lookup"><span data-stu-id="62047-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="62047-142">Creare un toohold account e il contenitore di archiviazione, il disco personalizzato e le macchine virtuali create</span><span class="sxs-lookup"><span data-stu-id="62047-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="62047-143">Una volta create tutte le VM, è possibile eliminare il disco</span><span class="sxs-lookup"><span data-stu-id="62047-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="62047-144">Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="62047-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="62047-145">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="62047-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="62047-146">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="62047-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="62047-147"><a id="prepimage"></a></span><span class="sxs-lookup"><span data-stu-id="62047-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="62047-148">Preparare hello disco toobe caricato</span><span class="sxs-lookup"><span data-stu-id="62047-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="62047-149">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="62047-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="62047-150">Hello seguenti articoli semplificato come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure:</span><span class="sxs-lookup"><span data-stu-id="62047-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="62047-151">**[Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-155">**[SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="62047-157">**[Altro - Distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="62047-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="62047-158">Vedere anche hello  **[note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes)**  per suggerimenti generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="62047-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="62047-159">Hello [contratto di servizio di piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applica tooVMs in esecuzione Linux solo quando una delle hello approvate per le distribuzioni viene utilizzata con i dettagli di configurazione hello come specificato nelle versioni supportate in [Linux in approvate per Azure Distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62047-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="62047-160">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="62047-160">Create a resource group</span></span>
<span data-ttu-id="62047-161">Gruppi di risorse in modo logico riunire toosupport di risorse di Azure hello tutte le macchine virtuali, ad esempio una rete virtuale hello e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="62047-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="62047-162">Per altre informazioni sui gruppi di risorse, vedere la [panoramica dei gruppi di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62047-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="62047-163">Prima di caricare il disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="62047-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="62047-164">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso:</span><span class="sxs-lookup"><span data-stu-id="62047-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="62047-165">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="62047-165">Create a storage account</span></span>

<span data-ttu-id="62047-166">Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="62047-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="62047-167">Tutte le macchine virtuali con dischi non gestite che vengono creati tramite il toobe necessità disco personalizzata in hello stesso account di archiviazione come disco.</span><span class="sxs-lookup"><span data-stu-id="62047-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="62047-168">esempio Hello crea un account di archiviazione denominato `mystorageaccount` nel gruppo di risorse hello creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="62047-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="62047-169">Ottenere chiavi degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="62047-169">List storage account keys</span></span>
<span data-ttu-id="62047-170">Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="62047-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="62047-171">Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio toocarry le operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="62047-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="62047-172">Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="62047-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="62047-173">Visualizzare le chiavi di accesso hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="62047-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="62047-174">Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="62047-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="62047-175">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="62047-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="62047-176">Prendere nota del `key1` come sarà necessario utilizzarlo toointeract con l'account di archiviazione in passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="62047-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="62047-177">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="62047-177">Create a storage container</span></span>
<span data-ttu-id="62047-178">In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione dei dischi.</span><span class="sxs-lookup"><span data-stu-id="62047-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="62047-179">Un account di archiviazione può contenere un numero qualsiasi di contenitori.</span><span class="sxs-lookup"><span data-stu-id="62047-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="62047-180">Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="62047-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="62047-181">esempio Hello crea un contenitore denominato `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="62047-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="62047-182">Caricare il file VHD.</span><span class="sxs-lookup"><span data-stu-id="62047-182">Upload VHD</span></span>
<span data-ttu-id="62047-183">Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="62047-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="62047-184">Caricare e archiviare il disco personalizzato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="62047-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="62047-185">Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello disco con percorsi toohello personalizzato nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="62047-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="62047-186">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="62047-186">Create hello VM</span></span>
<span data-ttu-id="62047-187">toocreate una macchina virtuale con dischi non gestiti, specificare disco tooyour URI di hello (`--image`) con [creare vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="62047-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="62047-188">esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="62047-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="62047-189">Specificare hello `--image` parametro con [creare vm az](/cli/azure/vm#create) toopoint tooyour personalizzato disco.</span><span class="sxs-lookup"><span data-stu-id="62047-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="62047-190">Verificare che `--storage-account` corrispondenze hello account di archiviazione in cui è memorizzato nel disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="62047-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="62047-191">Non si dispone toouse hello stesso contenitore come hello toostore disco personalizzata nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="62047-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="62047-192">Apportare eventuali altri contenitori che toocreate hello come hello passaggi precedenti prima di caricare il disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="62047-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="62047-193">esempio Hello crea una macchina virtuale denominata `myVM` dal disco personalizzato:</span><span class="sxs-lookup"><span data-stu-id="62047-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="62047-194">È comunque necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello **creare vm az** comando, ad esempio nome utente e le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="62047-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="62047-195">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62047-195">Resource Manager template</span></span>
<span data-ttu-id="62047-196">Modelli di gestione risorse di Azure sono i file JavaScript Object Notation (JSON) che definiscono l'ambiente hello desiderato toobuild.</span><span class="sxs-lookup"><span data-stu-id="62047-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="62047-197">modelli di Hello sono suddivisi in toodifferent i provider di risorse, ad esempio compute o rete.</span><span class="sxs-lookup"><span data-stu-id="62047-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="62047-198">È possibile utilizzare i modelli esistenti o crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="62047-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="62047-199">Altre informazioni sull' [uso di Resource Manager e relativi modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62047-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="62047-200">All'interno di hello `Microsoft.Compute/virtualMachines` provider del modello, è un `storageProfile` nodo che contiene i dettagli di configurazione hello per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62047-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="62047-201">Hello due parametri principali tooedit sono hello `image` e `vhd` URI che puntano tooyour personalizzato e disco virtuale della nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62047-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="62047-202">esempio Hello viene illustrato un esempio di hello JSON per l'utilizzo di un disco personalizzato:</span><span class="sxs-lookup"><span data-stu-id="62047-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="62047-203">È possibile utilizzare [questo toocreate modello esistente di una macchina virtuale da un'immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leggere le informazioni sulle [la creazione di modelli di Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="62047-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="62047-204">Dopo aver creato un modello configurato, utilizzare [distribuzione gruppo az creare](/cli/azure/group/deployment#create) toocreate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="62047-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="62047-205">Specificare l'URI del modello di JSON hello con hello `--template-uri` parametro:</span><span class="sxs-lookup"><span data-stu-id="62047-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="62047-206">Se si dispone di un file JSON archiviato localmente nel computer in uso, è possibile utilizzare hello `--template-file` parametro invece:</span><span class="sxs-lookup"><span data-stu-id="62047-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="62047-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62047-207">Next steps</span></span>
<span data-ttu-id="62047-208">Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62047-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="62047-209">È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="62047-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="62047-210">Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62047-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

