---
title: Caricare o copiare una macchina virtuale Linux personalizzata con l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Caricare o copiare una macchina virtuale personalizzata usando il modello di distribuzione di Resource Manager e l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 7c297725c26ea6c44403a10ecdcc3542f89f10b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="9eec7-103">Creare una macchina virtuale Linux da un disco personalizzato usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9eec7-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="9eec7-104">Questo articolo illustra come caricare un disco rigido virtuale personalizzato o copiare un disco rigido virtuale esistente in Azure e creare nuove macchine virtuali Linux dal disco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9eec7-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="9eec7-105">È possibile installare e configurare una distribuzione Linux in base ai propri requisiti e quindi usare il disco rigido virtuale per creare rapidamente una nuova macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9eec7-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="9eec7-106">Se si desidera creare più macchine virtuali dal disco personalizzato, si deve creare un'immagine dal disco rigido virtuale o dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9eec7-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="9eec7-107">Per altre informazioni vedere [Creare un'immagine personalizzata di una macchina virtuale di Azure tramite l'interfaccia della riga di comando](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="9eec7-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="9eec7-108">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="9eec7-108">You have two options:</span></span>
* [<span data-ttu-id="9eec7-109">Caricare un VHD</span><span class="sxs-lookup"><span data-stu-id="9eec7-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="9eec7-110">Copiare una VM di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="9eec7-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="9eec7-111">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="9eec7-111">Quick commands</span></span>

<span data-ttu-id="9eec7-112">Quando si crea una nuova macchina virtuale usando [az vm create](/cli/azure/vm#create) da un disco specializzato o personalizzato, **collegare** il disco (--attach-os-disk) anziché specificare un'immagine personalizzata o del marketplace (--image).</span><span class="sxs-lookup"><span data-stu-id="9eec7-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="9eec7-113">L'esempio seguente crea una macchina virtuale denominata *myVM* usando il disco gestito denominato *myManagedDisk* creato dal disco rigido virtuale personalizzato:</span><span class="sxs-lookup"><span data-stu-id="9eec7-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="9eec7-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="9eec7-114">Requirements</span></span>
<span data-ttu-id="9eec7-115">Per completare la procedura seguente, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9eec7-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="9eec7-116">Una macchina virtuale Linux che è stata preparata per l'uso in Azure.</span><span class="sxs-lookup"><span data-stu-id="9eec7-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="9eec7-117">La sezione [Preparare la macchina virtuale](#prepare-the-vm) di questo articolo descrive come trovare le informazioni specifiche della distribuzione relative all'installazione dell'Agente Linux di Azure (waagent) necessario affinché la macchina virtuale funzioni correttamente in Azure e l'utente possa connettersi tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="9eec7-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="9eec7-118">File VHD di una [distribuzione Linux approvata da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) esistente, oppure vedere le [informazioni sulle distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), in un disco virtuale in formato VHD.</span><span class="sxs-lookup"><span data-stu-id="9eec7-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="9eec7-119">Sono disponibili vari strumenti per la creazione di una VM e un file VHD:</span><span class="sxs-lookup"><span data-stu-id="9eec7-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="9eec7-120">Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione a usare il disco rigido virtuale come formato di immagine.</span><span class="sxs-lookup"><span data-stu-id="9eec7-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="9eec7-121">Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="9eec7-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="9eec7-122">È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="9eec7-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="9eec7-123">Il formato VHDX più recente non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="9eec7-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="9eec7-124">Quando si crea una VM, specificare VHD come formato.</span><span class="sxs-lookup"><span data-stu-id="9eec7-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="9eec7-125">Se necessario, è possibile convertire i dischi VHDX nel formato VHD usando [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o il cmdlet di PowerShell [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="9eec7-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="9eec7-126">Inoltre, Azure non supporta il caricamento di VHD dinamici, pertanto è necessario convertire tali dischi in VHD statici prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="9eec7-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="9eec7-127">Per convertire dischi dinamici durante il processo di caricamento in Azure, sono disponibili strumenti come [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) .</span><span class="sxs-lookup"><span data-stu-id="9eec7-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="9eec7-128">Assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9eec7-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9eec7-129">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="9eec7-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9eec7-130">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="9eec7-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="9eec7-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="9eec7-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="9eec7-132">Preparare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9eec7-132">Prepare the VM</span></span>

<span data-ttu-id="9eec7-133">Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="9eec7-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="9eec7-134">Gli articoli seguenti forniscono le istruzioni per preparare le diverse distribuzioni Linux supportate in Azure:</span><span class="sxs-lookup"><span data-stu-id="9eec7-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="9eec7-135">Distribuzioni basate su CentOS</span><span class="sxs-lookup"><span data-stu-id="9eec7-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="9eec7-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="9eec7-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="9eec7-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-139">SLES e openSUSE</span><span class="sxs-lookup"><span data-stu-id="9eec7-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9eec7-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="9eec7-141">Altro - Distribuzioni non approvate</span><span class="sxs-lookup"><span data-stu-id="9eec7-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="9eec7-142">Vedere anche le [Note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per suggerimenti più generali sulla preparazione di immagini Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="9eec7-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="9eec7-143">Il [Contratto di Servizio per la piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) è applicabile alle VM che eseguono Linux solo quando una distribuzione approvata viene usata con i dettagli di configurazione specificati nella sezione "Versioni e distribuzioni supportate" in [Distribuzioni di Linux supportate da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9eec7-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="9eec7-144">Opzione 1: caricare un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="9eec7-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="9eec7-145">È possibile caricare un disco rigido virtuale personalizzato in esecuzione in un computer locale o che è stato esportato da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="9eec7-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="9eec7-146">Per usare il disco rigido virtuale per creare una nuova macchina virtuale di Azure, è necessario caricare il disco rigido virtuale in un account di archiviazione e creare un disco gestito dal disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="9eec7-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="9eec7-147">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9eec7-147">Create a resource group</span></span>

<span data-ttu-id="9eec7-148">Prima di caricare il disco personalizzato e creare le VM, è necessario creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9eec7-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="9eec7-149">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *eastus*: [Panoramica di Azure Managed Disks](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9eec7-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="9eec7-150">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9eec7-150">Create a storage account</span></span>

<span data-ttu-id="9eec7-151">Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="9eec7-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="9eec7-152">Nell'esempio seguente viene creato un account di archiviazione denominato *mystorageaccount* nel gruppo di risorse creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="9eec7-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="9eec7-153">Ottenere chiavi degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9eec7-153">List storage account keys</span></span>
<span data-ttu-id="9eec7-154">Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9eec7-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="9eec7-155">Queste chiavi di accesso vengono usate per autenticarsi nell'account di archiviazione, ad esempio per eseguire operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="9eec7-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="9eec7-156">Ulteriori informazioni sulla [gestione dell'accesso all'archiviazione sono disponibili qui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9eec7-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="9eec7-157">Visualizzare le chiavi di accesso con [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="9eec7-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="9eec7-158">Visualizzare le chiavi di accesso per l'account di archiviazione creato:</span><span class="sxs-lookup"><span data-stu-id="9eec7-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="9eec7-159">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="9eec7-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="9eec7-160">Prendere nota di **key1** perché verrà usato per interagire con l'account di archiviazione nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="9eec7-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="9eec7-161">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9eec7-161">Create a storage container</span></span>
<span data-ttu-id="9eec7-162">Nello stesso modo in cui si creano directory diverse per organizzare in modo logico il file system locale si creano anche i contenitori con un account di archiviazione per organizzare i dischi.</span><span class="sxs-lookup"><span data-stu-id="9eec7-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="9eec7-163">Un account di archiviazione può contenere un numero qualsiasi di contenitori.</span><span class="sxs-lookup"><span data-stu-id="9eec7-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="9eec7-164">Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="9eec7-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="9eec7-165">Nell'esempio seguente viene creato un contenitore denominato *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="9eec7-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="9eec7-166">Caricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="9eec7-166">Upload the VHD</span></span>
<span data-ttu-id="9eec7-167">Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="9eec7-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="9eec7-168">Caricare e archiviare il disco personalizzato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="9eec7-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="9eec7-169">Specificare la chiave di accesso e il contenitore creato nel passaggio precedente, quindi selezionare il percorso del disco personalizzato sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="9eec7-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="9eec7-170">Il caricamento del disco rigido virtuale potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="9eec7-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="9eec7-171">Creare un disco gestito</span><span class="sxs-lookup"><span data-stu-id="9eec7-171">Create a managed disk</span></span>


<span data-ttu-id="9eec7-172">Creare un disco gestito dal disco rigido virtuale con [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="9eec7-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="9eec7-173">Nell'esempio seguente viene creato un disco gestito denominato *myManagedDisk* dal disco rigido virtuale caricato nell'account di archiviazione e nel contenitore denominati:</span><span class="sxs-lookup"><span data-stu-id="9eec7-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="9eec7-174">Opzione 2: copiare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="9eec7-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="9eec7-175">È anche possibile creare la macchina virtuale personalizzata in Azure, copiare il disco del sistema operativo e associarlo a una nuova macchina virtuale per crearne un'altra copia.</span><span class="sxs-lookup"><span data-stu-id="9eec7-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="9eec7-176">Questa è l'operazione corretta per il test, ma se si desidera usare una macchina virtuale di Azure esistente come modello per più macchine virtuali nuove, è effettivamente necessario creare un'**immagine**.</span><span class="sxs-lookup"><span data-stu-id="9eec7-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="9eec7-177">Per altre informazioni sulla creazione di un'immagine da una macchina virtuale di Azure esistente, vedere [Creare un'immagine personalizzata di una macchina virtuale di Azure tramite l'interfaccia della riga di comando](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="9eec7-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="9eec7-178">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="9eec7-178">Create a snapshot</span></span>

<span data-ttu-id="9eec7-179">Questo esempio crea uno snapshot di una macchina virtuale denominata *myVM* nel gruppo di risorse *myResourceGroup* e uno snapshot denominato *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="9eec7-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="9eec7-180">Creare il disco gestito</span><span class="sxs-lookup"><span data-stu-id="9eec7-180">Create the managed disk</span></span>

<span data-ttu-id="9eec7-181">Creare un nuovo disco gestito dallo snapshot.</span><span class="sxs-lookup"><span data-stu-id="9eec7-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="9eec7-182">Ottenere l'ID dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="9eec7-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="9eec7-183">In questo esempio, lo snapshot è denominato *osDiskSnapshot* ed è nel gruppo di risorse *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9eec7-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="9eec7-184">Creare il disco gestito.</span><span class="sxs-lookup"><span data-stu-id="9eec7-184">Create the managed disk.</span></span> <span data-ttu-id="9eec7-185">In questo esempio, si creerà un disco gestito denominato *myManagedDisk* dallo snapshot che ha una dimensione di 128 GB nell'archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="9eec7-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="9eec7-186">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="9eec7-186">Create the VM</span></span>

<span data-ttu-id="9eec7-187">A questo punto, creare la macchina virtuale con [az vm create](/cli/azure/vm#create) e collegare (--attach-os-disk) il disco gestito come disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9eec7-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="9eec7-188">L'esempio seguente crea una macchina virtuale denominata *myNewVM* usando il disco gestito creato dal disco rigido virtuale caricato:</span><span class="sxs-lookup"><span data-stu-id="9eec7-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="9eec7-189">Dovrebbe essere possibile accedere con SSH nella macchina virtuale usando le credenziali della macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="9eec7-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9eec7-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9eec7-190">Next steps</span></span>
<span data-ttu-id="9eec7-191">Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9eec7-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="9eec7-192">È anche consigliabile [aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) alle nuove VM.</span><span class="sxs-lookup"><span data-stu-id="9eec7-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="9eec7-193">Se nelle VM sono in esecuzione applicazioni a cui si deve accedere, assicurarsi di [aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9eec7-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

