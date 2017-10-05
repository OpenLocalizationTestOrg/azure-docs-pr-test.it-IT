---
title: Caricare un disco Linux personalizzato con l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Creare e caricare un disco rigido virtuale in Azure usando il modello di distribuzione di Resource Manager e l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 9159960af396e89f373da711e0cc46fdd996ab83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="d51f8-103">Caricare e creare una VM Linux da un disco personalizzato usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d51f8-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="d51f8-104">Questo articolo illustra come caricare un disco rigido virtuale su un account di archiviazione di Azure con l'interfaccia della riga di comando di Azure 2.0 e come creare VM Linux da questo disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-104">This article shows you how to upload a virtual hard disk (VHD) to an Azure storage account with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="d51f8-105">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d51f8-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d51f8-106">Questa funzionalità consente di installare e configurare una distribuzione Linux in base ai propri requisiti e quindi di usare il disco rigido virtuale per creare rapidamente macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d51f8-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="d51f8-107">Questo argomento usa gli account di archiviazione per i dischi rigidi virtuali finali, ma è possibile anche eseguire questi passaggi usando i [dischi gestiti](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="d51f8-107">This topic uses storage accounts for the final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="d51f8-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="d51f8-108">Quick commands</span></span>
<span data-ttu-id="d51f8-109">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica in dettaglio i comandi base per caricare un disco rigido virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="d51f8-109">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="d51f8-110">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="d51f8-110">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="d51f8-111">Assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d51f8-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d51f8-112">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="d51f8-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d51f8-113">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="d51f8-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="d51f8-114">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d51f8-115">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `WestUs`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="d51f8-116">Creare un account di archiviazione in cui salvare i dischi virtuali con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-116">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="d51f8-117">Nell'esempio seguente viene creato un nuovo account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="d51f8-118">Elencare le chiavi di accesso per l'account di archiviazione con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="d51f8-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="d51f8-119">Annotare il valore di `key1`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="d51f8-120">Creare un contenitore nell'account di archiviazione con [az storage container create](/cli/azure/storage/container#create) usando la chiave di archiviazione ottenuta.</span><span class="sxs-lookup"><span data-stu-id="d51f8-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="d51f8-121">Nell'esempio seguente viene creato un contenitore denominato `mydisks` usando il valore della chiave di archiviazione da `key1`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="d51f8-122">Usare infine [az storage blob upload](/cli/azure/storage/blob#upload) per caricare il disco rigido virtuale nel contenitore creato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="d51f8-123">Specificare il percorso locale per il disco rigido virtuale in `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="d51f8-124">Specificare l'URI ne disco (`--image`) con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-124">Specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d51f8-125">L'esempio seguente crea una VM denominata `myVM` usando il disco virtuale caricato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="d51f8-125">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="d51f8-126">L'account di archiviazione di destinazione deve essere lo stesso in cui è stato caricato il disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="d51f8-126">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="d51f8-127">È anche necessario specificare tutti i parametri aggiuntivi richiesti dal comando **az vm create**, ad esempio rete virtuale, indirizzo IP pubblico, nome utente e chiavi SSH, oppure rispondere ai messaggi inerenti.</span><span class="sxs-lookup"><span data-stu-id="d51f8-127">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="d51f8-128">Sono disponibili altre informazioni sui [parametri di Resource Manager per l'interfaccia della riga di comando](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="d51f8-128">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="d51f8-129">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d51f8-129">Requirements</span></span>
<span data-ttu-id="d51f8-130">Per completare la procedura seguente, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d51f8-130">To complete the following steps, you need:</span></span>

* <span data-ttu-id="d51f8-131">**Sistema operativo Linux installato in un file VHD**: installare una [distribuzione Linux approvata da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), oppure vedere le [informazioni sulle distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), in un disco virtuale in formato VHD.</span><span class="sxs-lookup"><span data-stu-id="d51f8-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="d51f8-132">Sono disponibili vari strumenti per la creazione di una VM e un file VHD:</span><span class="sxs-lookup"><span data-stu-id="d51f8-132">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="d51f8-133">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione a usare il disco rigido virtuale come formato di immagine.</span><span class="sxs-lookup"><span data-stu-id="d51f8-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="d51f8-134">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="d51f8-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="d51f8-135">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d51f8-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d51f8-136">Il formato VHDX più recente non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="d51f8-136">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="d51f8-137">Quando si crea una VM, specificare VHD come formato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-137">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="d51f8-138">Se necessario, è possibile convertire i dischi VHDX nel formato VHD usando [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o il cmdlet [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d51f8-138">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="d51f8-139">Inoltre, Azure non supporta il caricamento di VHD dinamici, pertanto è necessario convertire tali dischi in VHD statici prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="d51f8-139">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="d51f8-140">Per convertire dischi dinamici durante il processo di caricamento in Azure, sono disponibili strumenti come [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) .</span><span class="sxs-lookup"><span data-stu-id="d51f8-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="d51f8-141">Le VM create da un disco personalizzato devono trovarsi nello stesso account di archiviazione del disco stesso</span><span class="sxs-lookup"><span data-stu-id="d51f8-141">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="d51f8-142">Creare un account di archiviazione e un contenitore in cui inserire il disco personalizzato e le VM create</span><span class="sxs-lookup"><span data-stu-id="d51f8-142">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="d51f8-143">Una volta create tutte le VM, è possibile eliminare il disco</span><span class="sxs-lookup"><span data-stu-id="d51f8-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="d51f8-144">Assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d51f8-144">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d51f8-145">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="d51f8-145">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d51f8-146">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="d51f8-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="d51f8-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="d51f8-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="d51f8-148">Preparare il disco da caricare</span><span class="sxs-lookup"><span data-stu-id="d51f8-148">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="d51f8-149">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="d51f8-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="d51f8-150">Gli articoli seguenti forniscono le istruzioni per preparare le diverse distribuzioni Linux supportate in Azure:</span><span class="sxs-lookup"><span data-stu-id="d51f8-150">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="d51f8-151">**[Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-155">**[SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d51f8-157">**[Altro - Distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d51f8-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="d51f8-158">Vedere anche le **[Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes)** per suggerimenti più generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="d51f8-158">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d51f8-159">Il [Contratto di Servizio per la piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) è applicabile alle VM che eseguono Linux solo quando una distribuzione approvata viene usata con i dettagli di configurazione specificati nella sezione "Versioni e distribuzioni supportate" in [Distribuzioni di Linux supportate da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d51f8-159">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="d51f8-160">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d51f8-160">Create a resource group</span></span>
<span data-ttu-id="d51f8-161">I gruppi di risorse riuniscono in modo logico tutte le risorse di Azure a supporto delle macchine virtuali, come l'archiviazione e la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d51f8-161">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="d51f8-162">Per altre informazioni sui gruppi di risorse, vedere la [panoramica dei gruppi di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d51f8-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d51f8-163">Prima di caricare il disco personalizzato e creare le VM, è necessario creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-163">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="d51f8-164">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `westus`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-164">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="d51f8-165">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d51f8-165">Create a storage account</span></span>

<span data-ttu-id="d51f8-166">Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="d51f8-167">Le VM con dischi non gestiti create partendo dal disco personalizzato devono trovarsi nello stesso account di archiviazione del disco.</span><span class="sxs-lookup"><span data-stu-id="d51f8-167">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> 

<span data-ttu-id="d51f8-168">Nell'esempio seguente viene creato un account di archiviazione denominato `mystorageaccount` nel gruppo di risorse creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="d51f8-168">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="d51f8-169">Ottenere chiavi degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d51f8-169">List storage account keys</span></span>
<span data-ttu-id="d51f8-170">Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d51f8-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="d51f8-171">Queste chiavi di accesso vengono utilizzate per autenticarsi nell'account di archiviazione, ad esempio per eseguire operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d51f8-171">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="d51f8-172">Ulteriori informazioni sulla [gestione dell'accesso all'archiviazione sono disponibili qui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d51f8-172">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="d51f8-173">Visualizzare le chiavi di accesso con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="d51f8-173">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="d51f8-174">Visualizzare le chiavi di accesso per l'account di archiviazione creato:</span><span class="sxs-lookup"><span data-stu-id="d51f8-174">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="d51f8-175">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="d51f8-175">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="d51f8-176">Prendere nota dell'elemento `key1` perché verrà utilizzato per interagire con l'account di archiviazione nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="d51f8-176">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="d51f8-177">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d51f8-177">Create a storage container</span></span>
<span data-ttu-id="d51f8-178">Nello stesso modo in cui si creano directory diverse per organizzare in modo logico il file system locale si creano anche i contenitori con un account di archiviazione per organizzare i dischi.</span><span class="sxs-lookup"><span data-stu-id="d51f8-178">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="d51f8-179">Un account di archiviazione può contenere un numero qualsiasi di contenitori.</span><span class="sxs-lookup"><span data-stu-id="d51f8-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="d51f8-180">Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="d51f8-181">Nell'esempio seguente viene creato un contenitore denominato `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="d51f8-181">The following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="d51f8-182">Caricare il file VHD.</span><span class="sxs-lookup"><span data-stu-id="d51f8-182">Upload VHD</span></span>
<span data-ttu-id="d51f8-183">Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="d51f8-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="d51f8-184">Caricare e archiviare il disco personalizzato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="d51f8-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="d51f8-185">Specificare la chiave di accesso e il contenitore creato nel passaggio precedente, quindi selezionare il percorso del disco personalizzato sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="d51f8-185">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-the-vm"></a><span data-ttu-id="d51f8-186">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="d51f8-186">Create the VM</span></span>
<span data-ttu-id="d51f8-187">Per creare una macchina virtuale con dischi non gestiti, specificare l'URI del disco (`--image`) con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-187">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d51f8-188">L'esempio seguente crea una VM denominata `myVM` usando il disco virtuale caricato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="d51f8-188">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="d51f8-189">Specificare il parametro `--image` con il comando [az vm create](/cli/azure/vm#create) in modo da puntare al disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-189">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="d51f8-190">Assicurarsi che `--storage-account` corrisponda all'account di archiviazione in cui è archiviato il disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-190">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="d51f8-191">Non è necessario utilizzare lo stesso contenitore come disco personalizzato per archiviare le VM.</span><span class="sxs-lookup"><span data-stu-id="d51f8-191">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="d51f8-192">Assicurarsi di creare qualsiasi contenitore aggiuntivo seguendo la stessa procedura utilizzata in precedenza prima di caricare il disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d51f8-192">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="d51f8-193">L'esempio seguente crea una VM denominata `myVM` dal disco personalizzato:</span><span class="sxs-lookup"><span data-stu-id="d51f8-193">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="d51f8-194">È ancora necessario specificare tutti i parametri aggiuntivi richiesti dal comando **az vm create**, ad esempio nome utente e chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="d51f8-194">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="d51f8-195">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d51f8-195">Resource Manager template</span></span>
<span data-ttu-id="d51f8-196">I modelli di Azure Resource Manager sono file JavaScript Object Notation (JSON) che definiscono l'ambiente che si desidera generare.</span><span class="sxs-lookup"><span data-stu-id="d51f8-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="d51f8-197">I modelli sono suddivisi in diversi provider di risorse, ad esempio calcolo o rete.</span><span class="sxs-lookup"><span data-stu-id="d51f8-197">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="d51f8-198">È possibile utilizzare i modelli esistenti o crearne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="d51f8-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="d51f8-199">Altre informazioni sull' [uso di Resource Manager e relativi modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d51f8-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="d51f8-200">Nel provider `Microsoft.Compute/virtualMachines` del modello, è presente un nodo `storageProfile` contenente i dettagli sulla configurazione della VM.</span><span class="sxs-lookup"><span data-stu-id="d51f8-200">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="d51f8-201">I due parametri principali da modificare sono gli URI `image` e `vhd`, che puntano al disco personalizzato e al disco virtuale della nuova VM.</span><span class="sxs-lookup"><span data-stu-id="d51f8-201">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="d51f8-202">Di seguito viene mostrato un esempio di JSON per l'utilizzo di un disco personalizzato:</span><span class="sxs-lookup"><span data-stu-id="d51f8-202">The following shows an example of the JSON for using a custom disk:</span></span>

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

<span data-ttu-id="d51f8-203">È possibile usare [questo modello esistente per creare una VM da un'immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) oppure consultare le informazioni sulla [creazione di modelli di Azure Resource Manager personalizzati](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d51f8-203">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="d51f8-204">Dopo aver configurato un modello, creare le VM tramite il comando [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="d51f8-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="d51f8-205">Specificare l'URI del modello JSON con il parametro `--template-uri` :</span><span class="sxs-lookup"><span data-stu-id="d51f8-205">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="d51f8-206">Se si dispone di un file JSON archiviato localmente nel computer in uso, è possibile utilizzare il parametro alternativo `--template-file` :</span><span class="sxs-lookup"><span data-stu-id="d51f8-206">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="d51f8-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d51f8-207">Next steps</span></span>
<span data-ttu-id="d51f8-208">Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d51f8-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d51f8-209">È anche consigliabile [aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) alle nuove VM.</span><span class="sxs-lookup"><span data-stu-id="d51f8-209">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="d51f8-210">Se nelle VM sono in esecuzione applicazioni a cui si deve accedere, assicurarsi di [aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d51f8-210">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

